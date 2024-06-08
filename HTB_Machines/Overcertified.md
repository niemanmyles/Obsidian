![[Pasted image 20240607104657.png]]


SMB Enum: 
![[Pasted image 20240606143950.png]]

![[Pasted image 20240606144441.png]]

![[Pasted image 20240606145723.png]]

![[Pasted image 20240606145329.png]]
![[Pasted image 20240606145437.png]]
let's dump it in a pretty format.

![[Pasted image 20240607105206.png]]

![[Pasted image 20240607105524.png]]

Testing for user SPNs (because we saw the mssql account in the ldap dump), we get one, but get an error.
https://medium.com/@danieldantebarnes/fixing-the-kerberos-sessionerror-krb-ap-err-skew-clock-skew-too-great-issue-while-kerberoasting-b60b0fe20069

![[Pasted image 20240607110009.png]]
![[Pasted image 20240607113604.png]]
so the domain is certified.htb, rerunning with the right domain (lol)

![[Pasted image 20240607113744.png]]

we get the hash, cool. Can we crack it?
![[Pasted image 20240607114003.png]]

We sure can. This gives us the information MSSQLSERVER:lucky7

we try connecting to the mssql server

![[Pasted image 20240607114503.png]]
running an enumeration module reveals something interesting: the account running the SQL server is CERTIFIEDDC\thomas, and we can steal his hash!

Make sure you run this on the tunnel, and not your local address...
![[Pasted image 20240607134153.png]]
![[Pasted image 20240607134211.png]]
Attempting to crack it resulted in 
![[Pasted image 20240607134517.png]]
...
the password 159357

![[Pasted image 20240607134554.png]]
and we have a user flag!

Bloodhound scan didn't return much, but the machine's name indicates ADCS is an escalation path

![[Pasted image 20240607140657.png]]
![[Pasted image 20240607140709.png]]
sweet...what does that mean

It means we can impersonate the admin

![[Pasted image 20240607142928.png]]


so we've generated a cert, now we need to make it usable, copy paste to kali and run this 

![[Pasted image 20240607143015.png]]
put in no password both times
then use rubeus to request ticket

![[Pasted image 20240607143142.png]]


![[Pasted image 20240607143156.png]]

OKAY so certipy actually makes hthis really nice

![[Pasted image 20240607154027.png]]
