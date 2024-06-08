My first medium machine, should be fun!

![[Pasted image 20240530205019.png]]

Okay, SMB and HTTP. We should enumerate the website first.

![[Pasted image 20240530205112.png]]

more printers.

We get a list of users, as well as a page where we can input a malicious LDAP server, similar to the 'Return' box

![[Pasted image 20240530205222.png]]
![[Pasted image 20240530205245.png]]

```
htb\cube0x0
htb\egre55
htb\bertolis
htb\diogt
htb\felamos
htb\makelaris
htb\MinatoTW
htb\TRX
htb\MrR3boot
```

![[Pasted image 20240530210606.png]]

and we manage to grab

***htb\svc-printer:GrHT!32yt234***

attempting to use Evil-WinRM to reach the target results in some weirdness

![[Pasted image 20240530211256.png]]

it seems to be running cmd instead of powershell for some reason, so lets see other ways of logging in with winrm

![[Pasted image 20240530214734.png]]

this is not working

ah, that's probably why

![[Pasted image 20240530221858.png]]

Might have to bite the bullet on this one and boot my windows vm

Nah, lets install wsman libs instead lol
![[Pasted image 20240530222524.png]]

Ah, a shell, finally

![[Pasted image 20240530222640.png]]

So we can see that we're in a pretty locked down session, but wtf is pester?
![[Pasted image 20240530222748.png]]

Turns out pester could be our ticket out of this restricted session, as it's a way to run powershell test scripts

![[Pasted image 20240530223155.png]]
and it's in LOLBAS, lovely!


![[Pasted image 20240530223416.png]]

trying to launch powershell we see that we're running from the documents folder and can traverse basically wherever we want to

![[Pasted image 20240530223831.png]]

that didn't work unfortunately, maybe we can find a way to upload a PS1 somewhere?

![[Pasted image 20240530224248.png]]
smb isn't going to work

lets look for lolbins using ps1

we can actually trick it into making a ps1 file 

![[Pasted image 20240530233413.png]]

but how to write to it? no idea.


![[Pasted image 20240531105519.png]]

![[Pasted image 20240531105529.png]]OKAY

You can make stuff from the command line pull from an arbitrary SMB share, because windows lmao

![[Pasted image 20240531113348.png]]

make a meterpreter then copy it over


![[Pasted image 20240603141953.png]]
Now we should try pivoting
![[Pasted image 20240531114707.png]]


We need to set up routing to the remote subnet, we can do that with metasploit

![[Pasted image 20240531115723.png]]
![[Pasted image 20240531115821.png]]
![[Pasted image 20240531140455.png]]
it's a DC

it was unattend.xml :( 
im gonna kms

![[Pasted image 20240603162819.png]]

![[Pasted image 20240603163334.png]]![[Pasted image 20240603163447.png]]