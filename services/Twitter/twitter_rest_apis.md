---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Using the Insights for Twitter REST APIs
{: #rest_apis}

*Last updated: 13 May 2016*

The {{site.data.keyword.twittershort}} service consists of RESTful APIs to search and consume Twitter content. The query language section below lists the query terms that are supported by the service APIs. Examples are provided to demonstrate how queries can be constructed.
{:shortdesc}

## REST API documentation {: #rest_api}
REST API documentation is built using Swagger, which allows you to test API operations and instantly view the results to help you build your applications faster.
The following API operations are currently available:

* Search: Finds Tweets in the Decahose or filtered PowerTrack stream.
* Count: Returns the number of Tweets based on a specified query.
* Check: Determines whether a list of messages complies with Twitter policies and Twitter users.
* Tracks: Provides Entry Plan users an assortment of endpoints to manage PowerTrack filters.

For more information on the supported REST APIs and its resources, see the [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window} reference. Select the region where your application exists. Each region is independent; you cannot use service credentials that are provisioned to you in one region to authenticate to a service in another region.

From the reference documentation, click **List Operations** to view details of each operation. After clicking the **Try it out!** button, you might be asked to provide credentials. You need to provide the user name and password from your **VCAP_SERVICES** environment variables. You can find this information by opening your application and clicking **Environment Variables** from the table of contents.

**Note**: Failure to enter proper credentials results in an "Unauthorized" message in the response body.

**Important**: Active tracks that are created using the **Try it out!** feature collects Tweets from Twitter, which count towards your monthly allowance. When tracks are no longer required, change their state to **Inactive** or simply delete the track.

<!-- 
The following video demonstrates the use of API operations from the API reference documentation and cURL examples entered from the command line. 

[//]: # <iframe width="420" height="315" src="https://www.youtube.com/embed/LZKVn496XJc" frameborder="0" allowfullscreen></iframe>

[//]: # To watch the video in a larger format, go to: [https://youtu.be/LZKVn496XJc](https://youtu.be/LZKVn496XJc){: new.window}
-->

## Query language {: #querylanguage}

With {{site.data.keyword.twittershort}}, you can search Twitter content using a rich set of query parameters and filters to produce more accurate results.

The following Boolean operators are supported in your queries. 

| **Operator**        | **Description**                                                                                                                   | **Examples**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| term1 **AND** term2 | Returns Tweets that contain both term1 and term2. White space between two terms is treated as AND, so the operator can be omitted. | `#ibm twitter`      |
| term1 **OR** term2  | Returns Tweets that contain either term1 or term2.    | `#money OR revenue` |
| -term1              | Returns Tweets that do not contain term1.  |`ibm -apple`  |

*Table 1. Boolean Operators*

Operator precedence: "-" takes precedence over "AND", and "AND" takes precedence over "OR". You should use parentheses to make operator precedence explicit. For example, `large animals` -(`giraffes` OR `bears`) searches for Tweets that contain the terms "large" and "animals", but excludes Tweets containing "giraffes" and "bears".

The following table lists the currently supported query terms.

| **Term** 	| **Description** 	| **Examples** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| keyword 	| Matches Tweets that have "keyword" in their body. The search is case-insensitive. 	| analytics 	|
| "exact phrase match" 	| Matches Tweets that contain the exact keyword sequence. 	| "IBM and analytics" 	|
| `#hashtag` 	| Matches Tweets with the hashtag *#hashtag*. 	| `#insight2015` 	|
| `bio_lang:language` 	| Matches Tweets from users whose profile language settings match the specified language code.  See `lang:` for a list of support languages. 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| Matches Tweets from users whose profile location setting contains the specified `location` reference. 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| Matches Tweets whose tagged place or location matches the specified country code. </br>**For a list of supported country codes, please see**: http://en.wikipedia.org/wiki/ISO_3166-1 	| `country_code:us` 	|
| `followers_count:lowerLimit,upperLimit` 	| Matches Tweets from users that have a number of followers that fall within the specified range. The upper bound is optional and both limits are inclusive. 	| `followers_count:500` 	|
| `friends_count:lowerLimit,upperLimit` 	| Matches Tweets from users that follow a number of users that fall within the specified range. The upper bound is optional and both limits are inclusive. 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| Matches Tweets from users with the preferredUsername *twitterHandle*. Must not contain the &#64; symbol. 	| `from:alexlang11` 	|
| `has:children` 	| Matches Tweets from users that have children. 	| `has:children` 	|
| `is:married` 	| Matches Tweets from users that are married. 	| `is:married` 	|
| `is:verified` 	| Matches Tweets where the author has been verified by Twitter. 	| `analytics is:verified` 	|
| `lang:language-code` 	| Matches Tweets from a particular language. The list of supported language codes is: <ul><li>`ar` (Arabic)</li><li>`zh` (Chinese)</li><li>`da` (Danish)</li><li>`dl` (Dutch)</li><li>`en` (English)</li><li>`fi` (Finnish)</li><li>`fr` (French)</li><li>`de` (German)</li><li>`el` (Greek)</li><li>`he` (Hebrew)</li><li>`id` (Indonesian)</li><li>`it` (Italian)</li><li>`ja` (Japanese)</li><li>`ko` (Korean)</li><li>`no` (Norwegian)</li><li>`fa` (Persian)</li><li>`pl` (Polish)</li><li>`pt` (Portuguese)</li><li>`ru` (Russian)</li><li>`es` (Spanish)</li><li>`sv` (Swedish)</li><li>`th` (Thai)</li><li>`tr` (Turkish)</li><li>`uk` (Ukrainian)</li></ul>    | `lang:de` (to match German Tweets) 	|
| `listed_count:lowerLimit,upperLimit` 	| Matches Tweets where Twitter's listing of the author falls within the specified range. The upper bound is optional and both limits are inclusive. 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| Matches Tweets from a geographical region, specified by its longitude and latitude coordinates and a radius. </br></br>All coordinates are represented in decimal degrees. The `longitude` must be a value between -180 and +180, while `latitude` must be a value between -90 and +90. Specifying a value outside the supported ranges returns an error. Values must be entered as floating-point numbers; integers are not supported. </br></br>The radius of the surrounding area must be specified in miles (mi) or kilometers (km). 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| Matches Tweets that have been posted at or after "startTime". The "endTime" is optional and both limits are inclusive. Timestamps must be in one of the following formats:  </br>```yyyy-mm-dd yyyy-mm-ddTHH:MM:SSZ``` </br>  Timezone is based on UTC (Coordinated Universal Time). When specifying hours, minutes, and seconds, the time must be enclosed by "T" and "Z", as in the prescribed format. 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| Matches Tweets with a particular sentiment. Supported values are: </br><dl>positive</dl> <dlentry>Tweet contains more positive than negative sentiment phrases.</dlentry> </br></br><dl>negative</dl> <dlentry>Tweet contains more negative than positive sentiment phrases.</dlentry>  </br></br><dl>neutral</dl>  <dlentry>Tweet does not contain any sentiment, or is in a language that does not offer sentiment detection.</dlentry> </br></br><dl>ambivalent</dl>  <dlentry>Tweet contains an equal amount of positive and negative sentiment phrases.</dlentry> 	| `sentiment:positive` 	|
| `statuses_count:lowerLimit,upperLimit` 	| Matches Tweets from users that have posted a number of statuses that falls within the specified range. The upper bound is optional and both limits are inclusive. 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| Matches Tweets from users whose profile settings match the specified time zone. 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| Matches Tweets from users whose profile settings match the specified city. 	| `time_zone:"Dublin"` 	|
*Table 2. Query terms*

All supported query terms can be combined with the above Boolean operators. For example,

```ibm -apple followers_count:500```
