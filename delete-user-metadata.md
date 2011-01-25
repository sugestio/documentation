# Delete user metadata
User metadata that was previously submitted, can be deleted. This operation does not delete any of the consumption data associated with this user.

Supported formats:

* any

## Request

### Method

* DELETE

### URL

http://api.sugestio.com/sites/**{account}**/users/**{userid}**.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains user metadata.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there is no metadata for this user.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

## Examples

Delete metadata associated with user 17: 

	DELETE /sites/sandbox/users/17.json

Delete metadata associated with user ae54t16:

	DELETE /sites/sandbox/users/ae54t16.xml