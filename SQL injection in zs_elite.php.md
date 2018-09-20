### ZZCMS V8.3 SQL injection in /user/zs_elite.php line 48 via id parameter
## Vulnerability CMS and version
zzcms v8.3   Download link:http://www.zzcms.net/download/zzcms8.3.zip
## Triggering conditions
Log in to access the zs_elite.php page
## Vulnerability details
in CMS /user/zs_elite.php line 48,id parameter value comes from $_REQUEST function that can bypass cms security filtering.
![](https://github.com/seedis/zzcms/blob/master/image/11.png)
The value of the id parameter is finally brought to line 118 [/user/zs_elite.php], and the final SQL statement is executed, resulting in SQL injection.
![](https://github.com/seedis/zzcms/blob/master/image/22.png)
## POC
```
http://192.168.30.216/user/zs_elite.php?id=-11' union select 1,'test',user(),4,5%23&page=1
```
![](https://github.com/seedis/zzcms/blob/master/image/33.png)
