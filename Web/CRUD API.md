## CRUD

As we can see, we can easily specify the table and the row we want to perform an operation on through such APIs. Then we may utilize different HTTP methods to perform different operations on that row. In general, APIs perform 4 main operations on the requested database entity:

|Operation|HTTP Method|Description|
|---|---|---|
|`Create`|`POST`|Adds the specified data to the database table|
|`Read`|`GET`|Reads the specified entity from the database table|
|`Update`|`PUT`|Updates the data of the specified database table|
|`Delete`|`DELETE`|Removes the specified row from the database table|

These four operations are mainly linked to the commonly known CRUD APIs, but the same principle is also used in REST APIs and several other types of APIs. Of course, not all APIs work in the same way, and the user access control will limit what actions we can perform and what results we can see. The [Introduction to Web Applications](https://enterprise.hackthebox.com/module/details/75) module further explains these concepts, so you may refer to it for more details about APIs and their usage.

![[Pasted image 20240528101424.png]]