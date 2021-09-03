# Quick Summary

Frolic is an easy linux box. It is hosting a vulnerable version of playSMS on a nonstandard port. Using an authenticated remote code execution exploit, we get a shell into the box.
For the privilege escalation part, root left a setuid binary in one of the home directories. Binary is vulnerable to buffer overflow attack. With a simple return-to-libc payload we gain root privileges in the box.
