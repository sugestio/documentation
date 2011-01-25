# Delete item metadata
Item metadata that was previously submitted, can be deleted. This operation does not delete any of the consumption data associated with this item.

Supported formats:

* any

## Request

### Method

* DELETE

### URL

http://api.sugestio.com/sites/**{account}**/items/**{itemid}**.**{format}**

* **account** - your account key.
* **itemid** - a string that uniquely identifies the item.
* **format** - response format.

## Response

### HTTP status codes

* **202 Accepted** - the item metadata will be deleted.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

## Examples

Delete metadata associated with item 874: 

	DELETE /sites/sandbox/items/874.csv

Delete metadata associated with item qa362fdd:

	DELETE /sites/sandbox/items/qa362fdd.xml