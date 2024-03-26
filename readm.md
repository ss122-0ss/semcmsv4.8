# Semcms latest version(v4.8) allow Arbitrary file upload when it runs on a windows server whose hard drive patition is NTFS.

## 1. We should log in to the Web Administrator Console.

![image-20240326165720634](C:\Users\28162\AppData\Roaming\Typora\typora-user-images\image-20240326165720634.png)

Choose a jpg webshell,whose content is

```
 <?php phpinfo();?>
```

![image-20240326170256513](C:\Users\28162\AppData\Roaming\Typora\typora-user-images\image-20240326170256513.png)

### Afterward, click the "Submit" button, and then interupt and observe the HTTP request in Burp Suite.



![image-20240326170745700](C:\Users\28162\AppData\Roaming\Typora\typora-user-images\image-20240326170745700.png)





### Manually change the “wname” param to “1.jpg.php:”  andin Burp Suite(see picture below).

![image-20240326171029751](C:\Users\28162\AppData\Roaming\Typora\typora-user-images\image-20240326171029751.png)



## And the response will show the path & filename(../Images/projoucts/1.jpg.php) you just uploaded.



### **However, due to the characteristics of NTFS, the actual file will appear as a 0kb-sized "111.jpg.php," rather than the "111.jpg.php:.jpg" shown in response.**

![image-20240326171137261](C:\Users\28162\AppData\Roaming\Typora\typora-user-images\image-20240326171137261.png)

## 3. (Key point) Rewrite the zero-KB webshell

### Place the HTTP data packet from the recent "Submit" click into Burp's Repeater, preparing to make modifications before resending it once again.

![image-20240326171506623](C:\Users\28162\AppData\Roaming\Typora\typora-user-images\image-20240326171506623.png)



### By accessing the webshell file from the URL http://localhost/semcms/images/prdoucts/1.jpg.php, the malicious code is executed.

![image-20240326171656760](C:\Users\28162\AppData\Roaming\Typora\typora-user-images\image-20240326171656760.png)