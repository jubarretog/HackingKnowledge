---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# HTTP

Fundamental protocol used for communication on the web. It defines how messages are formatted and transmitted between a client and a server. It is based on a request-response model.

## <mark style="color:blue;">Request-Response</mark>

Is the core communication pattern used in the HTTP protocol, where a client (such as a web browser) sends a request to a server, and the server processes that request and sends back a response such as a web page or a resource.

### <mark style="color:purple;">**Client Request**</mark>

The client initiates communication by sending an HTTP request to the server. This request contains various details, including:

* **Method**: Specifies the type of action, such as retrieving, sending, or deleting data, among others. Here we have some of the most common:
  * **GET Request:** Used for getting content from a web server.
  * **POST Request:** Used for submitting data to the web server and potentially creating records.
  * **PUT Request:** Used for submitting data to a web server to update information.
  * **DELETE Request:** Used for deleting information/records from a web server.
  * **HEAD Request:** The only difference between HEAD and GET requests is that for HTTP HEAD, the server only returns headers without a body.
* **URL**: Uniform Resource Locator, provides the location of the resource and the protocol to be used to retrieve it. Have the structure: `scheme://user:password@host:port/path?query#fragment`. It can be broken down as follows:
  * **Scheme:** The protocol to use for accessing the resource.
  * **User-Password:** For services that require authentication to log in, a username and password can be put into the URL.
  * **Host:** The domain name or IP address of the server you wish to access.
  * **Port:** The Port that you are going to connect to.
  * **Path:** The file name or location of the resource you are trying to access.
  * **Query String:** Extra bits of information that can be sent to the requested path, receive values that are passed are parameters to the service.
  * **Fragment**: Reference to a location on the actual page requested. This is commonly used for pages with long content and can have a certain part of the page directly linked to it.
* **Headers**: Information about the client (e.g., browser type, accepted data formats, etc.). Here we have some of the most common:
  * **Host:** Tell it which website you require, otherwise you'll just receive the default website for the server.
  * **User-Agent:** Tell your browser software and version number.
  * **Content-Length:** Tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data.
  * **Accept-Encoding**: Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.
  * **Cookie:** Data sent to the server to help remember the information of the client.
* **Body**: Data sent with certain requests, usually when submitting form data. It is optional.

### <mark style="color:purple;">Server Response</mark>

The server processes the request and sends an **HTTP response** back to the client. This response includes:

*   **Status Code**: Indicates whether the request was successful or if there was an issue. These are categorized based on the type of information they provide as follows:\
    \


    <table><thead><tr><th width="374">Type</th><th>Description</th></tr></thead><tbody><tr><td>100-199 - Information Response</td><td>These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common.</td></tr><tr><td>200-299 - Success</td><td>This range of status codes is used to tell the client their request was successful.</td></tr><tr><td>300-399 - Redirection</td><td>These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether.</td></tr><tr><td>400-499 - Client Errors</td><td>Used to inform the client that there was an error with their request.</td></tr><tr><td>500-599 - Server Errors</td><td>This is reserved for errors happening on the server side and usually indicates quite a major problem with the server handling the request.</td></tr></tbody></table>

    Also here we can find some of the most common status codes:

| Code                         | Description                                                                                                                                                                                                                  |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200 - OK                     | The request was completed successfully.                                                                                                                                                                                      |
| 201 - Created                | A resource has been created (for example a new user or new blog post).                                                                                                                                                       |
| 301 - Permanent Redirect     | This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.                                                                               |
| 302 - Temporary Redirect     | Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again soon.                                                                                             |
| 400 - Bad Request            | This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expects a certain parameter that the client didn't send. |
| 401 - Not Authorized         | You are not currently allowed to view this resource until you have been authorized by the web application, most commonly with a username and password.                                                                       |
| 403 - Forbidden              | You do not have permission to view this resource whether you are logged in or not.                                                                                                                                           |
| 405 - Method Not Allowed     | The resource does not allow this method request, for example, you send a GET request to the resource /create-account when it was expecting a POST request instead.                                                           |
| 404 - Page Not Found         | The page/resource you requested does not exist.                                                                                                                                                                              |
| 500 - Internal Service Error | The server has encountered some kind of error with your request that it doesn't know how to handle properly.                                                                                                                 |
| 503 - Service Unavailable    | This server cannot handle your request as it's either overloaded or down for maintenance.                                                                                                                                    |

* **Headers**: Additional information about the server or the response. Here we have some of the most common:
  * **Set-Cookie:** Information to store which gets sent back to the web server on each request.
  * **Cache-Control**: How long to store the content of the response in the browser's cache before it requests it again.
  * **Content-Type:** This tells the client what type of data is being returned to know how to process the data.
  * **Content-Encoding:** The method that has been used to compress the data to make it smaller when sending it over the internet.
* **Body**: The actual content requested by the client, such as an HTML page, JSON data, or an image, among others.
