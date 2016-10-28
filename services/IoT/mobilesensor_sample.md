---

copyright:
  years: 2016
lastupdated: "2016-10-19"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Mobile Device Sensor Sample

The mobile device sensor sample uses JavaScript to connect your phone the {{site.data.keyword.iot_full}} and publish sensor data to your {{site.data.keyword.iot_short}} organization.
{:shortdesc}

The {{site.data.keyword.iot_short}} Python client library is used to subscribe to commands and visualize the sensor data that is published by your phone. The data visualization is presented on a website that is built in the Web Server Gateway Interface (WSGI) framework.

This application demonstrates an approach to controlling user's access to sensor data from specific devices. When **Let's Play** is clicked, the application creates a user record in a {{site.data.keyword.cloudantfull}} database, and calls the {{site.data.keyword.iot_short}} device management API to register the device.

## Prerequisites

Before deploying this sample:

- Create a {{site.data.keyword.bluemix_notm}} account and log in. For more information on {{site.data.keyword.bluemix_notm}}, see [Begin your free trial](https://apps.admin.ibmcloud.com/manage/trial/bluemix.html).
- Download and install the Cloud Foundry command-line interface. The Cloud Foundry command-line interface allows you to modify and deploy service instances to {{site.data.keyword.bluemix_notm}}. For more information, see [Start coding with the cf command-line interface](https://www.ng.bluemix.net/docs/#starters/install_cli.html)

## Deploying this sample

To deploy your own copy of this sample in {{site.data.keyword.bluemix_notm}} use the following steps:

1. Create a new Python application in {{site.data.keyword.bluemix_notm}}.
  a. In your {{site.data.keyword.bluemix_notm}} dashboard, click **Create App**, then click **Web**.
  b. Select **Python** and click **Continue**.
  c. Choose an application name and click **Finish**.
  Your Python application is now being staged.
2. Create an instance of the {{site.data.keyword.cloudant_short_notm}} NoSQL DB service.
  a. In your {{site.data.keyword.bluemix_notm}} dashboard, click **Use Services or APIs**.
  b. Select **Data and Analytics** in the menu, and click **Cloudant NoSQL DB**.
  c. Click **Create**.
3. Bind your instance of {{site.data.keyword.cloudant_short_notm}} NoSQL DB and your instance of {{site.data.keyword.iot_short}} to your Python application.
  a. Click **Bind a Service or API**.
  b. Select your {{site.data.keyword.cloudant_short_notm}} NoSQL DB service and your {{site.data.keyword.iot_short}} instance, and click **Add**.
4. Clone the [{{site.data.keyword.iot_short}} Python Github repository](https://github.com/ibm-messaging/iot-python.git). To clone the repository from a command-line interface navigate to the directory which is to be the destination of the repository clone and run the following command:
```
$ git clone https://github.com/ibm-messaging/iot-python.git
```
5. In the command-line interface, change your directory to the mobile device sensor sample by using the following command:
```
$ cd iot-python/samples/bluemixZoneDemo
```
6. Push your application into {{site.data.keyword.bluemix_notm}} by using the following command, replacing `app_name` with the name of your Python application:
```
$ cf push app_name -m 32M -b https://github.com/cloudfoundry/cf-buildpack-python.git -c "python server.py"
```
7. Open `http://app_name.mybluemix.net/` in a web browser on your phone. You should see a page illustrating how

You see a page that illustrates how, using MQTT messaging, the accelerometer data from your
phone is sent to the <keyword conref="cloudoeconrefs.dita#cloudoeconrefs/iot_short"/>, and a
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/bluemix_short"/> app uses this data to mirror
your movements. Enter your device ID, click <uicontrol>Connect</uicontrol>, and then go on, try
moving your phone.
