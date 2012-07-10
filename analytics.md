# Analytics
Sugestio periodically generates reports on the state of your data and the activity of your users. Weekly reports are generated each Monday. Monthly reports are generated at the start of each month. Reports consist of two section. The _totals_ section looks at the data set as a whole and shows long term trends. The _period_ section looks more closely at data from the previous week or month.

Supported formats:
* json

## Request

### Method

* GET

### URLs

/sites/**{account}**/analytics.json
/sites/**{account}**/analytics/weekly.json
/sites/**{account}**/analytics/monthly.json

* **account** - your account key.

/sites/**{account}**/analytics/**{id}**.json

* **account** - your account key.
* **id** - a string that uniquely identifies a report.

### Query parameters

## Response

### HTTP status codes

* **200 OK** - the response body contains analytics data.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body

The response body consists of one or more analytics reports. Due to their large size, the _analytics.json_ resource contains a only a minimal representation of the available reports. Complete reports can then be retrieved through their unique identifier. The _weekly.json_ and _monthly.json_ resources contain multiple complete reports. A report has the following minimal attributes:

* **id** - a string that uniquely identifies the report.
* **type** - defines the evaluation period. Possibly values:
	* **weekly** - the report contains an evaluation of a one week period.
	* **monthly** - the report contains an evalation of a one month period.
* **from_epoch** - beginning of the evaluation period
* **from_readable** - beginning of the evaluation period.
* **until_epoch** - end of the evaluation period
* **until_readable** - end of the evaluation period.

Complete reports also have the following attributes:

* **totals** - report section containing information on the entire data set. Subsections:
	* **counts** - contains the following counters:
		* **consumptions** - number of consumptions.
		* **items** - number of items with metadata and/or consumption data.
		* **items_active** - number of items with consumption data.
		* **users** - number of users with metadata and/or consumption data.
		* **users_active** - number of users with consumption data.
	* **consumptions** - detailed analysis of a particular consumption type **(array)**
		* **type** - consumption type.
		* **detail** - consumption detail.
		* **count** - number of consumptions.
		* **users_active** - number of users that have consumptions of this type.		
		* **user_distribution** - number of users with a given amount of consumptions of this type (P95)  **(array)**
			* **consumptions** - number of consumptions
			* **users** - number of users
		* **items_active** - number of items that have consumptions of this type.
		* **item_distribution** - number of items with a given amount of consumptions of this type (P95)  **(array)**
			* **consumptions** - number of consumptions
			* **users** - number of items

* **period** - report section containing information on data from the evaluation period. Subsections:
	* **counts** - contains the following counters:
		* **consumptions** - number of consumptions.
		* **items_active** - number of items that had consumptions during the evaluation period.
		* **items_new** - number of items that had no consumptions prior to the evaluation period.
		* **items_returning** - number of items that already had consumptions prior to the evaluation period.
		* **users_active** - number of users that had consumptions during the evaluation period.
		* **users_new** - number of users that had no consumptions prior to the evaluation period.
		* **users_returning** - number of users that already had consumptions prior to the evaluation period.
	* **consumptions** - detailed analysis of a particular consumption type **(array)**
		* **type** - consumption type.
		* **detail** - consumption detail.
		* **count** - number of consumptions.
		* **users_active** - number of users that have consumptions of this type.
		* **users_returning** - number of users that already had consumptions of this type prior to this evaluation period.
		* **users_new** - number of users that had no consumptions of this type prior to this evaluation period.
		* **user_distribution** - number of users with a given amount of consumptions of this type (P95)  **(array)**
			* **consumptions** - number of consumptions.
			* **users** - number of users with this many consumptions.
		* **items_active** - number of items that have consumptions of this type.
		* **items_returning** - number of items that already had consumptions of this type prior to this evaluation period.
		* **items_new** - number of items that had no consumptions of this type prior to this evaluation period.
		* **item_distribution** - number of items with a given amount of consumptions of this type (P95)  **(array)**
			* **consumptions** - number of consumptions.
			* **users** - number of items with this many consumptions.
	* **webservice** - an overview of the webservice usage during the evaluation period. Each element contains a counter for each potential HTTP response (e.g. 200 or 404):
		* **get_recommendation**
			* **200** - number of HTTP 200/OK responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **404** - number of HTTP 404/Not Found responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **get_similaritem**
			* **200** - number of HTTP 200/OK responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **404** - number of HTTP 404/Not Found responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **get_similaruser**
			* **200** - number of HTTP 200/OK responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **404** - number of HTTP 404/Not Found responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **post_consumption**
			* **202** - number of HTTP 202/Accepted responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **post_item**
			* **202** - number of HTTP 202/Accepted responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **post_user**
			* **202** - number of HTTP 202/Accepted responses.
			* **400** - nulber of HTTP 400/Bad Request responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **delete_consumption**
			* **202** - number of HTTP 202/Accepted responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **delete_item**
			* **202** - number of HTTP 202/Accepted responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* **delete_user**
			* **202** - number of HTTP 202/Accepted responses.
			* **400** - number of HTTP 400/Bad Request responses.
			* **500** - number of HTTP 500/Internal Server Error responses.
		* ...
