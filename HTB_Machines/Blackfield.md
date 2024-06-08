![[Pasted image 20240604092337.png]]

initial portscan revealed ldap, rpc, and kerberos and dns
![[Pasted image 20240604092057.png]]
LDAP Anonymous bind not allowed, nice!

Running enum4linux gets us the hostname ``Blackfield`` as well as letting us know that SMB allows '':'' sessions 
![[Pasted image 20240604092424.png]]

![[Pasted image 20240604092437.png]]

So we try connecting with no password and can see some interesting non-default shares such as ``forensic`` and ``profiles$``
![[Pasted image 20240604092720.png]]
Lets see what we can read/write to
![[Pasted image 20240604093505.png]]
okay, let's try  profiles


![[Pasted image 20240604094327.png]]
Okay, so we can take that and use this nice bash oneliner to make a text file with all the usernames
![[Pasted image 20240604094317.png]]
What do we do with a big list of usernames? We test for kerberos pre-auth!

![[Pasted image 20240604094710.png]]
![[Pasted image 20240604094710.png]]![[Pasted image 20240604094742.png]]
okay sweet, now we know that
audit2020 and 
![[Pasted image 20240604094820.png]]
exist
![[Pasted image 20240604094919.png]]




support:#00^BlackKnight




![[Pasted image 20240604095452.png]]
run a bloodhound scan with the creds, found not a lot interesting. Let's see if we can explore that forensics share.
![[Pasted image 20240604095702.png]]

Still no access. I'd imagine that the audit2020 account is probably the only way into that. How can I get there?

![[Pasted image 20240604095820.png]]
oh bloodhound my beloved


We can exploit like this:

net rpc password "audit2020" "newP@ssword2022" -U "BLACKFIELD"/"support"%"#00^BlackKnight" -S "10.129.230.214"

checking with smbclient, it seems to have worked.
![[Pasted image 20240604101150.png]]

oh boy did it work

![[Pasted image 20240604101316.png]]

bro was not subtle

![[Pasted image 20240604101651.png]]

is that...an lsass dump
![[Pasted image 20240604101721.png]]


![[Pasted image 20240604101812.png]]
oh god it is

![[Pasted image 20240604102046.png]]
from this we pwn svc_backup
9658d1d1dcd9250115e2205d9f48400d
![[Pasted image 20240604102749.png]]
and can now winrm!

![[Pasted image 20240604102921.png]]
![[Pasted image 20240604102939.png]]

Interesting: SeBackupPrivilege, Backup Operators

okay, how can we use these?

![[Pasted image 20240604131615.png]]
this really sucked, so here's the commands you need to pass to diskshadow

```
set verbose on
set metadata C:\Windows\Temp\meta.cab
set context clientaccessible
set context persistent
begin backup
add volume C: alias cdrive
create
expose %cdrive% E:
end backup
exit
```

![[Pasted image 20240604132048.png]]
Clone the ntds
![[Pasted image 20240604132105.png]]
download the db, dump hashes

![[Pasted image 20240604132703.png]]

![[Pasted image 20240604132841.png]]