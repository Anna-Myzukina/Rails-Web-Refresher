# Rails-Web-Refresher
The Odin Project

[Test any URI, by sending custom HTTP request and checking the HTTP response. TestURI.org is a free web-sniffer.net alternative.](http://testuri.org/sniffer)


#### These request verbs are:

* GET: fetch an existing resource. The URL contains all the necessary information the server 
needs to locate and return the resource.

* POST: create a new resource. POST requests usually carry a payload that specifies the data for the new resource.

* PUT: update an existing resource. The payload may contain the updated data for the resource.

* DELETE: delete an existing resource.
The above four verbs are the most popular, and most tools and frameworks explicitly expose these request verbs. PUT and 
* DELETE are sometimes considered specialized versions of the POST verb, and they may be packaged as POST requests with the payload containing the exact action: create, update or delete.

### There are some lesser used verbs that HTTP also supports:

* HEAD: this is similar to GET, but without the message body. It's used to retrieve the server headers for a particular resource, generally to check if the resource has changed, via timestamps.

* TRACE: used to retrieve the hops that a request takes to round trip from the server. Each intermediate proxy or gateway would inject its IP or DNS name into the Via header field. This can be used for diagnostic purposes.

* OPTIONS: used to retrieve the server capabilities. On the client-side, it can be used to modify the request based on what the server can support.
Status Codes
With URLs and verbs, the client can initiate requests to the server. In return, the server responds with status codes and message payloads. The status code is important and tells the client how to interpret the server response. The HTTP spec defines certain number ranges for specific types of responses:

#### 1xx: Informational Messages
-   All HTTP/1.1 clients are required to accept the Transfer-Encoding header.

        This class of codes was introduced in HTTP/1.1 and is purely provisional. The server can send a Expect: 100-continue message, telling the client to continue sending the remainder of the request, or ignore if it has already sent it. HTTP/1.0 clients are supposed to ignore this header.

#### 2xx: Successful
    This tells the client that the request was successfully processed. The most common code is 200 OK. For a GET request, the server sends the resource in the message body. There are other less frequently used codes:

* 202 Accepted: the request was accepted but may not include the resource in the response. This is useful for async processing on the server side. The server may choose to send information for monitoring.
* 204 No Content: there is no message body in the response.
* 205 Reset Content: indicates to the client to reset its document view.
* 206 Partial Content: indicates that the response only contains partial content. Additional headers indicate the exact range and content expiration information.

#### 3xx: Redirection
* 404 indicates that the resource is invalid and does not exist on the server.

      This requires the client to take additional action. The most common use-case is to jump to a different URL in order to fetch the resource.

* 301 Moved Permanently: the resource is now located at a new URL.
* 303 See Other: the resource is temporarily located at a new URL. The Location response header contains the temporary URL.
* 304 Not Modified: the server has determined that the resource has not changed and the client should use its cached copy. This relies on the fact that the client is sending ETag (Enttity Tag) information that is a hash of the content. The server compares this with its own computed ETag to check for modifications.

#### 4xx: Client Error
These codes are used when the server thinks that the client is at fault, either by requesting an invalid resource or making a bad request. The most popular code in this class is 404 Not Found, which I think everyone will identify with. 404 indicates that the resource is invalid and does not exist on the server. The other codes in this class include:

* 400 Bad Request: the request was malformed.
* 401 Unauthorized: request requires authentication. The client can repeat the request with the Authorization header. If the client already included the Authorization header, then the credentials were wrong.
* 403 Forbidden: server has denied access to the resource.
* 405 Method Not Allowed: invalid HTTP verb used in the request line, or the server does not support that verb.
* 409 Conflict: the server could not complete the request because the client is trying to modify a resource that is newer than the client's timestamp. Conflicts arise mostly for PUT requests during collaborative edits on a resource.

#### 5xx: Server Error
This class of codes are used to indicate a server failure while processing the request. The most commonly used error code is * 500 Internal Server Error. The others in this class are:

* 501 Not Implemented: the server does not yet support the requested functionality.
* 503 Service Unavailable: this could happen if an internal system on the server has failed or the server is overloaded. Typically, the server won't even respond and the request will timeout.
