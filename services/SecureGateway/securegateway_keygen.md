---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-25"

---
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cert/Key Management

## Generating a self-signed certifiate/key pair

To generate a self-signed certificate/key pair, run the following command:

```
openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout serverKey.pem -out serverCert.pem
```
{: pre}


## Uploading a cert/key pair to the browser

To access a destination enforcing mutual authentication, you must convert your cert/key pair to a PKCS#12 file and upload it to your browser.

To create the PKCS#12 file, use the following command:

```
openssl pkcs12 -export -in <path_to_cert> -inkey <path_to_key> -name "my-sg-pair" -out <path_to_write_to>.p12
```
{: pre}

In Firefox, the .p12 file can be uploaded to Options > Preferences > Advanced > Certificates > View Certificates > Your Certificates > Import

In Chrome, the .p12 file can be uploaded to Settings > HTTPS/SSL > Manage certificates > Import

In Internet Explorer, the .p12 file can be uploaded to Settings > Content > Certificates > Import
