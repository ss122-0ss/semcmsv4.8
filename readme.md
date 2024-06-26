# Semcms latest version(v4.8) allow Arbitrary file upload when it runs on a windows server whose hard drive patition is NTFS.

- **Exploit Title:**  Semcms latest version(v4.8) allow Arbitrary file upload when it runs on a windows server whose hard drive patition is NTFS.
- **Date:** 2024-04-01
- **Exploit Author:** shuo sheng,jixin zhang
- **Vendor Homepage:** [https://code-projects.org/simple-school-management-in-php-with-source-code/](http://www.sem-cms.com/)
- **Software Link:** [https://download.code-projects.org/details/d10e92aa-e37f-46fd-9bf8-45878956d7c0](http://www.sem-cms.com/TradeCmsdown/php/semcms_php_4.8.zip)
- **Version:** Semcms v4.8

The code vulnerability exists in SECMMS_upload.php
![图片](https://github.com/ss122-0ss/semcmsv4.8/assets/131983607/74c96af7-75ea-4743-bcee-1fb66083c584)

## 1. We should log in to the Web Administrator Console.

![图片](https://github.com/ss122-0ss/semcmsv4.8/assets/131983607/2061afa7-35a9-45e5-a298-a2b385c48188)


Choose a jpg webshell,whose content is

```
 <?php phpinfo();?>
```



### Afterward, click the "Submit" button, and then interupt and observe the HTTP request in Burp Suite.


![图片](https://github.com/ss122-0ss/semcmsv4.8/assets/131983607/87eb60a3-e2b1-4673-939b-16e896dab231)



### Manually change the “wname” param to “1.jpg.php:”  andin Burp Suite(see picture below).

![图片](https://github.com/ss122-0ss/semcmsv4.8/assets/131983607/99cac086-d518-4722-b4cc-c055e2f25aa5)


## And the response will show the path & filename(../Images/projoucts/1.jpg.php) you just uploaded.

### **However, due to the characteristics of NTFS, the actual file will appear as a 0kb-sized "111.jpg.php," rather than the "111.jpg.php:.jpg" shown in response.**
![图片](https://github.com/ss122-0ss/semcmsv4.8/assets/131983607/93e5198b-f40d-492a-bdd3-e96a023e43ca)


## 3. (Key point) Rewrite the zero-KB webshell

### Place the HTTP data packet from the recent "Submit" click into Burp's Repeater, preparing to make modifications before resending it once again.

![图片](https://github.com/ss122-0ss/semcmsv4.8/assets/131983607/50aa8980-b5f4-4931-b0bf-4b04591746ad)



### By accessing the webshell file from the URL http://localhost/semcms/images/prdoucts/1.jpg.php, the malicious code is executed.

![图片](https://github.com/ss122-0ss/semcmsv4.8/assets/131983607/a53bcc4a-6581-4e6a-a4d4-d04b1e5d6bd6)

