---

copyright:
  years: 2017
lastupdated: "2017-03-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.hisinstranalshort}} 
{: #getting_started_hisinstranalshort}

The {{site.data.keyword.hisinstranalshort}} service leverages IBM Algorithmics' sophisticated financial models to price and evaluate securities for historical dates.
{:shortdesc}

With thirty years of financial engineering expertise, IBM Algorithmics' pricing models are trusted by the world's largest financial institutions to meet their risk, performance, and regulatory needs.

The {{site.data.keyword.hisinstranalshort}}s service supports the historical computation of the theoretical or market calibrated valuation, and all relevant associated analytics, for investment securities such as equities, fixed income, and derivatives. 

Use this service for building back-testing, performance attribution calculations, and end of month/quarter historical reporting.

## Before you begin

The following steps show you how to obtain access to the {{site.data.keyword.hisinstranalshort}} service and invoke API methods. To use the {{site.data.keyword.hisinstranalshort}} REST API, it is important that you understand the basics of RESTful web services and JSON representations.

You must install cURL before you can use the service.

## Step 1: Create an application and bind it to the service

1. Create an application that binds to the service instance.
2. Review the service instance access credentials, similar to the following example:
```
{
  "accessToken": "<api-key>",
  "uri": "<service-url>"
}
```

## Step 2: Getting the value of an instrument for an earlier date

To use the following example, replace api-key with your service key and service-url with the URL for your service.

```
curl -X GET -H "X-IBM-Access-Token: <api-key>” “<service-url>/api/v1/historical/instrument/<id-of-instrument>?date=2017-01-01”
```

{:codeblock}

The following is an example of a response to a successful request:

```
[
  {
    "instrument": “<id-of-instrument>",
    "scenario": “Base Scenario",
    "values": [
      {
        "THEO/Price": "100 USD",
        "date": "2017/01/01"
      }
    ]
  }
]
```

Example using `POST`. Using `POST` is preferred if you are requesting a large number of analytics, or if there are commas within the analytic names.

```
curl -X POST -H "X-IBM-Access-Token: <api-key>” -d '{"analytics":["THEO/Value","THEO/Price", "THEO/Effective Duration"]}' “<service-url>/api/v1/historical/instrument/<id-of-instrument>?date=2017-01-01”
```

{:codeblock}

The following is an example of a response to a successful request:

```
[
  {
    "instrument": “<id-of-instrument>",
    "scenario": "Base Scenario",
    "values": [
      {
        "THEO/Effective Duration": "6.6194 T",
        "THEO/Price": "101.9994 USD",
        "THEO/Value": "103.3580 USD",
        "date": "2017/01/01"
      }
    ]
  }
]
```

A list of instruments is available [here](http://public.dhe.ibm.com/software/analytics/solutions/en/fintech/Sample_Instrument_Universe.xlsx).

The following table contains `Field Name` values that you can pass to the API for the measures, and the asset classes (Fixed Income, Equity, or Derivative) that they apply to:

|Measure Name|Field Name|Fixed Income|Equity|Derivatives|
|------------|----------|------------|------|-----------|
|Accrued Interest|THEO/Accrued Interest|X| | |
|Clean Value|THEO/Price|X|X|X|
|Dirty Value|THEO/Value|X|X|X|
|Exposure|THEO/Exposure|X|X|X|
|Yield|THEO/Yield|X| | |
|Macaulay Duration|THEO/Macaulay Duration|X| |X|
|Adjusted Duration|THEO/Adjusted Duration|X| |X|
|Effective Duration|THEO/Effective Duration|X| |X|
|Spread Duration|THEO/Adjusted Duration2|X| |X|
|Effective Convexity|THEO/Effective Convexity|X| |X|
|Delta|THEO/Delta| | |X|
|Domestic Rho|THEO/Domestic Rho| | |X|
|Gamma|THEO/Gamma| | |X|
|Theta|THEO/Theta| | |X|
|Vega|THEO/Vega| | |X|
|P&L|POS/Unrealized Profit and Loss Theoretical|X|X|X|
|Return|Theo/Value@REL(scen&time,%diff)|X|X|X|
{: caption="Table 1. {{site.data.keyword.hisinstranalshort}} field name values" caption-side="top"}
