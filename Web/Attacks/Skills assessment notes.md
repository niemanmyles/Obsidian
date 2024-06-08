![[Pasted image 20240530103441.png]]

here's the webpage

![[Pasted image 20240530103531.png]]

![[Pasted image 20240530103658.png]]![[Pasted image 20240530103751.png]]

![[Pasted image 20240530103907.png]]
![[Pasted image 20240530110434.png]]

Api endpoint? lets download the first 100 lol

![[Pasted image 20240530110805.png]]

okay, now we know the schema for the users api is

```json
{
"uid":"15",
"username":"b.moriarty",
"full_name":"Brandi Moriarty",
"company":"Veum - Bechtelar"
}
```

![[Pasted image 20240530110949.png]]
This could be the admin user, let's see what we can do (lets try resetting their password)

![[Pasted image 20240530111728.png]]
attempting to give them an arbitrary password such as P@ssw0rd gives us a token

{"token":"e51a85fa-17ac-11ec-8e51-e78234eb7b0c"}

which we can use on the /reset.php endpoint

![[Pasted image 20240530113819.png]]
Damn, no post

![[Pasted image 20240530113827.png]]
![[Pasted image 20240530113844.png]]



![[Pasted image 20240530114001.png]]
they call me the web hacker lmaoo

![[Pasted image 20240530114212.png]]
yo new endpoint just dropped

we can grab the config with [XXE] ![[Pasted image 20240530134959.png]]

LETS GOOO
![[Pasted image 20240530140346.png]]