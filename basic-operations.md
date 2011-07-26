# Basic operations
This chapter gives a broad overview of the different types of data operations that are supported by the web service. Chapter 2 (_Manage your data set_) provides more extensive documentation and detailed examples for each operation and resource. When managing your data set, submitting or deleting resources are the most important operation types. Retrieval operations provide a way to double check that the data that was submitted made it through okay. Bulk export allows for all submitted data to be retrieved with one request.

## Submitting or updating
Resources can be created or updated by issuing a POST request. The request body contains a representation of the resource that is being submitted. Resources can be presented as Form data, JSON or XML.

### Create or update an item

	POST /sites/my_account/items.json

### Create a consumption

	POST /sites/my_account/users/1/consumptions.json

## Deleting
Resources can be deleted by issuing a DELETE request. Note that metadata and consumption data are independent resources. Deleting the metadata for an item does not delete the consumptions of that item, or vice-versa.

### Delete all metadata for a particular item

	DELETE /sites/my_account/items/1.json

### Delete all metadata for a particular user

	DELETE /sites/my_account/users/1.json

### Delete consumption data for user 1
The previous request deleted only the user metadata. The user's consumptions were not affected in any way. The following request must be issued to delete all consumption data related to this user:

	DELETE /sites/my_account/users/1/consumptions.json

## Retrieving
Resources can be retrieved by issuing a GET request.

### Retrieve all metadata for a particular item

	GET /sites/my_account/items/1.json

### Retrieve a consumption

	GET /sites/my_account/consumptions/ad0edefc-da6d-40ca-a0f6-8b290adf95c5.json

## Bulk export
Resources can be retrieved in bulk by issuing a GET request.

### Retrieve all item metadata

	GET /sites/my_account/items.json

### Retrieve all consumptions

	GET /sites/my_account/consumptions.json