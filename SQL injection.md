# ZZCMS SQL injection in  /user/jobmanage.php via bigclass parameter
## CMS version
zzcms 8.3 Download link:http://www.zzcms.net/about/6.htm
## Vulnerability location
By default, the ZZCMS framework performs security filtering on the $_GET request and the $_POST request parameter via the addslashes() function.
![](https://github.com/seedis/zzcms/blob/master/image/5.png)
But /user/jobmanage.php in line 42-47,the parameter **bigclass** comes from $_REQUEST function that can bypass ZZCMS security filtering lead to SQL injection.
![](https://github.com/seedis/zzcms/blob/master/image/3.png)

## POC
![](https://github.com/seedis/zzcms/blob/master/image/4.png)
