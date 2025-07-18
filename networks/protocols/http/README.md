# HTTP

The **HyperText Transfer Protocol** is used for communication on the web, defining how messages are formatted and transmitted between a client and a server. It is based on a request-response model being also a stateless protocol. Operates in the Application layer, typically on port 80. It was originally designed to transfer HTML, but it has evolved to transfer multiple types of documents

## <mark style="color:blue;">Request-Response Model</mark>

It is the core communication pattern used in the HTTP protocol. It transmits data in text blocks where a client, such as a web browser, sends a request to a server, and the server processes that request and sends back a response, such as a web page or a resource. In HTTP, this is implemented as follows:

### <mark style="color:purple;">**Client Request**</mark>

The client initiates communication by sending an HTTP request to the server. This request contains various details, including:

* **Method**: Specifies the type of action, such as retrieving, sending, or deleting data, among others. The most common HTTP methods are:
  * **GET:** Used for getting content from a web server
  * **POST:** Used for submitting data to the web server and potentially creating records
  * **PUT:** Used for submitting data to a web server to update information
  * **DELETE:** Used for deleting information/records from a web server
  * **HEAD:** The only difference between HEAD and GET requests is that for HTTP HEAD, the server only returns headers without a body
  * **OPTIONS:** Returns the HTTP methods that the server supports
  * **CONNECT:** Converts the request connection to a transparent TCP/IP tunnel
  * **TRACE:** Does a message loopback test along the path to the target resource
* **URL**: Uniform Resource Locator, provides a resource's location and the protocol to retrieve it. Have the structure: _scheme://user:password@host:port/path?query#fragment_.\
  This can be broken down as follows:
  * **Scheme:** The protocol to use for accessing the resource
  * **User-Password:** For services that require authentication to log in, a username and password can be put into the URL
  * **Host:** The domain name or IP address of the server you wish to access
  * **Port:** The Port that you are going to connect to
  * **Path:** The file name or location of the resource you are trying to access
  * **Query String:** Extra bits of information that can be sent to the requested path, receive values that are passed are parameters to the service
  * **Fragment**: Reference to a location on the actual page requested. This is commonly used for pages with long content, and can have a certain part of the page directly linked to it
* **Headers**: Contain information about the client, such as browser type, and accepted data formats, among others. Here are some of the most common:
  * **Host:** Tell it which website you require, otherwise you'll receive the default website for the server
  * **User-Agent:** Tell your browser software and version number
  * **Content-Length:** Tells the web server how much data to expect in the web request. This way, the server can ensure it isn't missing any data
  * **Accept-Encoding**: Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet
  * **Cookie:** Data fragments sent to the server to maintain the information of the client between requests. They are set in the form _name=value_, separated by semicolons
* **Body**: Optional data sent with certain requests, usually when submitting a form

Here we find an example of an HTTP request:

{% code overflow="wrap" lineNumbers="true" %}
```ruby
GET /search/?q=hello HTTP/1.1    # The verb, resource, and protocol version
Host: google.com                 # The host, a domain or IP
Accept: text/html                # Example header
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 2026
X-Request-Id: 1cb33dc1-7a2e-4800-be5b-3b71c591984c
X-Nginx-Pool: read.users-api.melifrontends.com
X-Nginx-Host: i-0ffba3dbbeccc5b13-10.54.28.106
```
{% endcode %}

### <mark style="color:purple;">Server Response</mark>

The server processes the request and sends an **HTTP response** back to the client. This response includes:

*   **Status Code**: Indicates whether the request was successful or if there was an issue. These are categorized based on the type of information they provide as follows:\
    \


    <table><thead><tr><th width="374">Type</th><th>Description</th></tr></thead><tbody><tr><td>100-199 - Information Response</td><td>These are sent to tell the client the first part of their request has been accepted, and they should continue sending the rest of their request. These codes are no longer very common</td></tr><tr><td>200-299 - Success</td><td>This range of status codes is used to tell the client their request was successful</td></tr><tr><td>300-399 - Redirection</td><td>These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether</td></tr><tr><td>400-499 - Client Errors</td><td>Used to inform the client that there was an error with their request</td></tr><tr><td>500-599 - Server Errors</td><td>This is reserved for errors happening on the server side and usually indicates quite a major problem with the server handling the request</td></tr></tbody></table>

Also, some of the most common status codes are:

| Code                         | Description                                                                                                                                                                                                                 |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200 - OK                     | The request was completed successfully                                                                                                                                                                                      |
| 201 - Created                | A resource has been created, for example, a new user or post                                                                                                                                                                |
| 301 - Permanent Redirect     | This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead                                                                               |
| 302 - Temporary Redirect     | Similar to the above permanent redirect, but as the name suggests, this is only a temporary change, and it may change again soon                                                                                            |
| 400 - Bad Request            | This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expects a certain parameter that the client didn't send |
| 401 - Not Authorized         | You are not currently allowed to view this resource until you have been authorized by the web application, most commonly with a username and password                                                                       |
| 403 - Forbidden              | You do not have permission to view this resource, whether you are logged in or not                                                                                                                                          |
| 405 - Method Not Allowed     | The resource does not allow this method request, for example, you send a GET request to the resource /create-account when it was expecting a POST request instead                                                           |
| 404 - Page Not Found         | The page/resource requested doesn't exist                                                                                                                                                                                   |
| 500 - Internal Service Error | The server has encountered some kind of error with your request that it doesn't know how to handle properly                                                                                                                 |
| 503 - Service Unavailable    | The server cannot handle your request as it's either overloaded or down for maintenance                                                                                                                                     |

* **Headers**: Additional information about the server or the response. Some of the most common are:
  * **Set-Cookie:** Information to store, which gets sent back to the web server on each request
  * **Cache-Control**: How long to store the content of the response in the browser's cache before it requests it again
  * **Content-Type:** This tells the client what type of data is being returned, so it can know how to process the data
  * **Content-Encoding:** The method that has been used to compress the data to make it smaller when sending it over the internet
* **Body**: The actual content requested by the client, such as an HTML page, JSON data, or an image, among others

Here we find an example of an HTTP response:

{% code overflow="wrap" lineNumbers="true" %}
```ruby
HTTP/1.1 200 OK            # Protocol version and status code
Content-Type: application/json; charset=utf-8 # Headers
Content-Length: 2026

{                    #Body
  "id":1,
  "nickname":"juan"
}
```
{% endcode %}

## <mark style="color:blue;">**HTTP Cookie Security Flags**</mark>

Security flags are a relevant configuration for HTTP cookies. They control the behavior, accessibility, and security of cookies sent between the client and the server. They are set on the server, via the Set-Cookie HTTP response header, which includes instructions for the browser on how to handle cookies.

Here we explain some of the security flags that can be controlled:

* Secure: The cookie can only be sent over HTTPS connections (not HTTP). It is mandatory if the _SameSite=Strict_ flag is set\
  Example: _Set-Cookie: sessionid=123; Secure_
* **HttpOnly:** The cookie is not accessible by JavaScript (document.cookie), which helps prevent XSS attacks. Example: _Set-Cookie: sessionid=123; HttpOnly_
* **SameSite:** Restricts cookie cross-site requests, which helps prevent CSRF. It can be set as _Strict_, _Lax_, or _None._ Example: _Set-Cookie: sessionid=123; SameSite=Strict_
  * **Strict:** The cookie is only sent if the request comes from the same site; any request initiated by a link or request from an external domain will not include the cookie
  * **Lax:** The cookie is sent in some cross-site navigation situations (for example, when clicking on a link), but not in automatic requests such as image uploads or third-party AJAX requests
  * **None:** The cookie is sent in all circumstances, including cross-site requests. When using this, it is mandatory to mark the cookie as Secure
* **Domain:** Specifies which hosts/domains can receive the cookie.\
  Example: _Set-Cookie: sessionid=123; Domain=.site.com_
* **Path:** Specifies the URL path that must exist in the request to send the cookie.\
  Example: _Set-Cookie: sessionid=123; Path=/admin_
* **Expires/Max-Age:** Sets how long the cookie persists in the client.\
  Example: _Set-Cookie: sessionid=123; Max-Age=3600_
