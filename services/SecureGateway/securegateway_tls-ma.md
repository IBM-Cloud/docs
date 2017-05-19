---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Node.js TLS Mutual Authentication

This sample will go over how to configure Mutual Authentication for both sides of an on-premises destination: User Authentication and Resource Authentication.

I know that the resource I want to connect to will be hosted on the same machine as the Secure Gateway Client, it will be listening on port 8999, and that it requires mutual authentication to allow a connection.  With this information, I can begin creating my destination.

![Initial TLS Mutual Authentication](./images/tlsMA.png?raw=true "Initial TLS Mutual Authentication")

## User Authentication
I'm creating a brand new application, so I don't have any pre-existing certificate/key pairs for my application to use, so I will have the Secure Gateway servers automatically generate a pair for me.  To do this, I just have to leave the User Authentication upload field empty.  If I already had a pair that my application would be using, I would upload my certificate into this field, instead.

## Resource Authentication

### On-Premises Authentication
In order for the Secure Gateway Client to authenticate the resource it is connecting to, I have to provide the client with the certificate (or certificate chain) that the resource will be presenting.  My resource doesn't have a full certificate chain, so I just need to upload its certificate to the On-Premises Authentication field.  This field accepts up to 6 separate certificate files (.pem, .cer, .der, .crt).

### Client Certificate and Key
If I need to specify how the Secure Gateway Client will identify itself to my resource, I can upload a certificate and key here for the Client to use.  Because the Client and the resource are running on the same machine, I can leave these empty and have the Secure Gateway servers automatically generate a pair for me.  If my resource was on a separate host, I would need to [generate a cert/key pair to upload](./securegateway_keygen.html).

![Local TLS Mutual Authentication](./images/localTLSma.png?raw=true "Local TLS Mutual Authentication")

When I create this destination, the Secure Gateway servers will automatically generate a cert/key pair for my application to use as well as a pair for the Secure Gateway Client to use when connecting to my local resource.  The destination will also have the certificate of my local resource to provide to the Secure Gateway Client for use in the CA during the connection.  After creation, I can edit my destination to see the following information:

![Local TLS Mutual Authentication Details](./images/editLocalTLSma.png?raw=true "Local TLS Mutual Authentication Details")

## Downloading the Security Files
From the destination info panel of my destination, there is a link to download a .zip file containing all the certificates and keys associated with my destination:

![Mutual Authentication Info Panel](./images/infoPanelMA.png?raw=true "Mutual Authentication Info Panel")

After downloading the .zip and extracting the files, I now have the following:

File Name | Purpose
-- | --
secureGatewayCert.pem | Primary certificate of the Secure Gateway server
DigiCertCA2.pem | Intermediate certificate of the Secure Gateway server
DigiCertTrustedRoot.pem | Root certificate of the Secure Gateway server
Nn5TJ34LyVQ_i2NOT_cert.pem | Auto-generated certificate to be used by my application when connecting to the cloud host and port
Nn5TJ34LyVQ_i2NOT_key.pem | Auto-generated key to be used by my application when connecting to the cloud host and port
Nn5TJ34LyVQ_i2NOT_destCert.pem | Auto-generated certificate for the SG Client to use when connecting to the destination
Nn5TJ34LyVQ_i2NOT_destKey.pem | Auto-generated key for the SG Client to use when connecting to the destination
Nn5TJ34LyVQ_clientCert.pem | Auto-generated certificate from your gateway for the SG Client to use in the event it does not have a `_destCert` or `_destKey` file
localServerCert.pem | The certificate of my local resource to be used in the CA of the Secure Gateway Client

## Creating the Application
Now that I have my cloud host and port for my destination as well as the various certificates and keys, I can begin writing my application to connect to Secure Gateway.  This is a simple Node.js application that will connect to my local TLS server, receive a small amount of data, and then close the connection.

```javascript
let fs = require('fs');
let tls = require('tls');

let client_opts = {
    cert : fs.readFileSync('Nn5TJ34LyVQ_i2NOT_cert.pem'),
    key : fs.readFileSync('Nn5TJ34LyVQ_i2NOT_key.pem'),
    host : 'cap-sg-prd-1.integration.ibmcloud.com',
    port : 17996,
    rejectUnauthorized : true
}

let so = tls.connect(client_opts, function() {
    console.log('Client connected, authorized:', so.authorized);
    if (!so.authorized) console.log('Client authorization error:', so.authorizationError)
});

so.on('data', function(data) {
    console.log('Client data:', data.toString())
});

so.on('error', function(err) {
    console.log('Client error',err);
});

so.on('close', function() {
    console.log('Client connection closing');
});
```
{: codeblock}

## Creating the TLS Server
I have my local TLS server which is a simple Node.js application that will listen for connections, write a message on a successful connection, and then close that connection.

```javascript
let fs = require('fs');
let tls = require('tls');

let server_opts = {
    cert : fs.readFileSync('localServerCert.pem'),
    key : fs.readFileSync('localServerKey.pem'),
    // pfx : fs.readFileSync(''),
    // passphrase : '',
    ca : [fs.readFileSync('Nn5TJ34LyVQ_i2NOT_destCert.pem')],
    rejectUnauthorized : true,
    requestCert : true
}

// Create the local TLS Server with the settings defined above
let server = tls.createServer(server_opts, function(socket) {
    socket.write('Successful connection message from the server');
    socket.end();
});

// Set up the various event listeners for the server and log their output
server.on('error', function(err) {
    console.log('Server error', err);
});

server.on('close', function() {
    console.log('Server closing');
});

server.on('tlsClientError', function(err) {
    console.log('Server tlsClientError', err);
});

server.listen(8999);
```
{: codeblock}

## Update the Client Access Control List
Before testing my application, I need to make sure the ACL on my Client is configured appropriately.  I have added `localhost:8999` to my ACL:

```
--------------------------------------------------------------------
           -- Secure Gateway Client Access Control List --

 Connections to unlisted rules are currently: denied

 hostname:port                path           value
 localhost:8999                            Allow
--------------------------------------------------------------------
```
{: screen}

## Testing the connection
Now that my application, my local server, and my Client have all been configured, I get the following output from my application and my Client:

### Application

```
Client connected, authorized: true
Client data: Successful connection message from the server
Client connection closing
```
{: screen}

### Secure Gateway Client

```
[2017-04-07 12:22:42.363] [INFO] (Client ID Nn5TJ34LyVQ_qCB) Connection #1 is being established to localhost:8999
[2017-04-07 12:22:42.381] [INFO] (Client ID Nn5TJ34LyVQ_qCB) Connection #1 to localhost:8999 was closed
```
{: screen}

## Success!
We have successfully configured Mutual Authentication for both User Authentication and Resource Authentication!
