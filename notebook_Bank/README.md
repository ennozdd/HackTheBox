# Quick Summary

Bank is a fairly simple box. Path to foothold starts after we find the virtual host. Generally in htb, virtual hostname is the same as the box's name so our calculated guess would be bank.htb. There is, in fact, a virtual host routing with bank.htb. It welcomes us with a simple login page. However, We manage to get a reverse shell without any credentials using file upload feature . Once in the box we notice /etc/passwd is writable. Older versions of linux allow password hashes in /etc/passwd. We change the password in /etc/passwd to get root on the box.
