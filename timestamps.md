# Timestamps
Timestamps, such as a date of birth or the time of consumption, can be submitted in several formats. The timezone is always UTC.

## Unix time

Number of seconds since midnight, January 1, 1970 UTC. Example:

	1278448474

## Short

Year, month and day. Examples: 

	2010-07-01
	1990-12-31

## Medium

Year, month, day, hour, minutes. Examples: 

	2010-07-01T15:00
	1990-12-31T09:00

## Long

Year, month, day, hour, minutes, seconds. Examples:

	2010-07-01T15:00:00
	1990-12-31T09:00:00

## Automatic

Putting *NOW* as the value for a date attribute automatically assigns the current date.

## More examples

### POST parameters

Automatically assign the current date:

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: application/x-www-form-urlencoded

	userid=1&itemid=150&date=NOW

### Xml data

An example of the long timestamp format:

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: text/xml

	<consumptions>
		<consumption>
			<userid>1</itemid>
			<itemid>150</itemid>
			<date>2010-08-01T08:17</date>
		</consumption>
	</consumptions>