Hosting webpage with users
![[Pasted image 20240529105453.png]]

A little trial and error reveals a username format of 

(first initial) + (last name)

Also, ldapglobalcat is open and allows anonymous bindings, through that we find the account "Hugo Smith"

![[Pasted image 20240529105640.png]]

Using this in an Asreproasting attack to attempt to grab hashes 
![[Pasted image 20240529105742.png]]

Nets us a hash, nice! Is it crackable?

![[Pasted image 20240529105819.png]]

it's HTB, of course you can crack it lol

```
fsmith:Thestrokes23
```
fsmith has good taste in bands.

it's about time to spin up bloodhound.

running this command we can collect data for bloodhound to ingest
![[Pasted image 20240529112838.png]]

we realize we can psremote into the DC
![[Pasted image 20240529112905.png]]


![[Pasted image 20240529112824.png]]

![[Pasted image 20240529113033.png]]

we ❤ winpeas

![[Pasted image 20240529113206.png]]
Moneymakestheworldgoround!
we've found autologon creds, sick

![[Pasted image 20240529113400.png]]

and it looks like he has DCSync perms!

Lets dump the db rq
	edit: this took forever, make sure you type the username correctly


![[Pasted image 20240529130714.png]]
okay lets try passing the hash with winrm to rdp as admin

![[Pasted image 20240529130653.png]]
It worked, rooted the box