# Ratings
The *detail* parameter of a consumption contains information about the rating system and the rating value. Currently, STAR, THUMB and PERCENTAGE ratings are supported.

## Star ratings

### Structure

STAR:**{max}**:**{min}**:**{value}**

* **max** - the maximum number of that stars users can award.
* **min** - the minimum number of that stars users can award.
* **value** - the number of stars that were awarded.	

### Examples

In the following example, the rating system is five-star voting where users can rate content from one to five. Here, the user awarded three stars:

	STAR:5:1:3

A four-star voting system, users can rate content from zero to four. The user awarded two stars:

	STAR:4:0:2

## Thumbs

### Structure

THUMB:**{value}**

* **value** - up or down.

### Examples

Thumbs up:

	THUMB:UP

Thumbs down:

	THUMB:DOWN

## Percentage

### Structure

PERCENTAGE:**{value}**

* **value** - the percentage awarded.

### Examples

The user rated the content 85%:

	PERCENTAGE:85

## More examples

### POST parameters

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: application/x-www-form-urlencoded

	userid=1&itemid=150&type=RATING&detail=STAR:5:1:3

### Xml data

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: text/xml

	<consumptions>
		<consumption>
			<userid>1</itemid>
			<itemid>150</itemid>
			<type>RATING</type>
			<detail>THUMB:UP</detail>	
		</consumption>
	</consumptions>