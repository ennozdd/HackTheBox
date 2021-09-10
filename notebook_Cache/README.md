# Quick Summary

Cache is a medium difficulty box. It hosts a vulnerable version of openEMR. Through sqli we dump credentials to get authenticated remote code execution in the box. For the root part, memcache contains the plaintext password of the user luffy. The user happens to be a member of docker group, we elevate privileges by launching an interactive shell as root into a newly created container in which the host file system is mounted.
