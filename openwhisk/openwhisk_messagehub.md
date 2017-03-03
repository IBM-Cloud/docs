---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Using the Message Hub package
{: #openwhisk_catalog_message_hub}

This package allows you to communicate with [Message Hub](https://developer.ibm.com/messaging/message-hub) instances for publishing an consuming messages using native high performance Kafka API.
{: shortdesc}

## Creating a Trigger that listens to an IBM MessageHub instance
{: #openwhisk_catalog_message_hub_trigger}

In order to create a trigger that reacts when messages are posted to a Message Hub instance, you need to use the feed named `/messaging/messageHubFeed`. This feed action supports the following parameters:

|Name|Type|Description|
|---|---|---|
|kafka_brokers_sasl|JSON Array of Strings|This parameter is an array of `<host>:<port>` strings which comprise the brokers in your Message Hub instance|
|user|String|Your Message Hub user name|
|password|String|Your Message Hub password|
|topic|String|The topic you would like the trigger to listen to|
|kafka_admin_url|URL String|The URL of the Message Hub admin REST interface|
|isJSONData|Boolean (Optional - default=false)|When set to `true` this will cause the provider to attempt to parse the message value as JSON before passing it along as the trigger payload.|
|isBinaryKey|Boolean (Optional - default=false)|When set to `true` this will cause the provider to encode the key value as Base64 before passing it along as the trigger payload.|
|isBinaryValue|Boolean (Optional - default=false)|When set to `true` this will cause the provider to encode the message value as Base64 before passing it along as the trigger payload.|

While this list of parameters may seem daunting, they can be automatically set for you by using the package refresh CLI command:

1. Create an instance of Message Hub service under your current organization and space that you are using for OpenWhisk.

2. Verify that the the topic you want to listen to already exists in Message Hub or create a new topic, for example `mytopic`.

3. Refresh the packages in your namespace. The refresh automatically creates a package binding for the Message Hub service instance that you created.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```

  Your package binding now contains the credentials associated with your Message Hub instance.

4. Now all you need to do is create a Trigger that will be fired when new messages are posted to your Message Hub topic.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Setting up a Message Hub package outside Bluemix

If you want to set up your Message Hub outside of Bluemix, you must manually create a package binding for your Message Hub service. You need the Message Hub service credentials and connection information.

1. Create a package binding that is configured for your Message Hub service.

  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  {: pre}

2. Now you can create a Trigger using your new package that will be fired when new messages are posted to your Message Hub topic.

  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}


## Listening for messages
{: #openwhisk_catalog_message_hub_listen}

After creating a trigger, the system will monitor the specified topic in your messaging service. When new messages are posted, the trigger will be fired.

The payload of that trigger will contain a `messages` field which is an array of messages that have been posted since the last time your trigger fired. Each message object in the array will contain the following fields:
- topic
- partition
- offset
- key
- value

In Kafka terms, these fields should be self-evident. However, `key` has an optional feature `isBinaryKey` that allows the `key` to transmit binary data. Additionally, the `value` requires special consideration. Optional fields `isJSONData` and `isBinaryValue` are available to handle JSON and binary messages. These fields, `isJSONData` and `isBinaryValue`, cannot be used in conjunction with each other.

As an example, if `isBinaryKey` was set to `true` when the trigger was created, the `key` will be encoded as a Base64 string when returned from they payload of a fired trigger.

For example, if a `key` of `Some key` is posted with `isBinaryKey` set to `true`, the trigger payload will resemble the below:

```json
{
    "messages": [
        {
            "partition": 0,
            "key": "U29tZSBrZXk=",
            "offset": 421760,
            "topic": "mytopic",
            "value": "Some value"
        }
    ]
}
```

If the `isJSONData` parameter was set to `false` (or not set at all) when the trigger was created, the `value` field will be the raw value of the posted message. However, if `isJSONData` was set to `true` when the trigger was created, the system will attempt to parse this value as a JSON object, on a best-effort basis. If parsing is successful, then the `value` in the trigger payload will be the resulting JSON object.

For example, if a message of `{"title": "Some string", "amount": 5, "isAwesome": true}` is posted with `isJSONData` set to `true`, the trigger payload might look something like this:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": {
          "amount": 5,
          "isAwesome": true,
          "title": "Some string"
      }
    }
  ]
}
```

However, if the same message content is posted with `isJSONData` set to `false`, the trigger payload would look like this:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

Similar to `isJSONData`, if `isBinaryValue` was set to `true` during trigger creation, the resultant `value` in the trigger payload will be encoded as a Base64 string.

For example, if a `value` of `Some data` is posted with `isBinaryValue` set to `true`, the trigger payload might look something like this:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "U29tZSBkYXRh"
    }
  ]
}
```

If the same message is posted without `isBinaryData` set to `true`, the trigger payload would resemble the below example:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "Some data"
    }
  ]
}
```

### Messages are batched
You will notice that the trigger payload contains an array of messages. This means that if you are producing messages to your messaging system very quickly, the feed will attempt to batch up the posted messages into a single firing of your trigger. This allows the messages to be posted to your trigger more rapidly and efficiently.

Please keep in mind when coding actions that are fired by your trigger, that the number of messages in the payload is technically unbounded, but will always be greater than 0. Here is an example of a batched message (please note the change in the *offset* value):
 
 ```json
 {
   "messages": [
       {
         "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```

## Producing messages to Message Hub
If you would like to use an OpenWhisk action to conveniently produce a message to Message Hub, you can use the `/messaging/messageHubProduce` action. This action takes the following parameters:

|Name|Type|Description|
|---|---|---|
|kafka_brokers_sasl|JSON Array of Strings|This parameter is an array of `<host>:<port>` strings which comprise the brokers in your Message Hub instance|
|user|String|Your Message Hub user name|
|password|String|Your Message Hub password|
|topic|String|The topic you would like the trigger to listen to|
|value|String|The value for the message you would like to produce|
|key|String (Optional)|The key for the message you would like to produce|

While the first three parameters can be automatically bound by using `wsk package refresh`, here is an example of invoking the action with all required parameters:

```
wsk action invoke /messaging/messageHubProduce -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p value "This is the content of my message"
```
{: pre}

## Examples

### Integrating OpenWhisk with IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage, and IBM Data Science Experience
Example that integrates OpenWhisk with IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage, IBM Data Science Experience (Spark) service can be [found here](https://medium.com/openwhisk/transit-flexible-pipeline-for-iot-data-with-bluemix-and-openwhisk-4824cf20f1e0).

## References
- [IBM Message Hub](https://developer.ibm.com/messaging/message-hub/)
- [Apache Kafka](https://kafka.apache.org/)
