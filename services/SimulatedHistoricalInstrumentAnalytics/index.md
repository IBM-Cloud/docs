---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.simhistinstruanalshort}} 
{: #getting_started_simhistinstruanalshort}

The {{site.data.keyword.simhistinstruanalshort}} service leverages IBM Algorithmics' sophisticated financial models to price and compute analytics on securities for a historical date, under a given scenario.
{:shortdesc}

With thirty years of financial engineering expertise, IBM Algorithmics' pricing models are trusted by the world's largest financial institutions to meet their risk, performance, and regulatory needs.

The {{site.data.keyword.simhistinstruanalshort}} service supports the historical computation of the theoretical or market calibrated valuation, and all relevant associated analytics, for investment securities such as equities, fixed income, and derivatives over an alternate set of market conditions.

## Before you begin

The following steps show you how to obtain access to the {{site.data.keyword.simhistinstruanalshort}} service and invoke API methods. To use the {{site.data.keyword.simhistinstruanalshort}} REST API, it is important that you understand the basics of RESTful web services and JSON representations.

You must install cURL before you can use the service.

## Step 1: Create an application and bind it to the service

1. Create an application that binds to the service instance.
2. Review the service instance access credentials, similar to the following example:
```
{
  "accessToken": "<api-key>",
  "uri": "https://fss-analytics.mybluemix.net/"
}
```

## Step 2: Get the value of an instrument for an earlier date under a given scenario

To use the following example, replace api-key with your service key, the service-url with the URL for your service, and your scenario file.

```
curl -X POST -H "X-IBM-Access-Token: <api-key>" -H "EncType: multipart/form-data" -F "scenario_file=@<location-of-scenario-file>" "<service-url>
/api/v1/scenario/historical/instrument/<name-of-instrument>?date=2017-01-01”
```

{:codeblock}

The following is an example of a response to a successful request:

```
[
  {
    "instrument": “<name-of-instrument>",
    "scenario": “Base Scenario",
    "values": [
      {
        "THEO/Price": "100 USD",
        "date": "2017/01/01"
      }
    ]
  },
  {
    "instrument": “<name-of-instrument>",
    "scenario": “New Scenario",
    "values": [
      {
        "THEO/Price": "110 USD",
        "date": "2017/01/01"
      }
    ]
  }
]
```

### Example scenario files

[curve_shifts_sample.csv](http://public.dhe.ibm.com/software/analytics/solutions/en/fintech/curve_shifts_sample.csv) is a scenario sample file representing different interest rate curve movements with both parallel and non-parallel shifts.

[stresstests_sample.csv](http://public.dhe.ibm.com/software/analytics/solutions/en/fintech/stresstests_sample.csv) is a scenario sample file representing a hypothetical flight to quality, whereby treasury curves fall, swap rates rise, and equities drop 10%.

### Instruments

A list of instruments is available [here](http://public.dhe.ibm.com/software/analytics/solutions/en/fintech/Sample_Instrument_Universe.xlsx).

### Field Name values

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
{: caption="Table 1. {{site.data.keyword.simhistinstruanalshort}} field name values" caption-side="top"}
