[obsidian://open?vault=SRA&file=Web%2FRequests] 

## Intercepting Requests

#### Burp

In Burp, we can navigate to the `Proxy` tab, and request interception should be on by default. If we want to turn request interception on or off, we may go to the `Intercept` sub-tab and click on `Intercept is on/off` button to do so:

![Burp Intercept On](https://academy.hackthebox.com/storage/modules/110/burp_intercept_htb_on.jpg)

Once we turn request interception on, we can start up the pre-configured browser and then visit our target website after spawning it from the exercise at the end of this section. Then, once we go back to Burp, we will see the intercepted request awaiting our action, and we can click on `forward` to forward the request:

![Burp Intercept Page](https://academy.hackthebox.com/storage/modules/110/burp_intercept_page.jpg)


## Manipulating Intercepted Requests

Once we intercept the request, it will remain hanging until we forward it, as we did above. We can examine the request, manipulate it to make any changes we want, and then send it to its destination. This helps us better understand what information a particular web application is sending in its web requests and how it may respond to any changes we make in that request.

There are numerous applications for this in Web Penetration Testing, such as testing for:

1. SQL injections
2. Command injections
3. Upload bypass
4. Authentication bypass
5. XSS
6. XXE
7. Error handling
8. Deserialization


![[Pasted image 20240528105041.png]]
