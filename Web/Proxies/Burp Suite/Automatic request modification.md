# Automatic Modification

We may want to apply certain modifications to all outgoing HTTP requests or all incoming HTTP responses in certain situations. In these cases, we can utilize automatic modifications based on rules we set, so the web proxy tools will automatically apply them.

#### Burp Match and Replace

We can go to (`Proxy>Options>Match and Replace`) and click on `Add` in Burp. As the below screenshot shows, we will set the following options:

![Burp Match Replace](https://academy.hackthebox.com/storage/modules/110/burp_match_replace_user_agent_1.jpg)

|||
|---|---|
|`Type`: `Request header`|Since the change we want to make will be in the request header and not in its body.|
|`Match`: `^User-Agent.*$`|The regex pattern that matches the entire line with `User-Agent` in it.|
|`Replace`: `User-Agent: HackTheBox Agent 1.0`|This is the value that will replace the line we matched above.|
|`Regex match`: True|We don't know the exact User-Agent string we want to replace, so we'll use regex to match any value that matches the pattern we specified above.|