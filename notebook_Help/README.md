# Summary


Help is an easy rated linux box. It has 3 ports open, on port 80 we discover that HelpDeskZ is running which is a php based open source ticket service. The box is running an outdated version of the software. We can get the initial shell by running a public exploit as there is a CVE assigned for this version. For the privilege escalation part, there are two ways to get root on the box. One is through a kernel exploit and the other is through realizing a simple mistake from the user's `.bash_history`. The password of the root user is logged in bash_history but it is capitalized wrong.


