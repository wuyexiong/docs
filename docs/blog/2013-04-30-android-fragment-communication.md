---
layout: post
title: "Android Fragment 之间的通讯处理"
date: 2013-04-30 21:38
comments: true
categories: Android
---

#上集回顾
上一次已经有结果了，有三种通讯方式  
文章连接:[Click Me](http://wuyexiong.github.io/blog/2013/04/30/android-fragment/)

1.使用接口,让Activity扮演管理角色,负责分发消息到该窗口的子View

2.使用LocalBroadcastManager + IntentFilter解决不同组件通讯,Intent负责搭载数据

3.EventBus 

4.otto 这里不做介绍，下面有demo链接，基于注解的解偶通信组件


其实按照MVC的思想，Activity就真正的变成了Controler，  
Activity中不涉及任何的业务逻辑的代码，只负责分发消息到不同的子View(Fragment)。   
如果希望整个应用只有一个Activity，就需要再抽象出一层Controller，负责处理Activity与其子Controller的通讯 


##相关下载

 - [EventBus项目托管](https://github.com/greenrobot/EventBus)
 - [EventBus-PPT](http://pan.baidu.com/share/link?shareid=440866&uk=2030412954)
 - [otto项目托管]([https://github.com/square/otto](https://github.com/square/otto)
 - [otto-demo](http://www.subsis.dk/24/otto-for-android)

##项目

我们直接看代码吧，因为表达能力还训练，加上有点懒 ^_^ 😄  
项目结构  
{% img [eclipse-project] /images/20130430-android-fragment-communication/eclipse-project.png %}
<!-- more -->
###首先是布局de代码
 - `/layout/article_view.xml` ** ArticleFragment.java ** 关联的布局
{% codeblock lang:xml %}
<?xml version="1.0" encoding="utf-8"?>
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/article"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    android:textSize="18sp" >
</TextView>
{% endcodeblock %}
   
 - `/layout/news_articles.xml` ** HeadlinesFragment.java ** 关联的布局

{% codeblock lang:xml %}
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/fragment_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >
</FrameLayout>
{% endcodeblock %}

 - `/layout-large/new_articles.xml` ** HeadlinesFragment.java ** 关联的布局，在平板大分辨率的时候回被自动启用  
{% codeblock lang:xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal" >

    <fragment
        android:id="@+id/headlines_fragment"
        android:name="tree.love.android.fragments.HeadlinesFragment"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1" />

    <fragment
        android:id="@+id/article_fragment"
        android:name="tree.love.android.fragments.ArticleFragment"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="2" />

</LinearLayout>
{% endcodeblock %}

 - `MainActivity.java` 首页 -_- 其实就那么一页  哈哈哈  
{% codeblock lang:java%}
public class MainActivity extends FragmentActivity  implements HeadlinesFragment.OnHeadlineSelectedListener {
	
	private static final String TAG = "MainActivity";

	private LocalBroadcastManager mBroadcastManager;
	private BroadcastReceiver mItemViewListClickReceiver;
	
	public static final String ACTION_ITEMVIEW_LISTCLICK = "tree.love.android.fragments.itemview.listclick";
	
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.news_articles);
        //如果是手机分辨率布局
        if (findViewById(R.id.fragment_container) != null) {

        	// 如果之前保存了状态,我们不需要做任何事情,否则会重复加载Fragment
            if (savedInstanceState != null) {
                return;
            }
            // Create an instance of ExampleFragment
            HeadlinesFragment firstFragment = new HeadlinesFragment();

            //如果这个Activity被一个特殊的Intent传递,如果有需要,把该数据也传给Fragment
            firstFragment.setArguments(getIntent().getExtras());

            // 添加该Fragment到R.id.fragment_container这个容器布局中
            getSupportFragmentManager().beginTransaction()
                    .add(R.id.fragment_container, firstFragment).commit();
        }
    }

	private void initBroadcastListener() {
		mBroadcastManager = LocalBroadcastManager.getInstance(this);
        IntentFilter intentFilter = new IntentFilter();
        intentFilter.addAction(ACTION_ITEMVIEW_LISTCLICK);
        mItemViewListClickReceiver = new BroadcastReceiver()
		{
			@Override
			public void onReceive(Context context, Intent intent)
			{
				if(intent.getAction().equals(ACTION_ITEMVIEW_LISTCLICK))
				{
					Log.v(TAG, ACTION_ITEMVIEW_LISTCLICK + "," + intent.getIntExtra("position", -1));
				}
			}
		};
        mBroadcastManager.registerReceiver(mItemViewListClickReceiver, intentFilter);
	}

    /* 
     * 实现HeadlinesFragment.OnHeadlineSelectedListener中的ListView点击事件的回调接口
     */
    public void onArticleSelected(int position) {

        // 获取当前Activity是否已经加载了ArticleFragment
        ArticleFragment articleFrag = (ArticleFragment)
                getSupportFragmentManager().findFragmentById(R.id.article_fragment);

        if (articleFrag != null) {
        	//如果进到这里,说明我们正在使用大屏幕布局/.
        	//直接更新ArticleFragment的布局
            articleFrag.updateArticleView(position);

        } else {
            // 我们正在使用小屏幕布局
            // 创建Fragment,并且传递参数
            ArticleFragment newFragment = new ArticleFragment();
            Bundle args = new Bundle();
            args.putInt(ArticleFragment.ARG_POSITION, position);
            newFragment.setArguments(args);
            FragmentTransaction transaction = getSupportFragmentManager().beginTransaction();

            //可定制Fragment的退出和进入动画 , 设置在replace or add之前
            transaction.setCustomAnimations(android.R.anim.fade_in, android.R.anim.fade_out, android.R.anim.fade_in, android.R.anim.fade_out);
            
            // 替换R.id.fragment_container容器布局中的View
            transaction.replace(R.id.fragment_container, newFragment);
            
            // 添加事物回退栈,让系统管理,当用户点击返回按钮时,销毁当前加载到容器布局中的ArticleFragment
            transaction.addToBackStack(null);
            
            // 提交事物...不然你永远看不到ArticleFragment的出现 ^_^
            transaction.commit();
        }
    }
    
    /**
     * EventBus事件回掉
     * @param event
     */
    public void onEvent(ListClickEvent event)
    {
    	Log.v("", "onEvent position:" + event.getPosition());
    }
    
    @Override
    protected void onStart() {
    	super.onStart();
    	//在需要接收事件通知的类添加到EventBus
        EventBus.getDefault().register(this);
        //注册Receiver
        initBroadcastListener();
    }
    
    @Override
    protected void onPause()
    {
    	super.onPause();
    	//取消事件监听
    	EventBus.getDefault().unregister(this);
    	mBroadcastManager.unregisterReceiver(mItemViewListClickReceiver);
    }
}
{% endcodeblock %}

 - `HeadlinesFragment.java` ListView菜单布局
{% codeblock lang:java%}
 public class HeadlinesFragment extends ListFragment {
    OnHeadlineSelectedListener mCallback;

    // 通讯接口, 加载该Fragment的容器Activity必须实现此接口可以接收ListView的点击消息
    public interface OnHeadlineSelectedListener {
        /** 当HeadlinesFragment中的ListView点击的时候触发 */
        public void onArticleSelected(int position);
    }

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        int layout = Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB ? android.R.layout.simple_list_item_activated_1 : android.R.layout.simple_list_item_1;
        setListAdapter(new ArrayAdapter<String>(getActivity(), layout, Ipsum.Headlines));
    }

    @Override
    public void onStart() {
        super.onStart();

        if (getFragmentManager().findFragmentById(R.id.article_fragment) != null) {
            getListView().setChoiceMode(ListView.CHOICE_MODE_SINGLE);
        }
    }

    @Override
    public void onAttach(Activity activity) {
        super.onAttach(activity);

        // 保证容器Activity实现了回调接口 否则抛出异常警告
        try {
            mCallback = (OnHeadlineSelectedListener) activity;
        } catch (ClassCastException e) {
            throw new ClassCastException(activity.toString()  + " must implement OnHeadlineSelectedListener");
        }
    }

    @Override
    public void onListItemClick(ListView l, View v, int position, long id) {
        //1.通讯方式1  接口通知Activity
        mCallback.onArticleSelected(position);
        
        //2.通讯方式2  发送广播
        Intent intent = new Intent(MainActivity.ACTION_ITEMVIEW_LISTCLICK);
        intent.putExtra("position", position);
        LocalBroadcastManager.getInstance(getActivity()).sendBroadcast(intent);
        
        //3.通讯方式3  发送事件到消息中心,由消息中心负责分发事件
        EventBus.getDefault().post(new ListClickEvent(position));
        
        // 大屏幕pad分辨率使用两个panel的时候设置
        getListView().setItemChecked(position, true);
    }
}
{% endcodeblock %}

 - `ArticleFragment.java` 详情页布局。。就一个TextView啦。
{% codeblock lang:java %}
 public class ArticleFragment extends Fragment {
	
    final static String ARG_POSITION = "position";
    int mCurrentPosition = -1;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, 
        Bundle savedInstanceState) {

    	//回复在onSaveInstanceState中保存的是状态数据
        if (savedInstanceState != null) {
            mCurrentPosition = savedInstanceState.getInt(ARG_POSITION);
        }

        return inflater.inflate(R.layout.article_view, container, false);
    }

    @Override
    public void onStart() {
        super.onStart();

        Bundle args = getArguments();
        if (args != null) {
            updateArticleView(args.getInt(ARG_POSITION));
        } else if (mCurrentPosition != -1) {
            updateArticleView(mCurrentPosition);
        }
        
        EventBus.getDefault().register(this);
    }
    
    @Override
    public void onPause()
    {
    	super.onPause();
    	EventBus.getDefault().unregister(this);
    }

    public void updateArticleView(int position) {
        TextView article = (TextView) getActivity().findViewById(R.id.article);
        article.setText(Ipsum.Articles[position]);
        mCurrentPosition = position;
    }

    @Override
    public void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        outState.putInt(ARG_POSITION, mCurrentPosition);
    }
    
    public void onEvent(ListClickEvent event)
    {
    	Log.v("ArticleFragment", "onEvent" + event.getPosition());
    }
}
{% endcodeblock %}

