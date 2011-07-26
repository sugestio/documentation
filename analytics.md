# Analytics
Sugestio provides two sets of metrics. A first set of parameters evaluates the performance of the recommendation algoritm and compares it against common techniques like popular recommendations and random recommendations. The second set of metrics relates to the sparsity of the data set.

Supported formats:

* csv
* json
* xml

## Request

### Method

* GET

### URL

/sites/**{account}**/analytics.**{format}**

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

The response body consists of a series of analytics reports. A report has the following attributes:

* **id** - a string that uniquely identifies the report
* **performance attributes :**
	* **evaluation_Algorithm**
	* **evaluation_F1**
	* **evaluation_Precision**
	* **evaluation_Recall**
	* **evaluation_Recommendations**
	* **evaluation_RelevantItems**
	* **evaluation_RelevantRecommendations**
	* **evaluation_TestSetFrom**
	* **evaluation_TestSetUntil**
	* **evaluation_TrainingSetFrom**
	* **evaluation_TrainingSetUntil**
	* **popular_F1**
	* **popular_Precision**
	* **popular_Recall**
	* **popular_Recommendations**
	* **popular_RelevantItems**
	* **popular_RelevantRecommendations**
	* **random_F1**
	* **random_Precision**
	* **random_Recall**
	* **random_Recommendations**
	* **random_RelevantItems**
	* **random_RelevantRecommendations**
* **sparsity attributes :**
	* **sparsity_AvgConsumptionsPerItemInTestSet**
	* **sparsity_AvgConsumptionsPerItemInTrainingSet**
	* **sparsity_AvgConsumptionsPerItemInTrainingSetForTestItems**
	* **sparsity_AvgConsumptionsPerUserInTestSet**
	* **sparsity_AvgConsumptionsPerUserInTrainingSet**
	* **sparsity_AvgConsumptionsPerUserInTrainingSetForTestUsers**
	* **sparsity_ConsumptionsInTestSet**
	* **sparsity_ConsumptionsInTrainingSet**
	* **sparsity_ItemsInTestSet**
	* **sparsity_ItemsInTrainingSet**
	* **sparsity_PercTrainingItemsConsumedInTestSet**
	* **sparsity_PercTrainingUsersConsumingInTestSet**
	* **sparsity_SparsityTestMatrix**
	* **sparsity_SparsityTrainingMatrix**
	* **sparsity_UsersInTestSet**
	* **sparsity_UsersInTrainingSet**

## Examples

### Response formats

For brevity, only partial output is shown.

#### Csv format

The first line contains the column names. Each remaining line represents a single report. Fields are separated by _comma_.

	id,evaluation_Algorithm,evaluation_F1,evaluation_Precision,evaluation_Recall,...
	e2ddcbed-3da4-4626-83db-409ab5a4ccf8,UserBasedCF,0.0238095238,0.0269554753,0.0213211498,...
	03a49397-1cb4-4fe0-84a2-f26f8e5048e5,UserBasedCF,0.0246664424,0.0276035132,0.0222942846,...
	...

#### Json format

	[
		{
			"id":"e2ddcbed-3da4-4626-83db-409ab5a4ccf8",
			"evaluation_Algorithm":"UserBasedCF",
			"evaluation_F1":"0.0238095238",
			"evaluation_Precision":"0.0269554753",
			"evaluation_Recall":"0.0213211498",
			...
		},
		{
			"id":"03a49397-1cb4-4fe0-84a2-f26f8e5048e5",
			"evaluation_Algorithm":"UserBasedCF",
			"evaluation_F1":"0.0246664424",
			"evaluation_Precision":"0.0276035132",
			"evaluation_Recall":"0.0222942846"
			...
		},
		...
	]

#### Xml format

	<analytics>
		<report>
			<id>86a10a63-e6a9-4621-a80d-daeb8cee3828</id>
			<evaluation_Algorithm>UserBasedCF</evaluation_Algorithm>
			<evaluation_F1>0.0239962211</evaluation_F1>
			<evaluation_Precision>0.0299881936</evaluation_Precision>
			<evaluation_Recall>0.0200000000</evaluation_Recall>
			...
		</report>
		<report>
			<id>bd543c28-0df3-4782-a7b2-05f295bd53f5</id>
			<evaluation_Algorithm>UserBasedCF</evaluation_Algorithm>
			<evaluation_F1>0.0236622748</evaluation_F1>
			<evaluation_Precision>0.0294314381</evaluation_Precision>
			<evaluation_Recall>0.0197841727</evaluation_Recall>
			...
		</report>
		...
	</analytics>
