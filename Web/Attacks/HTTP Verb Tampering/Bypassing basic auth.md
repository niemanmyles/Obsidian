You may attempt to bypass authentication schemes with HTTP Verb Tampering. If the authorization method doesn't properly cover all scenarios then it could lead to a bypass.


As the page uses a `GET` request, we can send a `POST` request and see whether the web page allows `POST` requests (i.e., whether the Authentication covers `POST` requests). To do so, we can right-click on the intercepted request in Burp and select `Change Request Method`, and it will automatically change the request into a `POST` request:![change_request](https://academy.hackthebox.com/storage/modules/134/web_attacks_verb_tampering_change_request.jpg)

So, it seems like the web server configurations do cover both `GET` and `POST` requests. However, as we have previously learned, we can utilize many other HTTP methods, most notably the `HEAD` method, which is identical to a `GET` request but does not return the body in the HTTP response. If this is successful, we may not receive any output, but the `reset` function should still get executed, which is our main target.

To see whether the server accepts `HEAD` requests, we can send an `OPTIONS` request to it and see what HTTP methods are accepted, as follows:

mylesnieman@htb[/htb]`$ curl -i -X OPTIONS http://SERVER_IP:PORT/  HTTP/1.1 200 OK Date:  Server: Apache/2.4.41 (Ubuntu) Allow: POST,OPTIONS,HEAD,GET Content-Length: 0 Content-Type: httpd/unix-directory`

As we can see, the response shows `Allow: POST,OPTIONS,HEAD,GET`, which means that the web server indeed accepts `HEAD` requests, which is the default configuration for many web servers. So, let's try to intercept the `reset` request again, and this time use a `HEAD` request to see how the web server handles it:

![HEAD_request](https://academy.hackthebox.com/storage/modules/134/web_attacks_verb_tampering_HEAD_request.jpg)

Once we change `POST` to `HEAD` and forward the request, we will see that we no longer get a login prompt or a `401 Unauthorized` page and get an empty output instead, as expected with a `HEAD` request. If we go back to the `File Manager` web application, we will see that all files have indeed been deleted, meaning that we successfully triggered the `Reset` functionality without having admin access or any credentials:

![](https://academy.hackthebox.com/storage/modules/134/web_attacks_verb_tampering_after_reset.jpg)


![[Pasted image 20240529134831.png]]

By changing the verb in burp to "PUT", we are able to bypass the auth, wipe the files, and get the flag.