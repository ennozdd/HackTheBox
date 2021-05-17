# 10 - MyPlace

![](vx_images/1680345664295.png)


# Gobuster is having an issue.

```sql
$ gobuster dir -u http://10.10.10.58:3000 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o gobuster/initial.log                     
===============================================================                                                                                              
Gobuster v3.1.0                                                                                                                                              
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)                                                                                                
===============================================================                                                                                              
[+] Url:                     http://10.10.10.58:3000                                                                                                         
[+] Method:                  GET                                              
[+] Threads:                 10                                                                                                                              
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt                                                                    
[+] Negative Status codes:   404                                                                                                                             
[+] User Agent:              gobuster/3.1.0                                                                                                                  
[+] Timeout:                 10s                                                                                                                             
===============================================================               
2021/05/15 15:30:31 Starting gobuster in directory enumeration mode                                                                                          
===============================================================               
Error: the server returns a status code that matches the provided options for non existing urls. http://10.10.10.58:3000/99a05f91-2832-43a9-84e2-f9990261f75b
 => 200 (Length: 3861). To continue please exclude the status code, the length or use the --wildcard switch
```



# It seems we are blocked because of our user agent

![](vx_images/5261288594390.png)


# The other problem is that instead of giving 404 status page the server redirects the user to the index page.


![](vx_images/5974484576862.png)


# Burp suite logged some interesting files and folders

![](vx_images/3738565728328.png)




#  api directory has some credentials

![](vx_images/78128228786.png)



# sha256 crack


![](vx_images/4643630575401.png)


# Logging in as tom

![](vx_images/5769918849556.png)


# /partials/admin.html is never requested by the browser but it is referenced in one of the javascript files

![](vx_images/4634157536198.png)



# admin.html
Unfortunately Download Backup button doesn't work

![](vx_images/3298757082676.png)


# Another interesting directory


![](vx_images/831211897020.png)

# We find the username and the sha256 password of the admin user

![](vx_images/1237022767206.png)


# Luckly it is in the Crackstation's database

![](vx_images/70596871346.png)

# Logging in as admin 

![](vx_images/2218301492886.png)


