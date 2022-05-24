---
layout: post
title: "记录一段工具代码，很久以前写的加密解密字符串的方法"
date: 2013-04-30 16:57
comments: true
categories: Java
---

{% codeblock lang:java %}
/** 
     * 字符串加密 
     * @param passWord 加密密码 
     * @return 
     * @throws Exception 
     */  
    public static String encryptPassword(String passWord)throws Exception  
    {  
//        KeyGenerator keyGenerator = KeyGenerator.getInstance("PBEWithMD5AndDES");  
        SecretKeyFactory keyFactory = SecretKeyFactory.getInstance("PBEWithMD5AndDES");            
        KeySpec keySpec = new PBEKeySpec("123123123".toCharArray());  
        SecretKey secretKey = keyFactory.generateSecret(keySpec);
          
        PBEParameterSpec parameterSpec = new PBEParameterSpec(new byte[]{1,2,3,4,5,6,7,8},1000);  
        Cipher cipher = Cipher.getInstance("PBEWithMD5AndDES");
        cipher.init(Cipher.ENCRYPT_MODE, secretKey, parameterSpec);
        byte passEn[] = cipher.doFinal(passWord.getBytes());
        System.out.println(" haha 1" + new String(passEn,"UTF-8"));
        return bytesToHexString(passEn);  
    }  
{% endcodeblock %}
<!-- more -->
      
{% codeblock lang:java %}
    /** 
     * 字符串解密 
     * @param passWordEn 加密后的密码 
     * @return 
     * @throws Exception 
     */  
    public static String decryptPassword(String passWordEn) throws Exception  
    {  
        SecretKeyFactory keyFactory = SecretKeyFactory.getInstance("PBEWithMD5AndDES");
        KeySpec keySpec = new PBEKeySpec("123123123".toCharArray());  

        SecretKey secretKey = keyFactory.generateSecret(keySpec);  
        PBEParameterSpec parameterSpec = new PBEParameterSpec(new byte[]{1,2,3,4,5,6,7,8},1000);  
          
        Cipher cipher = Cipher.getInstance("PBEWithMD5AndDES");  
        cipher.init(Cipher.DECRYPT_MODE, secretKey, parameterSpec);  
        byte[] passDec = cipher.doFinal(hexStringToBytes(passWordEn));  
        return new String(passDec);  
    }  
      
      
    public static String bytesToHexString(byte[] src)  
    {  
        StringBuilder stringBuilder = new StringBuilder("");  
        if (src == null || src.length <= 0)  
        {  
            return null;  
        }  
        for (int i = 0; i < src.length; i++)  
        {  
            int v = src[i] & 0xFF;  
            String hv = Integer.toHexString(v);  
            if (hv.length() < 2)  
            {  
                stringBuilder.append(0);  
            }  
            stringBuilder.append(hv);  
        }  
        return stringBuilder.toString();  
    }  
      
    public static byte[] hexStringToBytes(String hexString)  
    {  
        if (hexString == null || hexString.equals(""))  
        {  
            return null;  
        }  
        hexString = hexString.toUpperCase();  
        int length = hexString.length() / 2;  
        char[] hexChars = hexString.toCharArray();  
        byte[] d = new byte[length];  
        for (int i = 0; i < length; i++)  
        {  
            int pos = i * 2;  
            d[i] = (byte)(charToByte(hexChars[pos]) << 4 | charToByte(hexChars[pos + 1]));  
        }  
        return d;  
    }  
  
    private static byte charToByte(char c)  
    {  
        return (byte)"0123456789ABCDEF".indexOf(c);  
    }  
{% endcodeblock %}