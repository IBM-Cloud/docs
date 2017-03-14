---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Getting started with {{site.data.keyword.investportshort}} (Experimental)
{: #getting_started_investportshort}

The {{site.data.keyword.investportshort}} service lets you store, update, and query your investment portfolios and associated holdings using flexible object definitions so you can store more information without worrying about format. With outstanding performance, flexible storage, filtering, and data retrieval, you can make informed and timely investment decisions quickly.
{:shortdesc}

After you create an application that binds to the service instance, use the service access credentials you get to make calls to the API. The service access credentials are similar to the following example:

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
For information about the API, see the [{{site.data.keyword.investportshort}} API Reference](https://console.ng.bluemix.net/apidocs/751).
