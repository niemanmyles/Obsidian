Scan: 
![[Pasted image 20240528135206.png]]


Web was hosting ADSelfService, vulnerable to CVE-2021-40539 (found by googling)
You have to modify the exploit to point to the right web port, and to reach back out to you on the correct IP

Possible user accounts from ````
![[Pasted image 20240528135322.png]]

Oh my god it was just running as system, no privesc needed
