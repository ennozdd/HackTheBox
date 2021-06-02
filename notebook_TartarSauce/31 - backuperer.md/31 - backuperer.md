# 35 - backuperer


# /usr/sbin/backuperer
```
#!/bin/bash

#-------------------------------------------------------------------------------------
# backuperer ver 1.0.2 - by ȜӎŗgͷͼȜ
# ONUMA Dev auto backup program
# This tool will keep our webapp backed up incase another skiddie defaces us again.
# We will be able to quickly restore from a backup in seconds ;P
#-------------------------------------------------------------------------------------

# Set Vars Here
basedir=/var/www/html
bkpdir=/var/backups
tmpdir=/var/tmp
testmsg=$bkpdir/onuma_backup_test.txt
errormsg=$bkpdir/onuma_backup_error.txt
tmpfile=$tmpdir/.$(/usr/bin/head -c100 /dev/urandom |sha1sum|cut -d' ' -f1)
check=$tmpdir/check

# formatting
printbdr()
{
    for n in $(seq 72);
    do /usr/bin/printf $"-";
    done
}
bdr=$(printbdr)

# Added a test file to let us see when the last backup was run
/usr/bin/printf $"$bdr\nAuto backup backuperer backup last ran at : $(/bin/date)\n$bdr\n" > $testmsg

# Cleanup from last time.
/bin/rm -rf $tmpdir/.* $check

# Backup onuma website dev files.
/usr/bin/sudo -u onuma /bin/tar -zcvf $tmpfile $basedir &

# Added delay to wait for backup to complete if large files get added.
/bin/sleep 30

# Test the backup integrity
integrity_chk()
{
    /usr/bin/diff -r $basedir $check$basedir
}

/bin/mkdir $check
/bin/tar -zxvf $tmpfile -C $check
if [[ $(integrity_chk) ]]
then
    # Report errors so the dev can investigate the issue.
    /usr/bin/printf $"$bdr\nIntegrity Check Error in backup last ran :  $(/bin/date)\n$bdr\n$tmpfile\n" >> $errormsg
    integrity_chk >> $errormsg
    exit 2
else
    # Clean up and save archive to the bkpdir.
    /bin/mv $tmpfile $bkpdir/onuma-www-dev.bak
    /bin/rm -rf $check .*
    exit 0
fi
```

Here is a quick summary of the executable
1 - Deletes /var/tmp/.\<hash> and /var/tmp/check/
2 - Takes a backup of  /var/www/html as a tar file in /var/tmp/.\<hash> as user **onuma**
3 - Sleeps 30 seconds
4 - Extracts tar file into /var/tmp/check as **root** this time
5 - Checks if the backup file is properly compressed, if it is compressed as expected, decompressed /var/tmp/check folder will get deleted, if it isn't, check folder will be left there for troubleshooting

Important things to note
1- Since initial backup is run by onuma, the user **onuma** has read & write acces to /var/tmp/.\<hash> tar file
2- It waits 30 seconds before decompressing as **root**.

We can change the tar file in between 30 seconds, in order to elevate privileges we can inject a setuid binary into the tar file because root is decompressing it, tar should preserve the permissions on our setuid binary.

[See 30 - Root.md](/home/kali/htb/tartarsauce/notes/30%20-%20Root.md)
