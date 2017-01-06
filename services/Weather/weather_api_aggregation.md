---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# API aggregation
{: #api_aggregation}

Some {{site.data.keyword.weather_short}} APIs can be aggregated. You can use aggregation to combine two or more atomic API
calls into a single HTTP request.
{: shortdesc}

An atomic API call references any of the APIs that define an alias for aggregation. Each API user
document contains the alias for aggregation name in the URL format section if it is available for
aggregation. For example, the standard daily forecast API has an alias for aggregation of
`v2fcstdaily10` that can be used to retrieve the 10-day daily forecast as part of an aggregated
request.

Aggregation has the following limitations:

* The total uncompressed response size for the complete aggregation must be less than 1
megabyte.
* URLs must be less than approximately 4,096 characters in length (including protocol, hostname,
path, and query string).
* You can aggregate up to 10 atomic APIs.

**Note:** If your request or response violates any of these limitations, you receive an
error response with a 500 HTTP Status code (typically 500 or 502, although others might be
returned).

## Aggregate API URLs
The aggregate API URL begins with `/v2/aggregate/` and is followed by aliases that
are separated by semi-colons.
For example, to aggregate the 10-day daily forecast API (`v2fcstdaily10`) with
current observations (`v2obscurrent`), use the following form:

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## Query parameter rules for atomic APIs and aggregation
Query parameters are required for all requests. The query parameters for
aggregation are passed the same way as for the atomic API calls with a
few extra rules. The following sections describe how
they can be applied to form different aggregations.

### Specify query parameters that apply to all atomic APIs

The simplest form of aggregation is
when query parameters apply to all atomic APIs. In this case, the query parameters have the standard
format of `?param1=value1&amp;param2=value2`.

The following example applies
`geocode=31.44,84.33&amp;language=en&amp;units=e` to the request for the
`v2fcstdaily10` and the `v2obscurrent` atomic
APIs:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### Specify which atomic APIs receive which query parameters

If you need to specify parameters
for specific atomic APIs, the query parameters can use the positional notation of
`?R1.param1=value1&amp;R2.param2=value2`. This format uses `param1`
for the first atomic API and `param2` for the second atomic API.

The following
example applies `geocode=31.44,84.33&amp;language=en&amp;units=e` to
`v2fcstdaily10` and `geocode=44.44,50.23&amp;language=en&amp;units=e`
to `v2obscurrent`.

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### Group query parameters for specific atomic APIs

You can group parameters by using positional
notation as a comma-separated format of `?R1,R2.param1=value1&amp;param2=value2`.
This format uses `param1` for the first and second atomic APIs and
`param2` for all atomic APIs.

The following example applies `geocode=34.06,84.21&amp;language=enUS&amp;units=e` to `v2fcstdaily10` and
`v2obscurrent`. It applies `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` to
`v2loc`:

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### Request the same resource multiple ways

You can request the same resource multiple ways, such
as in different languages or with different unit of measure. With this format, the atomic API can be
repeated in the request: `/v2/aggregate/v2fcstdaily10;v2fcstdaily10` and the
parameter's positional notation can be used to indicate which way to request which API:
`?R1.param1=value1&amp;R2.param1=value2`. In this case, the user receives the same
resource that is formatted or translated in different ways.

The following example applies `geocode=31.44,84.33&amp;language=en&amp;units=e` to the first
`v2fcstdaily10` and `geocode=31.44,84.33&amp;language=fr&amp;units=m`
to the second `v2fcstdaily10`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

The following example applies `geocode=31.44,84.33&amp;language=en&amp;units=e` to the
first `v2fcstdaily10` and
`geocode=33.54,85.43&amp;language=en&amp;units=e` to the second
`v2fcstdaily10` to retrieve multiple locations for the same
data:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




