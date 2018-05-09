# API design guide and conventions
Designing good APIs is key to our growth as we push more things into front-end applications. To that end, we should standardize conventions and follow general good practices while building the APIs.

## TL;DR version:
* [Make your APIs RESTful](#restful-apis)
* [Return useful and meaningful responses](#useful-and-meaningful-responses)
* [Use HTTP codes effectively](#http-codes)
* [Use SSL everywhere](#ssl)
* [Take time to make responses pretty and understandable](#pretty-responses)
* [Namespace and version the api](#namespacing)
* [Dates](#dates)

## RESTful APIs

* As much as possible, make your APIs restful.

Example:
```java
@RequestMapping(path = "me/tasks", method = RequestMethod.GET)
@RequestMapping(path = "tasks/{id}", method = RequestMethod.GET)
@RequestMapping(path = "tasks", method = RequestMethod.POST)
```


## Useful and meaningful responses

* It is important to return responses that make sense.
* The response should be in JSON format and varies depending on the type of request:

Request Type |  Response
--- | ---
GET | the entity corresponding to the requested resource
POST |  the entity that is created
PUT | the entity that is updated
DELETE | the entity the is deleted

* It is also important to return error messages should something go wrong.


## HTTP codes

* HTTP codes are a great way to indicate the status of the response and should be used properly.
* Use the following with the appropriate requests:


HTTP Code | Usage
--- | ---
200/202 | Response to a successful GET or PUT. Can also be used for a POST that doesn't result in a creation
201 | Response to a successful POST request that results in a creation
204 | Response to a successful DELETE
400 | Response when the request is malformed (eg. request body cannot be parsed)
401 | When the request is not authenticated with the proper credentials(eg. visitor accessing an endpoint without authenticating)
403 | When the request is authenticated, but not authorized to request the resource(eg. User accessing another user’s resources)
404 | When the requested resource is not found
422 | When there are validation errors


## SSL

* Always use SSL. **No exceptions**.
* Today, your web APIs can get accessed from anywhere there is internet (like libraries, coffee shops, airports among others). Not all of these are secure. Many don't encrypt communications at all, allowing for easy eavesdropping or impersonation if authentication credentials are hijacked.


## Pretty Responses

* Make sure that the response keys are all readable and meaningful.
* Denormalize data in the response and nest data as needed so that the response makes sense.


## Namespacing

* Versioning your API is important if you need to make drastic changes to your API.
* One way to version your API is in the url by namespacing your api endpoints

Example:
```java
@RequestMapping(path = "/internal/v0/workflow-service/", produces = "application/json")
```

* NOTE: Another way to version your API is in the headers, but this is not the preferred way of versioning at NYSHEX.


## Dates

* Always return dates in ISO 8601 format.
