# HTTP Status Codes

<small><em>The following information is from [Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) as of June 4, 2019.</em></small>

<small><em>* REST service-specific information is from [here](https://www.restapitutorial.com/httpstatuscodes.html)</em></small>

<small>An implementation of `http_response_code` for PHP < 5.4.0 can be found [here](http_response_code/).</small>

## [1xx Informational Response](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#1xx_Informational_response)

An informational response indicates that the request was received and understood. It is issued on a provisional basis while request processing continues. It alerts the client to wait for a final response. The message consists only of the status line and optional header fields, and is terminated by an empty line. As the HTTP/1.0 standard did not define any 1xx status codes, servers must not send a 1xx response to an HTTP/1.0 compliant client except under experimental conditions.

#### 100 Continue

<em>The server has received the request headers and the client should proceed to send the request body (in the case of a request for which a body needs to be sent; for example, a POST request). Sending a large request body to a server after a request has been rejected for inappropriate headers would be inefficient. To have a server check the request's headers, a client must send Expect: 100-continue as a header in its initial request and receive a 100 Continue status code in response before sending the body. If the client receives an error code such as 403 (Forbidden) or 405 (Method Not Allowed) then it shouldn't send the request's body. The response `417 Expectation Failed` indicates that the request should be repeated without the Expect header as it indicates that the server doesn't support expectations (this is the case, for example, of HTTP/1.0 servers).</em>

#### 101 Switching Protocols

<em>The requester has asked the server to switch protocols and the server has agreed to do so.</em>

#### 102 Processing (WebDAV; RFC 2518)

<em>A WebDAV request may contain many sub-requests involving file operations, requiring a long time to complete the request. This code indicates that the server has received and is processing the request, but no response is available yet. This prevents the client from timing out and assuming the request was lost</em>

#### 103 Early Hints (RFC 8297)

<em>Used to return some response headers before final HTTP message.</em>

## [2xx Success](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#2xx_Success)

This class of status codes indicates the action requested by the client was received, understood, and accepted.

#### 200 OK*

<em>Standard response for successful HTTP requests. The actual response will depend on the request method used. In a GET request, the response will contain an entity corresponding to the requested resource. In a POST request, the response will contain an entity describing or containing the result of the action.</em>

<small>* General status code. Most common code used to indicate success.</small>

#### 201 Created*

<em>The request has been fulfilled, resulting in the creation of a new resource.</em>

<small>* Successful creation occurred (via either POST or PUT). Set the Location header to contain a link to the newly-created resource (on POST). Response body content may or may not be present.</small>

#### 202 Accepted

<em>The request has been accepted for processing, but the processing has not been completed. The request might or might not be eventually acted upon, and may be disallowed when processing occurs.</em>

#### 203 Non-Authoritative Information (since HTTP/1.1)
<em>The server is a transforming proxy (e.g. a Web accelerator) that received a `200 OK` from its origin, but is returning a modified version of the origin's response.</em>

#### 204 No Content*

<em>The server successfully processed the request and is not returning any content.</em>

<small>* Status when wrapped responses (e.g. JSEND) are not used and nothing is in the body (e.g. DELETE).</small>

#### 205 Reset Content

<em>The server successfully processed the request, but is not returning any content. Unlike a 204 response, this response requires that the requester reset the document view.</em>

#### 206 Partial Content (RFC 7233)

<em>The server is delivering only part of the resource (byte serving) due to a range header sent by the client. The range header is used by HTTP clients to enable resuming of interrupted downloads, or split a download into multiple simultaneous streams.</em>

#### 207 Multi-Status (WebDAV; RFC 4918)

<em>The message body that follows is by default an XML message and can contain a number of separate response codes, depending on how many sub-requests were made.</em>

#### 208 Already Reported (WebDAV; RFC 5842)

<em>The members of a DAV binding have already been enumerated in a preceding part of the (multistatus) response, and are not being included again.</em>

#### 226 IM Used (RFC 3229)

<em>The server has fulfilled a request for the resource, and the response is a representation of the result of one or more instance-manipulations applied to the current instance.</em>

## [3xx Redirection](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#3xx_Redirection)

This class of status code indicates the client must take additional action to complete the request. Many of these status codes are used in URL redirection.

A user agent may carry out the additional action with no user interaction only if the method used in the second request is GET or HEAD. A user agent may automatically redirect a request. A user agent should detect and intervene to prevent cyclical redirects.

#### 300 Multiple Choices

<em>Indicates multiple options for the resource from which the client may choose (via agent-driven content negotiation). For example, this code could be used to present multiple video format options, to list files with different filename extensions, or to suggest word-sense disambiguation.</em>

#### 301 Moved Permanently

<em>This and all future requests should be directed to the given URI.</em>

#### 302 Found (Previously "Moved temporarily")

<em>Tells the client to look at (browse to) another URL. 302 has been superseded by 303 and 307. This is an example of industry practice contradicting the standard. The HTTP/1.0 specification (RFC 1945) required the client to perform a temporary redirect (the original describing phrase was "Moved Temporarily"), but popular browsers implemented 302 with the functionality of a `303 See Other`. Therefore, HTTP/1.1 added status codes 303 and 307 to distinguish between the two behaviors. However, some Web applications and frameworks use the 302 status code as if it were the 303.</em>

#### 303 See Other (since HTTP/1.1)

<em>The response to the request can be found under another URI using the GET method. When received in response to a POST (or PUT/DELETE), the client should presume that the server has received the data and should issue a new GET request to the given URI.</em>

#### 304 Not Modified (RFC 7232)*

<em>Indicates that the resource has not been modified since the version specified by the request headers If-Modified-Since or If-None-Match. In such case, there is no need to retransmit the resource since the client still has a previously-downloaded copy.</em>

<small>* Used for conditional GET calls to reduce band-width usage. If used, must set the Date, Content-Location, ETag headers to what they would have been on a regular GET call. There must be no body on the response.</small>

#### 305 Use Proxy (since HTTP/1.1)

<em>The requested resource is available only through a proxy, the address for which is provided in the response. For security reasons, many HTTP clients (such as Mozilla Firefox and Internet Explorer) do not obey this status code.</em>

#### 306 Switch Proxy

<em>No longer used. Originally meant "Subsequent requests should use the specified proxy."</em>

#### 307 Temporary Redirect (since HTTP/1.1)

<em>In this case, the request should be repeated with another URI; however, future requests should still use the original URI. In contrast to how 302 was historically implemented, the request method is not allowed to be changed when reissuing the original request. For example, a POST request should be repeated using another POST request.</em>

#### 308 Permanent Redirect (RFC 7538)

<em>The request and all future requests should be repeated using another URI. 307 and 308 parallel the behaviors of 302 and 301, but do not allow the HTTP method to change. So, for example, submitting a form to a permanently redirected resource may continue smoothly.</em>

## [4xx Client Errors](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_errors)

This class of status code is intended for situations in which the error seems to have been caused by the client. Except when responding to a HEAD request, the server should include an entity containing an explanation of the error situation, and whether it is a temporary or permanent condition. These status codes are applicable to any request method. User agents should display any included entity to the user.

#### 400 Bad Request*

<em>The server cannot or will not process the request due to an apparent client error (e.g., malformed request syntax, size too large, invalid request message framing, or deceptive request routing).</em>

<small>* General error when fulfilling the request would cause an invalid state. Domain validation errors, missing data, etc. are some examples.</small>

#### 401 Unauthorized (RFC 7235)*

<em>Similar to `403 Forbidden`, but specifically for use when authentication is required and has failed or has not yet been provided. The response must include a WWW-Authenticate header field containing a challenge applicable to the requested resource. See Basic access authentication and Digest access authentication. 401 semantically means "unauthorized", the user does not have valid authentication credentials for the target resource.</em>

<em>Note: Some sites incorrectly issue HTTP 401 when an IP address is banned from the website (usually the website domain) and that specific address is refused permission to access a website.</em>

<small>* Error code response for missing or invalid authentication token</small>

#### 402 Payment Required

<em>Reserved for future use. The original intention was that this code might be used as part of some form of digital cash or micropayment scheme, as proposed for example by GNU Taler, but that has not yet happened, and this code is not usually used. Google Developers API uses this status if a particular developer has exceeded the daily limit on requests. Sipgate uses this code if an account does not have sufficient funds to start a call. Shopify uses this code when the store has not paid their fees and is temporarily disabled.</em>

#### 403 Forbidden*

<em>The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort. This code is also typically used if the request provided authentication via the WWW-Authenticate header field, but the server did not accept that authentication.</em>

<small>* Error code for user not authorized to perform the operation or the resource is unavailable for some reason (e.g. time constraints, etc.).</small>

#### 404 Not Found*

<em>The requested resource could not be found but may be available in the future. Subsequent requests by the client are permissible.</em>

<small>* Used when the requested resource is not found, whether it doesn't exist or if there was a 401 or 403 that, for security reasons, the service wants to mask.</small>

#### 405 Method Not Allowed

<em>A request method is not supported for the requested resource; for example, a GET request on a form that requires data to be presented via POST, or a PUT request on a read-only resource.</em>

#### 406 Not Acceptable

<em>The requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request.[39] See Content negotiation.</em>

#### 407 Proxy Authentication Required (RFC 7235)

<em>The client must first authenticate itself with the proxy.</em>

#### 408 Request Timeout

<em>The server timed out waiting for the request. According to HTTP specifications: "The client did not produce a request within the time that the server was prepared to wait. The client MAY repeat the request without modifications at any later time."</em>

#### 409 Conflict*

<em>Indicates that the request could not be processed because of conflict in the current state of the resource, such as an edit conflict between multiple simultaneous updates.</em>

<small>* Whenever a resource conflict would be caused by fulfilling the request. Duplicate entries and deleting root objects when cascade-delete is not supported are a couple of examples.</small>

#### 410 Gone

<em>Indicates that the resource requested is no longer available and will not be available again. This should be used when a resource has been intentionally removed and the resource should be purged. Upon receiving a 410 status code, the client should not request the resource in the future. Clients such as search engines should remove the resource from their indices. Most use cases do not require clients and search engines to purge the resource, and a `404 Not Found` may be used instead.</em>

#### 411 Length Required

<em>The request did not specify the length of its content, which is required by the requested resource.</em>

#### 412 Precondition Failed (RFC 7232)

<em>The server does not meet one of the preconditions that the requester put on the request.</em>

#### 413 Payload Too Large (RFC 7231)

<em>The request is larger than the server is willing or able to process. Previously called "Request Entity Too Large".</em>

#### 414 URI Too Long (RFC 7231)

<em>The URI provided was too long for the server to process. Often the result of too much data being encoded as a query-string of a GET request, in which case it should be converted to a POST request.[46] Called "Request-URI Too Long" previously.</em>

#### 415 Unsupported Media Type (RFC 7231)
<em>The request entity has a media type which the server or resource does not support. For example, the client uploads an image as image/svg+xml, but the server requires that images use a different format.</em>

#### 416 Range Not Satisfiable (RFC 7233)

<em>The client has asked for a portion of the file (byte serving), but the server cannot supply that portion. For example, if the client asked for a part of the file that lies beyond the end of the file. Called "Requested Range Not Satisfiable" previously.</em>

#### 417 Expectation Failed

<em>The server cannot meet the requirements of the Expect request-header field.</em>

#### 418 I'm a teapot (RFC 2324, RFC 7168)

<em>This code was defined in 1998 as one of the traditional IETF April Fools' jokes, in RFC 2324, Hyper Text Coffee Pot Control Protocol, and is not expected to be implemented by actual HTTP servers. The RFC specifies this code should be returned by teapots requested to brew coffee. This HTTP status is used as an Easter egg in some websites, including Google.com.</em>

#### 421 Misdirected Request (RFC 7540)

<em>The request was directed at a server that is not able to produce a response[55] (for example because of connection reuse).</em>

#### 422 Unprocessable Entity (WebDAV; RFC 4918)

<em>The request was well-formed but was unable to be followed due to semantic errors.</em>

#### 423 Locked (WebDAV; RFC 4918)

<em>The resource that is being accessed is locked.</em>

#### 424 Failed Dependency (WebDAV; RFC 4918)

<em>The request failed because it depended on another request and that request failed (e.g., a PROPPATCH).</em>

#### 425 Too Early (RFC 8470)

<em>Indicates that the server is unwilling to risk processing a request that might be replayed.</em>

#### 426 Upgrade Required

<em>The client should switch to a different protocol such as TLS/1.0, given in the Upgrade header field.</em>

#### 428 Precondition Required (RFC 6585)

<em>The origin server requires the request to be conditional. Intended to prevent the 'lost update' problem, where a client GETs a resource's state, modifies it, and PUTs it back to the server, when meanwhile a third party has modified the state on the server, leading to a conflict.</em>

#### 429 Too Many Requests (RFC 6585)

<em>The user has sent too many requests in a given amount of time. Intended for use with rate-limiting schemes.</em>

#### 431 Request Header Fields Too Large (RFC 6585)

<em>The server is unwilling to process the request because either an individual header field, or all the header fields collectively, are too large.</em>

#### 451 Unavailable For Legal Reasons (RFC 7725)

<em>A server operator has received a legal demand to deny access to a resource or to a set of resources that includes the requested resource.[59] The code 451 was chosen as a reference to the novel Fahrenheit 451 (see the Acknowledgements in the RFC).</em>

## [5xx Server Errors](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_errors)

The server failed to fulfill a request.

Response status codes beginning with the digit "5" indicate cases in which the server is aware that it has encountered an error or is otherwise incapable of performing the request. Except when responding to a HEAD request, the server should include an entity containing an explanation of the error situation, and indicate whether it is a temporary or permanent condition. Likewise, user agents should display any included entity to the user. These response codes are applicable to any request method.

#### 500 Internal Server Error*

<em>A generic error message, given when an unexpected condition was encountered and no more specific message is suitable.</em>

<small>* The general catch-all error when the server-side throws an exception.</small>

#### 501 Not Implemented

<em>The server either does not recognize the request method, or it lacks the ability to fulfill the request. Usually this implies future availability (e.g., a new feature of a web-service API).</em>

#### 502 Bad Gateway

<em>The server was acting as a gateway or proxy and received an invalid response from the upstream server.</em>

#### 503 Service Unavailable

<em>The server cannot handle the request (because it is overloaded or down for maintenance). Generally, this is a temporary state.</em>

#### 504 Gateway Timeout

<em>The server was acting as a gateway or proxy and did not receive a timely response from the upstream server.</em>

#### 505 HTTP Version Not Supported

<em>The server does not support the HTTP protocol version used in the request.</em>

#### 506 Variant Also Negotiates (RFC 2295)

<em>Transparent content negotiation for the request results in a circular reference.</em>

#### 507 Insufficient Storage (WebDAV; RFC 4918)

<em>The server is unable to store the representation needed to complete the request.</em>

#### 508 Loop Detected (WebDAV; RFC 5842)

<em>The server detected an infinite loop while processing the request (sent instead of `208 Already Reported`).</em>

#### 510 Not Extended (RFC 2774)

<em>Further extensions to the request are required for the server to fulfill it.</em>

#### 511 Network Authentication Required (RFC 6585)

<em>The client needs to authenticate to gain network access. Intended for use by intercepting proxies used to control access to the network (e.g., "captive portals" used to require agreement to Terms of Service before granting full Internet access via a Wi-Fi hotspot).</em>
