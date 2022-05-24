---
layout: post
title: "Best resources for Android development"
date: 2014-05-14 20:22
comments: true
categories: Android
tags: [Android, Android开发, 安卓开发, Android资源, Android Resource]
keywords: Android, Android开发, 安卓开发, Android资源, Android Resource
---

From: <http://www.androidauthority.com/best-resources-android-development-372414/>


![android developer development][1]

   [1]: http://cdn04.androidauthority.net/wp-content/uploads/2014/05/android-developer-development-710x470.jpg

[Alper Çuğun][2]

   [2]: https://www.flickr.com/photos/alper/9311087323/in/photolist-5L3aL7-7tMf8K-b4eRR-fbMKSk-67jXuH-8khnRM-8FDxBW-5U8MeL-5PkuHo-qkm17-cdyrGQ-dB7P9-azfVn9-qF4kP-9DDr6M-ifdAm5-59yWNu-4m84mh-91Zwx9-7eFrjw-8aAVst-8aEbsj-efQ9DN-4m41TD-dstqWC-7gg12S-8aAV1i-xcE8k-Q39Rk-ggBEsp-4m84rY-bqUfmk-iFvtS-CGWNK-axV3Y4-aXnWdi-CGWYa-CGX7U-CGX4t-41m2A-CGWUF-5LrzQZ-CGWHc-CGWCy-66Nbn4-sNcQb-8w6duo-87Kfxa-gYeprU-ghX2B7/

Whether you’re a seasoned professional or just beginning with Android development, this list of resources (including tools, libraries, and blogs) is useful for any developer or team on just about any project, big or small. 

## OkHttp 

[![GitHub Square Ok][3]][4]

   [3]: http://cdn04.androidauthority.net/wp-content/uploads/2014/05/GitHub-Square-Ok-710x274.jpg
   [4]: http://square.github.io/okhttp/

OkHttp, a product of [Square][5], is an open-source HTTP and SPDY library for Android and Java. Android comes with two existing HTTP frameworks ([HttpURLConnection][6] and [HttpClient][7]) but over various Android OS versions have been rife with bugs that can make any normally-sane developer go nuts trying to nail down an HTTP problem. Fortunately, OkHttp solves many of the problems. OkHttp is built upon HttpUrlConnection — so the API should be familiar — but stays up-to-date with fixes from the Android codebase, meaning no compatibility nightmares with older OS versions. Oh, and if you’re looking for something that implements the Apache HttpClient API, that exists as a module: _okhttp-apache_. 

   [5]: http://corner.squareup.com/
   [6]: http://developer.android.com/reference/java/net/HttpURLConnection.html
   [7]: http://developer.android.com/reference/org/apache/http/client/HttpClient.html

Check out [OkHttp][8]
<!-- more -->

   [8]: http://square.github.io/okhttp/

## Retrofit 

[![Retrofit][9]][10]

   [9]: http://cdn01.androidauthority.net/wp-content/uploads/2014/05/Retrofit.jpg
   [10]: http://square.github.io/retrofit/

Retrofit, also a product of Square, is an open-source, type-safe REST client for Android and Java. The Android platform doesn’t lend itself much to simple client-server interaction when it comes to APIs. Retrofit aims to provide that, at least for [REST][11] requests. Retrofit supports quite a bit of customization, but out of the box will use GSON for JSON-parsing and saves a ton of time building form and multipart requests by simplifying it all into a straightforward interface. Bonus: Retrofit will use OkHttp if it’s available. 

   [11]: http://en.wikipedia.org/wiki/Representational_state_transfer

Check out [Retrofit][12]

   [12]: http://square.github.io/retrofit/

## Picasso 

[![Picasso][13]][14]

   [13]: http://cdn02.androidauthority.net/wp-content/uploads/2014/05/Picasso.jpg
   [14]: http://square.github.io/picasso/

Alright, this is the last Square open-source project I’ll list here, I promise (but there are plenty more you should [check out][15]). Picasso is an image downloading and caching library sporting a [fluent interface][16] for ease of use. Picasso has many options for customizing how it handles the downloaded image (including things like resizing and cropping, as well as providing an interface allowing you to transform the image how you see fit, such as [performing a circle crop][17] on it). Picasso will download the image (if not cached) and load it into the given target, which can be anything implementing the [Target interface][18] or in its simplest and most common usage, an ImageView. 

   [15]: http://square.github.io/
   [16]: http://en.wikipedia.org/wiki/Fluent_interface
   [17]: https://gist.github.com/Aracem/8913410/13f7abea0c43bb8647aaf3cb0d0c090471b85a69
   [18]: https://github.com/square/picasso/blob/master/picasso/src/main/java/com/squareup/picasso/Target.java

Check out [Picasso][19]

   [19]: http://square.github.io/picasso/

## AndroidViews 

[![Android Views][20]][21]

   [20]: http://cdn01.androidauthority.net/wp-content/uploads/2014/05/Android-Views-710x236.jpg
   [21]: http://www.androidviews.net/

AndroidViews.net is a site that aims to bring together many of the different tools, libraries, and resources into a browsable index. Unfortunately, there’s no search functionality and the site definitely isn’t comprehensive, so you’ll probably also want to check out the next resource on my list… 

Check out [AndroidViews][22]

   [22]: http://www.androidviews.net/

## Android Weekly 

[![Android Weekly][23]][24]

   [23]: http://cdn01.androidauthority.net/wp-content/uploads/2014/05/Android-Weekly-710x341.jpg
   [24]: http://androidweekly.net/

If there’s any mailing list you should ever want to be on, this is probably the first. Android Weekly is a newsletter of various musings in the Android development community, including new libraries, tools, blog posts, and more. If you don’t have email (is that a possibility?) or you just don’t like the prospect of giving them your email address, you can always check the site every Monday for the latest issue. 

Check out [Android Weekly][25]

   [25]: http://androidweekly.net/

## Android Niceties 

[![android niceties][26]][27]

   [26]: http://cdn02.androidauthority.net/wp-content/uploads/2014/05/android-niceties-710x197.jpg
   [27]: http://androidniceties.tumblr.com/

Android Niceties is a great collections of well-designed and thoughtfully-developed experiences in the Android ecosystem. Android Niceties has covered great, from major brand apps like [Duolingo][28], [Expedia][29], and [Etsy][30] to perhaps previously lesser-known apps like [Muzei][31], [Timely][32], and [Pocket][33]. 

   [28]: https://play.google.com/store/apps/details?id=com.duolingo
   [29]: https://play.google.com/store/apps/details?id=com.expedia.bookings
   [30]: https://play.google.com/store/apps/details?id=com.etsy.android
   [31]: https://play.google.com/store/apps/details?id=net.nurik.roman.muzei
   [32]: https://play.google.com/store/apps/details?id=ch.bitspin.timely
   [33]: https://play.google.com/store/apps/details?id=com.ideashower.readitlater.pro

Check out [Android Niceties][34]

   [34]: http://androidniceties.tumblr.com/

## Android Lifecycle 

[![Github-Android-Lifecycle][35]][36]

   [35]: http://cdn04.androidauthority.net/wp-content/uploads/2014/05/Github-Android-Lifecycle-710x287.jpg
   [36]: https://github.com/xxv/android-lifecycle

Touting itself as the “Complete Android Fragment & Activity Lifecycle” (I haven’t completely verified this, but it looks right…), this graph outlines the flow of Activity and Fragment in relation to user interaction within and outside of your application. 

Check out [Android Lifecycle][37]

   [37]: https://github.com/xxv/android-lifecycle

## Android Asset Studio 

![Android Asset Studio][38]

   [38]: http://cdn04.androidauthority.net/wp-content/uploads/2014/05/Android-Asset-Studio-710x337.jpg

This site has a myriad of tools built into it to simplify the creation of various Android-related resources including launcher icons, notification icons, navigation drawer icons, and more… 

Check out [Android Asset Studio][39]

   [39]: http://android-ui-utils.googlecode.com/hg/asset-studio/dist/index.html

## Android Holo Colors Generator 

[![Android Holo Colors Generator][40]][41]

   [40]: http://cdn02.androidauthority.net/wp-content/uploads/2014/05/Android-Holo-Colors-Generator-710x401.jpg
   [41]: http://android-holo-colors.com/

Built upon the Android Asset Studio, this tool simplifies the previously design-resource encumbering process of creating custom Holo-style Android widgets. Just plug in a color, specify your action bar theme, and get going! 

Check out [Android Holo Colors Generator][42]

   [42]: http://android-holo-colors.com/

## DPI Calculator for Android 

[![DPI Calculator for Android][43]][44]

   [43]: http://cdn01.androidauthority.net/wp-content/uploads/2014/05/DPI-Calculator-for-Android--710x314.jpg
   [44]: http://jennift.com/dpical.html

It is what it says it is. This tool is simple and elegant, allowing the user to plug in a number at any density (yeah, even tvdpi) and will calculate the value for any other density. This one’s a keeper for sure. 

Check out [DPI Calculator for Android][45]

   [45]: http://jennift.com/dpical.html

## Android Developers YouTube Channel 

[![Android Developers YouTube][46]][47]

   [46]: http://cdn03.androidauthority.net/wp-content/uploads/2014/05/Android-Developers-YouTube-710x334.jpg
   [47]: https://www.youtube.com/user/androiddevelopers

This one might seem a bit more obvious, but maybe you’re not subscribed to it. If you aren’t, you should be. Google is shifting its focus for Android (and the rest of its company, I hear) to be more design-oriented. This is and almost certainly will continue to be where you can find out much more about Android development, design, and UX — old and new. I also recommend the [Google Developers channel][48] if you’re into that kind of thing. 

   [48]: https://www.youtube.com/user/GoogleDevelopers

Check out the [Android Developers YouTube Channel][49]

   [49]: https://www.youtube.com/user/androiddevelopers

## Gradle, please 

[![Gradle Please][50]][51]

   [50]: http://cdn03.androidauthority.net/wp-content/uploads/2014/05/Gradle-Please-710x442.jpg
   [51]: http://gradleplease.appspot.com/

Thinking about switching to Gradle and need some help with your dependencies? Have been on Gradle but just want to simplify the dependency search? Look no further than _Gradle, please_. Plug in the name of your favorite library (heck, I dunno, maybe OkHttp, Picasso, or Retrofit?) and _Gradle, please_ will spit out your dependencies “compile” line ready to go. If you’re looking for something a little more complex, you can always check out [The Central Repository][52]. _Gradle, please_ also happens to provide all of the standard Google-provided dependencies at the top of the page for your convenience. 

   [52]: http://search.maven.org/

Check out [Gradle, please][53]

   [53]: http://gradleplease.appspot.com/

… and last but certainly, not least: 

## android/platform frameworks base 

[![GitHub-Android-Platform][54]][55]

   [54]: http://cdn03.androidauthority.net/wp-content/uploads/2014/05/GitHub-Android-Platform-710x256.jpg
   [55]: https://github.com/android/platform_frameworks_base

You might be wondering why I’m listing this. Well, I can’t tell you how many times I’ve been through this codebase. I don’t generally sift through on my local machine; rather, [I peruse the Android source on Github’s website][56]. Typically, I’ll be wondering how something works (like the complexities of [ListView][57]/[AdapterView][58], or the new hotness that is [TransitionManager][59]) and want to check it out — this is the best place to really dig in. Oh, and in case you’re still feeling adventurous, there’s also the [support library source][60] to browse. 

   [56]: http://dallasgutauckis.com/2012/04/25/looking-at-android-source-quickly/
   [57]: https://github.com/android/platform_frameworks_base/blob/master/core/java/android/widget/ListView.java
   [58]: https://github.com/android/platform_frameworks_base/blob/master/core/java/android/widget/AdapterView.java
   [59]: https://github.com/android/platform_frameworks_base/blob/master/core/java/android/transition/TransitionManager.java
   [60]: https://github.com/android/platform_frameworks_support

Check out [android/platform frameworks base][61]

   [61]: https://github.com/android/platform_frameworks_base

Happy developing, everyone. Please, share your favorite resources in the comments! 


[Android design][62][Android Developers][63][Android Development][64]

   [62]: http://www.androidauthority.com/tag/android-design/
   [63]: http://www.androidauthority.com/tag/android-developers/
   [64]: http://www.androidauthority.com/tag/android-development/

