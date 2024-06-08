Exploiting IDOR vulnerabilities is easy in some cases and hard in others.
## Insecure Parameters

Let's start with a basic example that showcases a typical IDOR vulnerability. The exercise below is an `Employee Manager` web application that hosts employee records:

![](https://academy.hackthebox.com/storage/modules/134/web_attacks_idor_employee_manager.jpg)

Our web application assumes that we are logged in as an employee with user id `uid=1` to simplify things. This would require us to log in with credentials in a real web application, but the rest of the attack would be the same. Once we click on `Documents`, we are redirected to

`/documents.php`:

![](https://academy.hackthebox.com/storage/modules/134/web_attacks_idor_documents.jpg)

When we get to the `Documents` page, we see several documents that belong to our user. These can be files uploaded by our user or files set for us by another department (e.g., HR Department). Checking the file links, we see that they have individual names:

Code: html

```html
/documents/Invoice_1_09_2021.pdf
/documents/Report_1_10_2021.pdf
```

We see that the files have a predictable naming pattern, as the file names appear to be using the user `uid` and the month/year as part of the file name, which may allow us to fuzz files for other users. This is the most basic type of IDOR vulnerability and is called `static file IDOR`. However, to successfully fuzz other files, we would assume that they all start with `Invoice` or `Report`, which may reveal some files but not all. So, let's look for a more solid IDOR vulnerability.

## Mass Enumeration

We can try manually accessing other employee documents with `uid=3`, `uid=4`, and so on. However, manually accessing files is not efficient in a real work environment with hundreds or thousands of employees. So, we can either use a tool like `Burp Intruder` or `ZAP Fuzzer` to retrieve all files or write a small bash script to download all files, which is what we will do.

Now, we can use a simple `for` loop to loop over the `uid` parameter and return the document of all employees, and then use `wget` to download each document link:

Code: bash

```bash
#!/bin/bash

url="http://SERVER_IP:PORT"

for i in {1..10}; do
        for link in $(curl -s "$url/documents.php?uid=$i" | grep -oP "\/documents.*?.pdf"); do
                wget -q $url/$link
        done
done
```

When we run the script, it will download all documents from all employees with `uids` between 1-10, thus successfully exploiting the IDOR vulnerability to mass enumerate the documents of all employees. This script is one example of how we can achieve the same objective. Try using a tool like Burp Intruder or ZAP Fuzzer, or write another Bash or PowerShell script to download all documents.