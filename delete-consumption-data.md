# Delete consumption metadata
Consumption data that was previously submitted, can be deleted. 

Supported formats:

* any

## Request

### Method

* DELETE

### URL

http://api.sugestio.com/sites/**{account}**/consumptions/**{consumptionid}**.**{format}**

* **account** - your account key.
* **consumptionid** - a string that uniquely identifies the consumption.
* **format** - response format.

## Response

### HTTP status codes

* **202 Accepted** - the consumption will be deleted.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

## Examples

Delete consumption 38069781-1bb8-4a5b-b07c-a9a4da0d2115: 

	DELETE /sites/sandbox/consumptions/38069781-1bb8-4a5b-b07c-a9a4da0d2115.xml