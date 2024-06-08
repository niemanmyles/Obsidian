![[Pasted image 20240529153441.png]]
initial scan


What's on the website?

![[Pasted image 20240529153533.png]]

oh good, printers
![[Pasted image 20240529153614.png]]
These are the settings found on the "settings.php" endpoint, which reveal

Domain: return.local
Hostname: printer.return.local
Username: svc-printer
Password: 1edFg43012!!

![[Pasted image 20240529155048.png]]
thankfully, ldap is plaintext. that looks like a password. testing the creds, it is.

We can log into this computer with evil-winrm

![[Pasted image 20240530145406.png]]
![[Pasted image 20240530145617.png]]

Okay this is a bit tricky if you don't know what you're doing, it took some googling. 
https://www.hackingarticles.in/windows-privilege-escalation-server-operator-group/

as seen here, you can modify service paths, so we should also try this (lol)

![[Pasted image 20240530150854.png]]

lets pick "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe" because it doesn't look important

![[Pasted image 20240530151229.png]]
uploading nc to replace the binary with

![[Pasted image 20240530151357.png]]
this is actually sick
![[Pasted image 20240530151539.png]]
