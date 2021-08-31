# Quick Summary

This is another easy linux box. I think the box is a pretty fun because it is easy and straightforward, there is no falling down the rabbit hole. 

While enumerating, we discover a few things from the index page and locate a secret file which gives us access to admin panel. On admin panel, we get a reverse shell through templates. Once in the box we come across an archived xxd dump. We recover the dump and extract the password that belongs to a user. In that user's home directory we find another interesting folder. The folder contains two files that are strongly related. We abuse a curl configuration to read the root flag as curl executes as root.
