aka,. HTTP or HTTPs

HTTP is a **"Stateless"** Protocol, which means that each command runs independent of any other command.

The Hypertext Transfer Protocol (HTTP) is the foundation of the World Wide Web, and is used to load webpages using hypertext links, text that contains links (URLs) to other resource. 

HTTP is an [application layer](https://www.cloudflare.com/learning/ddos/application-layer-ddos-attack/) protocol designed to transfer information between networked devices and runs on top of other layers of the network [protocol](https://www.cloudflare.com/learning/network-layer/what-is-a-protocol/) stack. A typical flow over HTTP involves a client machine making a request to a server, which then sends a response message.

In simple word, Website data is requested via HTTP internet communication protocol.
![[Pasted image 20250917201423.png]]

Each HTTP request made across the Internet carries with it a series of encoded data that carries different types of information. **A typical HTTP request contains:**

1. **HTTP version type**
2. **a URL**
3. **an HTTP method**
4. **HTTP request headers**
5. **Optional HTTP body.**

### HTTP URLs
A URL, or [Uniform Resource Locator](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL), is the address of another computer, or "server" on the internet. Part of the URL specifies _where to reach_ the server, and part of it tells the server _what information we want_.

### HTTP Method
An HTTP method, sometimes referred to as an HTTP verb, indicates the action that the HTTP request expects from the queried server. 

For example, two of the most common HTTP methods are ‘GET’ and ‘POST’:
1. A ‘GET’ request expects information back in return (usually in the form of a website) 
2. A ‘POST’ request typically indicates that the client is submitting information to the web server (such as form information, e.g. a submitted username and password).

### HTTP Request headers
HTTP headers contain text information stored in key-value pairs, and they are included in every HTTP request (and response, more on that later). These headers communicate core information, such as what browser the client is using and what data is being requested.

Example of HTTP request headers from Google Chrome's network tab:
![[http-request-headers.png]]

### HTTP Request body
The body of a request is the part that contains the ‘body’ of information the request is transferring. The body of an HTTP request contains any information being submitted to the web server, such as a username and password, or any other data entered into a form.


### HTTP Status code
HTTP status codes are 3-digit codes most often used to indicate whether an HTTP request has been successfully completed. Status codes are broken into the following 5 blocks:

1. 1xx Informational
2. 2xx Success
3. 3xx Redirection
4. 4xx Client Error
5. 5xx Server Error



![[ga7wRus-1019x720.png]]

```js
const apiKey = 'some_random_api_key';
const itemURL = 'https://someapi.com';

const items = await getData(itemURL);

async function getData(url){
	const response = await fetch(url,{
		method: 'GET',
		mode: 'cors',
		header:{
			"X-API-Key": apiKey,
			"Content-Type": "application/json",
		},
	});
	return response.json();
};
```

**Using URLs in HTTP**
The `http://` at the beginning of a [website URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL) specifies that the `http` protocol will be used for communication.
Other communication protocols use URLs as well, (hence "Uniform Resource Locator"). That's why we need to be specific when we're making HTTP requests by prefixing the URL with `http://`

### JavaScript Fetch API
The `fetch` function is made available to us by the JavaScript language running in the browser, all we have to do is provide it with the parameters it requires.

```js
const response = await fetch(url, settings);
const responseData = await response.json();
```

- `response` is the data that comes back from the server
- `url` is the URL we are making a request to
- `settings` is an object containing some request-specific settings
- The `await` keyword tells JavaScript to wait until the response comes back from the server before continuing
- `response.json()` converts the response data from the server into a JavaScript object

### Web Servers
Web server is used to store, sort, and serve that data so that it sticks around for longer than a single session, and can be accessed by multiple devices.

**Listening and Serving Data**
Similar to how a server at a restaurant brings your food to the table, a [web server](https://en.wikipedia.org/wiki/Web_server) serves web resources, such as web pages, images, and other data. The server is turned on and "listening" for inbound requests constantly so that the second it receives a new request, it can send an appropriate response.

### A Server Is Just a Computer
"Server" is just the name we give to a computer that is taking on the role of serving data across a network connection. A good server is turned on and available 24 hours a day, 7 days a week. While your laptop _can_ be used as a server, it makes more sense to use a computer in a data center that's designed to be up and running constantly.