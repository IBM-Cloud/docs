---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Getting started with {{site.data.keyword.investportshort}} (Experimental)
{: #getting_started_investportshort}

The {{site.data.keyword.investportshort}} service lets you store, update, and query your investment portfolios and associated holdings using flexible object definitions so you can store more information without worrying about format. With outstanding performance, flexible storage, filtering, and data retrieval, you can make informed and timely investment decisions quickly.
{:shortdesc}

## Before you begin
The following steps show you how to obtain access to the {{site.data.keyword.investportshort}} service and invoke API methods. To use the {{site.data.keyword.investportshort}} REST API, it is important that you understand the basics of RESTful web services and JSON representations.
Ensure that you have cURL installed because you'll use cURL to call the API in the examples.

## Step 1: Create an application and bind it to the service

1.  Create an application that binds to the service instance.
2.  Review the service instance access credentials, similar to the following example:
```
{
  "fss-portfolio-service": [
    {
      "credentials": {
        "url": "https://investment-portfolio.mybluemix.net/",
        "writer": {
          "userid": "aturearteratentstseenlyr",
          "password": "175256e9b6bff7607640562fd3c6c161bb97b059"
        },
        "reader": {
          "userid": "omptearokilaoresteneirin",
          "password": "3a77c4b5a6ad59db942081f6b7140a9b8c793ef6"
        }
      },
      ...
    }
  ]
}
```
Use the writer credentials when making API calls to either read or make changes to data. If you want to restrict access to read-only, then use the reader credentials.

## Step 2: Creating a portfolio entry

This operation creates a portfolio entry. Values are required for name and timestamp. To use the following example, replace service-user-id and service-user-password with your service credentials and service-url with the URL for your service.

```
curl -X POST -u "{service-user-id}":"{service-user_password}" --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ "name":"P1", "timestamp": "2017-02-24T19:53:56.830Z", "closed": false, "data": { "manager": "Edward Lam" }}' '{service-url}/api/v1/portfolios'
```
{:codeblock}

The following is an example of a response to a successful request:
```
{
  "_rev": "1-49f159ae5996ae96235adb66f4676662"
}
```

## Step 3:  Getting portfolio entries

This operation returns all portfolios from the system that the caller has access to based on the specified parameters. Each portfolio name may have multiple entries with different timestamps. Use the latest parameter to retrieve only the latest entry for each portfolio and use the openOnly parameter to retrieve only open portfolios.

```
curl -X GET -u "{service-user-id}":"{service-user_password}" --header 'Accept: application/json' '{service-url}/api/v1/portfolios'
```
{:codeblock}

The following is an example of a response to a successful request:
```
{
  "portfolios": [
    {
      "name": "P1",
      "timestamp": "2017-02-24T19:53:56.830Z"
    },
    {
      "name": "P1",
      "timestamp": "2017-02-27T13:12:26.014Z"
    },
    {
      "name": "P1",
      "timestamp": "2017-02-27T16:26:26.399Z"
    }
  ]
}
```

## Step 4: Creating holdings for a portfolio entry

This operation creates holdings associated with the specified portfolio entry. Use the portfolioName parameter to specify the portfolio with which to associate the new holdings. An entry for the portfolio must exist with the timestamp specified in the data.

```
curl -X POST -u "{service-user-id}":"{service-user_password}" --header 'Content-Type: application/json' --header 'Accept:application/json' -d '{ "timestamp": "2017-02-24T19:53:56.830Z", "holdings": [ { "asset": "IBM", "quantity": 36}, { "asset": "LNVGY", "quantity": 520 } ] }' '{service-url}/api/v1/portfolios/P1/holdings'
```
{:codeblock}

The following is an example of a response to a successful request:

```
{
  "_rev": "1-62dd790a827bd94fc6d3adeee6c64165"
}
```

## Step 5: Getting holdings for a portfolio

This operation returns holdings associated with the specified portfolio. Use the latest parameter to retrieve only the holdings for the most recent entry for the specified portfolio, the atDate parameter to retrieve holdings on or before the specified timestamp, and the hasKey parameter to retrieve holdings that have the specified keys defined.

```
curl -X GET -u "{service-user-id}":"{service-user_password}" --header 'Accept: application/json' '{service-url}/api/v1/portfolios/P1/holdings'
```
{:codeblock}

The following is an example of a response to a successful request:

```
{
  "holdings": [
    {
      "timestamp": "2017-02-24T19:53:56.830Z",
      "holdings": [
        {
          "asset": "IBM",
          "quantity": 36
        },
        {
          "asset": "LNVGY",
          "quantity": 520
        }
      ],
      "_rev": "1-62dd790a827bd94fc6d3adeee6c64165"
    }
  ]
}

```