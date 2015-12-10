{:shortdesc: .shortdesc}

# Nested message schemas

Real-Time Insights supports nested JSON message payloads that meet the IoT Foundation specification.   
{: shortdesc}

## Supported nested message payload format
Nested data points can be used when creating rules, dashboards, and templates.

>**Note:** Real-Time Insights does not support Custom JSON payloads. More information about the IoT Foundation message payload specification is in the [IoT Foundation documentation](https://docs.internetofthings.ibmcloud.com/messaging/payload.html).

The following examples illustrate supported nested message formats:
- Simple data  
```
{
    "d":
    {"msg": "Hello World"}  
}
```

- Complex data
```
{
    "d": {  
      "host": "IBM700-R9E683D",  
      "mem": 54.9,  
      "network":
      {  
        "up": 1.22,  
        "down": 0.55  
      },  
      "cpu": 1.3,  
    }  
}
```  

>**Important:** Nested JSON messages must contain the d element which is where you include all data for the event being transmitted in the message.
- The element is required for your message to meet the IoT Foundation message specification.
- The element must always be a JSON object (not an array)
- In the case where you wish to send no data the d element should still be present, but contain an empty object.
