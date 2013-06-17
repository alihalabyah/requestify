http-request - Simplifies nodeJS HTTP requests [![Build Status](https://secure.travis-ci.org/ranm8/http-request.png?branch=master)](http://travis-ci.org/ranm8/http-request)
==============================================

http-request is a nodeJS module that simplifies HTTP request making.

Importent to note, this module is still under development and can be unstable!

## Install

	npm install http-request  


## Ease of use

http-request is extremely easy to use and always return a promise (using the great Q module)...

Simply require the module and start requesting:

	var httpRequest = require('http-request'); 

GET Request:

	httpRequest.get('http://example.com').then(function(response) {
		// Get the response body
		response.getBody();
	});

POST Request in JSON:

	httpRequest.post('http://example.com', {
			params: {
				hello: 'world'
			},
			dataType: 'json'	
		})
		.then(function(response) {
			// Get the response body
			response.getBody();
		});


## API

### options

* `method` {string} - HTTP method to use, can be one of the following - POST|GET|DELETE|HEAD|PUT.
* `params` {object|string} - Can be either an object (key, val) or string, will be formatted according to the dataType property and served via response body.
* `headers` {object} - (key, value) object of headers (some headers like content-length are set by default)
* `cookies` {object} - (key, value) object of cookies to encode and serve via the request header.
* `auth` {{ username: string, password: string }} - Adds Basic authintication header with given username and password
* `dataType` {string} - Determines the request data type (json|form-url-encoded), this option will encode the request body according to the given dataType and will add the appropriate header.

### httpRequest.request(url, options)

Executes a custom request according to options object

	httpRequest.request('https://example.com/api/foo', {
		method: 'POST',
		params: {
			foo: 'bar'
			bar: 'foo'
		},
		headers: {
			'X-Forwarded-By': 'me'
		},
		cookies: {
			mySession: 'some cookie value'
		},
		auth: {
			username: 'foo',
			password: 'bar'
		},
		dataType: 'json'		
	})
	.then(function(response) {
		// get the response body
		response.getBody();
		
		// get the response headers
		response.getHeaders();
		
		// get specific response header
		response.getHeader('Accept');
		
		// get the code
		response.getCode();
	});

### httpRequest.get(url, options)

Exceutes a GET method request

	httpRequest.get('http://example.com').then(function(response) {
		// Get the response body
		response.getBody();
	});

### httpRequest.post(url, options)

Exceutes a POST method request

	httpRequest.post('http://example.com', {
		params: {
			hello: 'world'
		}
	})
	.then(function(response) {
		// Get the response body
		response.getBody();
	});


### httpRequest.put(url, options)

Exceutes a PUT method request

	httpRequest.put('http://example.com', {
		params: 'some file content',
		dataType: null	
	})
	.then(function(response) {
		// Get the response body
		response.getBody();
	});


### httpRequest.del(url, options)

Exceutes a DELETE method request

	httpRequest.del('http://example.com').then(function(response) {
		// Get the response body
		response.getBody();
	});


### httpRequest.head(url, options)

Exceutes a HEAD method request
	
	httpRequest.head('http://example.com').then(function(response) {
		// Get the response body
		response.getCode();
	});


