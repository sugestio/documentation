# Security

REST calls to the Sugestio webservice are secured through 2-legged [OAuth](http://oauth.net), also known as "signed fetch". Our [client libraries](http://www.sugestio.com/libraries) leverage existing OAuth implementations, greatly reducing development time. OAuth libraries are currently available for every popular software platform.

Further reading:

* [A list of OAuth libraries](http://oauth.net/code/)
* [A comparisson of 2-legged and 3-legged OAuth protocols](http://sites.google.com/site/oauthgoog/2leggedoauth/2opensocialrestapi)
* [OAuth signing process](http://oauth.net/core/1.0#signing_process)