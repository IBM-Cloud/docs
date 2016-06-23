---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Using the mobile app
{: #iot4e_using_mobile}
*Last updated: 14 Jun 2016*
{: .last-updated}

Get started with the {{site.data.keyword.iotelectronics_full}} mobile app to see how you can receive alerts, send commands, and check the status of your connected appliances.
{:shortdesc}

Complete the following tasks:
1. [Download the mobile app](#iot4e_downloadmobile).
2. [Configure {{site.data.keyword.amafull}}](#iot4e_configureMCA).
3. [Connect your mobile device to the {{site.data.keyword.iotelectronics}} environment](#iot4e_connecting_mobile).
4. [Register and control an appliance on your mobile device](#iot4e_adding_appliance).


 ## Downloading the mobile app
 {: #iot4e_downloadmobile}
 To get the mobile app, download and install it on your phone from the Apple App store.  On your phone, open the App store and search for "ibm iot". Choose **IBM IoT for Electronics** and install.

 Alternatively, you can install it to your phone by using [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8).

## Configuring {{site.data.keyword.amashort}}
{: #iot4e_configureMCA}

Before you can connect the mobile app, you must configure {{site.data.keyword.amafull}}.  

  1. On the **Connections** tab in your {{site.data.keyword.iotelectronics}}, open the {{site.data.keyword.amashort}} application. (You can also access the application from your {{site.data.keyword.Bluemix_notm}} dashboard.)  

    ![How to find {{site.data.keyword.amashort}}.](images/IoT4E_Connections.svg "{{site.data.keyword.iotelectronics}} connections")

  2. In the **Custom** section, click **Configure**.

   ![Configure {{site.data.keyword.amashort}}.](images/MCA_config_pg.svg "{{site.data.keyword.amashort}} Set Up Authentication page")  

  3. Enter the following authentication credentials:
    - **Realm name**: Enter **myRealm**.
    - **URL**: Enter the URL to identify your {{site.data.keyword.iotelectronics}} starter app in the following format: **https://<*myIoT4eStarterApp*>.mybluemix.net**  

      **Tip:** Be sure to use the secure `https://` prefix in the URL. You can find the URL of your starter app by clicking **Mobile options**.

  ![{{site.data.keyword.amashort}} Custom Authentication entry.](images/MCA_config_pg2.svg "{{site.data.keyword.amashort}} Custom Authentication entry")  

  4. Save.

## Connecting the mobile app to your {{site.data.keyword.iotelectronics}} environment
{: #iot4e_connecting_mobile}

To view your simulated devices on your mobile app, you must connect the mobile app to your {{site.data.keyword.iotelectronics}} Bluemix environment.

To connect the mobile app, follow these steps:

  1. On your computer, start your {{site.data.keyword.iotelectronics}} application and click **View App** to display the starter app.  

  ![{{site.data.keyword.iotelectronics}}  Getting Started page with View App highlighted.](images/IoT4E_getting_started.svg "{{site.data.keyword.iotelectronics}} Getting Started page with View App")  
  2. Select **Remotely control your connected appliances**.

  ![Select the  {{site.data.keyword.iotelectronics}} Consumer app experience.](images/IoT4E_consumer_app.svg "{{site.data.keyword.iotelectronics}} Consumer app experience")

  3. Create one or more washers. The mobile app cannot connect until a washer is created.

  4.	Scroll to the Connection QR code and scan it using your mobile device. The Connection QR code is located in the section labeled `To connect the app to the environment, you'll be asked to scan this QR Code`.

  ![Scan the  {{site.data.keyword.iotelectronics}} Connection QR code.](images/iot4e_mobile_connect_QR.svg "{{site.data.keyword.iotelectronics}} Connection QR code")

  5. Enter login credentials. Your user ID and password can be any length. Remember your login credentials for future sessions.  

## Registering and controlling an appliance on your mobile device
{: #iot4e_adding_appliance}

To view appliance status and receive notifications, you must register the appliance using your mobile app.

To register an appliance, complete the following steps:

  1. On your computer, scroll to a simulated washer and click it to display its data and Appliance QR code.

  ![Select a washer.](images/IoT4E_mobile_washer_QR.svg "Select a washer.")

  2.	Use your mobile device to scan the QR code of the washer to register the washer on your mobile phone. You will see the washer status on your mobile phone.

  3. On your computer, select a problem with the washer, such as Board Failure or Strong Vibration.  The problem sends an alert to your mobile phone.
