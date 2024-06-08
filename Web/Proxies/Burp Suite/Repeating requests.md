## Repeating Requests

#### Burp

Request repeating allows us to resend any web request that has previously gone through the web proxy. This allows us to make quick changes to any request before we send it, then get the response within our tools without intercepting and modifying each request.

Once we locate the request we want to repeat, we can click [`CTRL+R`] in Burp to send it to the `Repeater` tab, and then we can either navigate to the `Repeater` tab or click [`CTRL+SHIFT+R`] to go to it directly. Once in `Repeater`, we can click on `Send` to send the request:

![Burp repeat request](https://academy.hackthebox.com/storage/modules/110/burp_repeater_request.jpg)