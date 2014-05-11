The HTTP statuses are returned to communicate the status of an API Call.

- 200 OK - valid request
- 302 Moved - endpoint at a different location
- 400 Bad Request - the client made a bad request, something was missing
- 402 Request Failed - the client request was ok, but something else is wrong, NOT a server error
- 404 Not Found - the requested endpoint doesn't exist
- 500 Internal Server Error - oh no, this is a server error.

### Error Format

	{ 
		Error: true, 
		message: "ERROR MESSAGE HERE" 
		type: "MACHINE READABLE MESSAGE"
	}

#### message
A human readable error description, for example "Invalid API Key." 


#### Error Type
Error type is a machine readable message and includes the following:

invalid_request
: The request was either malformed or missing the api key, user agent type or was the wrong type (GET vs POST)

invalid_token
: The requested opportunity/campaign/donation endpoint requires a token and it either wasn't found or was incorrect

missing_parameters
: Update/Create request was missing one or more required parameters

invalid_parameters
: Update/Create request contained all required parameters, but validation failed