# Analytics
The performance of personal recommendations is analysed periodically. This includes widely used metrics such as precision and recall.

Supported formats:

* csv
* json
* xml

## Request

### Method

* GET

### URL

http://api.sugestio.com/sites/**{account}**/analytics.**{format}**

* **account** - your account key.
* **format** - response format.

### Query parameters

* **limit** - maximum number of records to be retrieved.

## Response

### HTTP status codes

* **200 OK** - the response body contains analytics data.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body

The following attributes are always present in a response:

* **evaluation**
	* TestSetFrom
	* TestSetUntil
	* F1
	* NumRecommendations
	* NumRelevantItems
	* NumRelevantRecommendations
	* Precision
	* Recall
* **recommendation**
	* Algorithm
	* Completed
	* DefaultRecommenderClass
	* MainRecommenderClass
	* MinConsumptionsForItems
	* MinConsumptionsForUsers
	* MinSimilarityToSave
	* numOfRecommendationsPerUser
	* PercentageTrainingSetSize
* **sparsity**
	* AvgNumConsumptionsPerItemInTestSet
	* AvgNumConsumptionsPerItemInTrainingSet
	* AvgNumConsumptionsPerItemInTrainingSetForTestItems
	* AvgNumConsumptionsPerUserInTestSet
	* AvgNumConsumptionsPerUserInTrainingSet
	* AvgNumConsumptionsPerUserInTrainingSetForTestUsers
	* NumConsumptionsInTestSet
	* NumConsumptionsInTrainingSet
	* NumItemsInTestSet
	* NumItemsInTrainingSet
	* NumUserInTestSet
	* NumUserInTrainingSet
	* PercentageOfTrainingItemsConsumedInTestSet
	* PercentageOfTrainingUsersConsumingInTestSet
	* SparsityOfConsumptionMatrix
	* SparsityOfTestMatrix