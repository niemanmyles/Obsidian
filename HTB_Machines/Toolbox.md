![[Pasted image 20240607154618.png]]

![[Pasted image 20240607154645.png]]
ftp has anonymous login
![[Pasted image 20240607154826.png]]
downloading that binary for potential analysis
![[Pasted image 20240607154900.png]]
it also has a website, with ~~users~~ names!

Christine Rooster
Brandon Sharp
Connor Hodson
Christine Aguilar
Robert Spears
Bruce Rogers
John Smith

```
crooster
bsharp
chodson
caguilar
rspears
brogers
jsmith
```

![[Pasted image 20240607155350.png]]

okay this page makes post requests

![[Pasted image 20240607160756.png]]
there's a vhost!
![[Pasted image 20240607162914.png]]
![[Pasted image 20240607163842.png]]
it's vulnerable to postgresql injection

![[Pasted image 20240607164830.png]]

this bypasses auth
