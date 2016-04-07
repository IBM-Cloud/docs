---

copyright:
 years: 2015, 2016

---

# Installing the Cordova Push plug-in
{: #cordova_install}

Install and use the client Push plug-in to further develop your Cordova applications. This also installs the Cordova Core plug-in, which initializes your connection to Bluemix.

### Before you begin

1. Download the latest Android Studio SDK and Xcode versions.
1. Set up your emulator. For Android Studio, use an emulator that supports Google Play API.
1. Install the Git command-line tool. For Windows, make sure you select the **Run Git from the Window Command Prompt** option. For information about how to download and install this tool, see [Git](https://git-scm.com/downloads).

1. Install the Node.js and Node Package Manager (NPM) tool. The NPM command-line tool is bundled with Node.js. For information about how to download and install Node.js, see [Node.js](https://nodejs.org/en/download/).
1. From the command line, install the Cordova command-line tools by using the **npm install -g cordova** command. This is required to use the Cordova Push plug-in. For information about how to install Cordova and set up your Cordova app, see [Cordova Apache](https://cordova.apache.org/#getstarted).

	**Note**: To view the Cordova Push plug-in readme file, go to [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)


## Installing the Cordova Push plug-in
1. Change to the folder that you want to create your Cordova app in and run the following command to create a Cordova application. If you have an existing Cordova app, go to step 3.


	cordova create your_app_name
	cd your_app_name
	```
1. Optional: (Optional) Edit the **config.xml** file and change the application name in the <name> element to one that you choose, rather than the default HelloCordova name.

	**Note**: Make sure you specify the correct Bundle ID. If you do not, the following error messages are displayed in Xcode.
	* The executable was signed with invalid entitlements.
	* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile.

	To fix this issue, specify the correct Bundle ID in Xcode or in your Cordova app **config.xml**  file.

1. Add the minimum supported API or the deployment target declaration to the config.xml file for your Cordova application. The minSdkVersion value must be higher than 15. The targetSdkVersion value must always reflect the latest Android SDK that is available from Google.
	* **Android** - With your editor, open the config.xml file and update the
```<platform name="android">``` element with minimum and target SDK versions:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - Update the <platform name="ios"> element with a deployment target declaration:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. From the Cordova command-line interface (CLI), add your platforms: iOS, Android, or both by using the following commands.

	```
	cordova platform add ios
	cordova platform add android
	```
1. From your Cordova application root directory, enter the following command to install the Cordova Push plug-in: **cordova plugin add ibm-mfp-push**.

	Depending on the platforms that you added, you see something similar to the following:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. From *your-app-root-folder*, verify that the Cordova Core and Push plug-in were installed successfully by using the following command: **cordova plugin list**.

	Depending on the platforms that you added, you see something similar to the following:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (iOS only) - Configure your iOS development environment.
	a. Open your your-app-name.xcodeproj file in *your-app-name***/platforms/ios** directory with Xcode.

	b. Add the Bridging Header. Go to **Build settings > Swift Compiler - Code Generation > Objective-C Bridging Header** and add the following path: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. Add the Frameworks parameter. Go to **Build Settings > Linking > Runpath Search Paths** and add the following parameter:
	```
	@executable_path/Frameworks
	```
	d. Uncomment the following Push import statements in your bridging header. Go to *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Build and run your application with Xcode.
1. (Android only)- Build your Android project by using the following command:
**cordova build android**.

	**Note**: Before opening your project in Android Studio, you must first build your Cordova application through the Cordova CLI. Otherwise, you will encounter build errors.

1. Next step. [Initializing the Cordova plug-in](t_cordova_initalize.html).
