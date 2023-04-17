# HTTP

## Common Request Headers

* **Host:** Tell it which web site you require, otherwise you'll just receive the default website for the server.
* **User-Agent:** Tell your browser software and version number.
* **Content-Length:** Tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data.
* **Accept-Encoding**: Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.
* **Cookie:** Data sent to the server to help remember your information.

## &#x20;Common Response Headers

* **Set-Cookie:** Information to store which gets sent back to the web server on each request.
* **Cache-Control**: How long to store the content of the response in the browser's cache before it requests it again.
* **Content-Type:** This tells the client what type of data is being returned to know how to process the data.
* **Content-Encoding:** What method has been used to compress the data to make it smaller when sending it over the internet.

## Methods

* **GET Request:** Used for getting information from a web server.
* **POST Request:** Used for submitting data to the web server and potentially creating new records.
* **PUT Request:** Used for submitting data to a web server to update information.
* **DELETE Request:** Used for deleting information/records from a web server.
* **HEAD Request:** The only difference between HEAD and GET requests is that for HTTP HEAD, the server only returns headers without body.

## Request and reponses

## Status code

| 100-199 - Information Response | These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common. |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200-299 - Success              | This range of status codes is used to tell the client their request was successful.                                                                                                    |
| 300-399 - Redirection          | These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether.                                      |
| 400-499 - Client Errors        | Used to inform the client that there was an error with their request.                                                                                                                  |
| 500-599 - Server Errors        | This is reserved for errors happening on the server-side and usually indicate quite a major problem with the server handling the request.                                              |

### Common Status Codes

| 200 - OK                     | The request was completed successfully.                                                                                                                                                                                       |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 201 - Created                | A resource has been created (for example a new user or new blog post).                                                                                                                                                        |
| 301 - Permanent Redirect     | This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.                                                                                |
| 302 - Temporary Redirect     | Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again in the near future.                                                                                |
| 400 - Bad Request            | This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expected a certain parameter that the client didn't send. |
| 401 - Not Authorised         | You are not currently allowed to view this resource until you have authorised with the web application, most commonly with a username and password.                                                                           |
| 403 - Forbidden              | You do not have permission to view this resource whether you are logged in or not.                                                                                                                                            |
| 405 - Method Not Allowed     | The resource does not allow this method request, for example, you send a GET request to the resource /create-account when it was expecting a POST request instead.                                                            |
| 404 - Page Not Found         | The page/resource you requested does not exist.                                                                                                                                                                               |
| 500 - Internal Service Error | The server has encountered some kind of error with your request that it doesn't know how to handle properly.                                                                                                                  |
| 503 - Service Unavailable    | This server cannot handle your request as it's either overloaded or down for maintenance.                                                                                                                                     |
