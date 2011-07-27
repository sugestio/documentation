# Delete consumption metadata
Consumption data that was previously submitted, can be deleted individually by referring to the consumption id. It is also possible to delete all consumption data belonging to a particular user or a specific user-item pair.

Supported formats:

* any

## Request

### Method

* DELETE

### URLs

/sites/**{account}**/consumptions/**{consumptionid}**.**{format}**

* **account** - your account key.
* **consumptionid** - a string that uniquely identifies the consumption.
* **format** - response format.

/sites/**{account}**/users/**{userid}**/consumptions.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **format** - response format.

/sites/**{account}**/users/**{userid}**/consumptions/**{itemid}**.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **itemid** - a string that uniquely identifies the item.
* **format** - response format.

## Response

### HTTP status codes

* **202 Accepted** - the consumption will be deleted.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

## Examples

Delete consumption 38069781-1bb8-4a5b-b07c-a9a4da0d2115: 

	DELETE /sites/sandbox/consumptions/38069781-1bb8-4a5b-b07c-a9a4da0d2115.xml

Delete all consumption data of user A:

	DELETE /sites/sandbox/users/A/consumptions.json

Delete all consumptions of item X by user A:

	DELETE /sites/sandbox/users/A/consumptions/X.csv