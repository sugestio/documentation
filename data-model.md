# Data model
Sugestio uses a simple, generic datamodel that consists of three data types:

* **consumptions**: user behavior data
* **items**: item metadata
* **users**: user metadata

The following image illustrates how these entities relate to one another. In the next few sections, each entity is discussed in more detail.

<img src="http://www.sugestio.com/sites/default/files/datamodel-small.png" alt="Data model illustration"/>

## Consumption data
Sugestio uses consumption data to learn about the behavioral patterns of the user. Generally speaking, users _consume_ items. For example:

* A customer purchases a DVD. 
* A website visitor rates an article
* A tourist visits a museum exhibition.
* ...

Consumptions must therefore identify the user and the item. Even if no other data is available, consumption data alone is sufficient to get recommendations.

### Consumption attributes

All fields are scalar and optional, unless indicated otherwise.

* **userid (required)** - a string that uniquely identifies the user.
* **itemid (required)** - a string that uniquely identifies the item.
* **id** - a string that uniquely identifies the consumption. Automatically generated (UUID v4) if this field is omitted.
* **type** - the type of consumption. Supported values:
	* **VIEW** - the user has viewed (or clicked) this item.
	* **RATING** - the user has rated this item.
	* **WISHLIST** - the user has added this item to their wishlist.
	* **BASKET** - the user has added this item to their shopping basket.
	* **PURCHASE** - the user has purchased this item
	* **COLLECTION** - the user has added this item to their collection.
	* **CHECKIN** - the user has been to this location.
* **detail** - detailed information about the consumption. The value of this field depends on the type of consumption. See *ratings* section for more information on submitting rating data.
* **date** - the moment of consumption. See *timestamps* section for more information.
* **location_simple** - location where the item is consumed. (e.g. *home*, *office*)
* **location_latlong** - decimal degree coordinates of the consumption location.

## Item metadata
Item metadata provides additional, descriptive information about the items. For example:

* Article keywords
* Product categories
* Book author
* ...

There are three ways in which Sugestio can use item metadata:

### Better user profiling
Content-based algorithms combine consumption patterns with item metadata to create an interest profile for each user. This profile can then be used to recommend new items that fit the user's interests.

### Intelligent recommendations
Item metadata can be used to filter recommendations to avoid inappropriate or ill-fitting recommendations. For example:

* Do not recommend products which are not currently in stock
* Only recommend events within walking distance
* Do not show DVD recommendations in the Music section of the shop

### Easier visualization, reduced server load
Recommendations are typically visualized as a block or as a list of product thumbnails. These thumbnails link to the product detail page. Sugestio attaches the item metadata to each recommendation. By submitting information like product name or thumbnail URL, it is not necessary to hit the database when visualizing the recommendations. The web service provides all the information that is needed to generate an visually attractive recommendation block.

### Item attributes

All attributes are scalar and optional, unless indicated otherwise.

* **id (required)** - a string that uniquely identifies the item.
* **title** - item title.
* **available** - can this item be recommended? Supported values:
	* **Y** - yes. (default)
	* **N** - no. Can be used to indicate that an item is out of stock.
* **published** - publication date. See *timestamps* section for more information.
* **description_short** - a short description of the item. (e.g. abstract)
* **description_full** - a full description of the item. (ex: page text)
* **from** - do not recommend the item before this date. See *timestamps* section for more information.
* **until** - do not recommend the item after this date. See *timestamps* section for more information.
* **location_city** - a string that uniquely identifies a city. e.g. the city name or postal code.
* **location_simple** - a string that uniquely identifies a location. e.g. a music venue, an art house.
* **location_latlong** - decimal degree coordinates of the item's location.
* **creator (array)** - artist, manufacturer, uploader, ...
* **tag (array)** - tags or keywords that describe the item.
* **category (array)** - the categories that this item belongs to.
* **segment (array)** - the content segment that this item belongs to.
* **permalink** - a link to the item on your website.
* **thumbnail** - a link to a picture of the item.


## User metadata
User metadata provides some basic demographic information about the user. This information can be used to avoid inappropriate recommendations.

### User attributes

All fields are scalar and optional, unless indicated otherwise.

* **id (required)** - a string that uniquely identifies the user. 
* **location_latlong** - decimal degree coordinates of the user's home location.
* **gender** - gender of the user. Possible values:
	* **M** - male
	* **F** - female
* **birthday** - birthday of the user. See *timestamps* section for more information.
* **friend (array)** - friends of this user. The optional trust value allows the construction of a trust-relationship structure between users. Sub-arguments:
	* **userid (required)** - a string that uniquely identifies the friend.
	* **trust** - the level of trust that the user has in this friend. Between -1.0 and 1.0.
* **apml** - URL of the user's Attention profile
* **foaf** - URL of the user's FOAF profile
