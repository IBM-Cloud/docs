---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Instrumenting MQA with an iOS app (Deprecated)
{: #instrumentios}

To use {{site.data.keyword.mqafull}} with your iOS app, you must download the SDK and instrument it by making some changes using the Xcode development environment.
{: shortdesc}

Before you can instrument an app with {{site.data.keyword.mqa}}, you must have a {{site.data.keyword.Bluemix}} account and the correctly installed version of the development environment for the platforms of the app you that are instrumenting.

To instrument {{site.data.keyword.mqa}} to work with your Objective-C or Swift app, complete the following tasks:

1. Add the required permissions and downloaded SDK to your iOS project.

	1. Create or open your project in Xcode.
	
	2. Add the following Dependency Libraries by selecting `+` in the *Linked Frameworks and Libraries* section of the *General* tab of your Xcode project:

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework
	
	3. Drag the {{site.data.keyword.mqa}} SDK for iOS `Q4M.framework` folder into the **Frameworks** group in the Navigator tree. In the Choose options window, select *Copy items if needed*, **Create groups**, and check the box for your project name as the target.
	
	4. In the Linking section of the *Build Settings* tab, set the *Other Linker flags* for Debug and Release to **-ObjC**. Important: Make sure that the *All* tab is selected so the Other Linker flags are included in the list.
	
	5. *For Objective-C only:* Add the following import statement to the `AppDelegate.m` and `ViewController.m` files:

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}
	
	6. *For Swift only:* Add an Objective-C bridging header for the {{site.data.keyword.mqa}} SDK for iOS by completing the following steps:
	
		1. Right-click the project root node, and select **New File**.
		 
		2. In the Choose Template window under iOS, click the Header File template in the Source section.
		 
		3. Name the file `MyProject-Bridging-Header.h`, where *MyProject* is the name of your Swift project, and select the name of your project as the target. For example, name the file `MyProject-Bridging-Header.h`.
		 
		4. Click **Create** to save the file in the root of your project.
		 
		5. In the new bridging header file, add the following import statement for the bridging header file:

			```
			#import <Q4M/MQALogger.h>
			``` 
			{: codeblock}
				
		6. With your project selected in 
			the Xcode Project Navigator, click **Build Settings**, and search for `Objective-C Bridging Header`.
		 
		7. Under **Swift Compiler - General**, set the value of **Objective-C Bridging Header** to the path of the bridging header. The path is relative to the root of your project. For example, if the project MQASampleApp is at `/user/example/MQASampleApp`, then the path is `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`. If you saved your file in the root of the project, then you can use environment variable to set the path by entering `${SRCROOT}/${PROJECT}-Bridging-Header.h`.
		 
		8. Save and build the app to verify that the path is correct.
	
	7. In the ```info.plist``` file, verify the following settings in your project information:
			
		* Bundle version - {{site.data.keyword.mqa}} uses the value from this field to determine when to send a new build notification to testers. When you upload a new build to {{site.data.keyword.mqa}}, ensure that you increment this number. The string in the Bundle version field is restricted to numbers and the period (.) character. Because this restriction is an Xcode requirement, most applications follow this convention and do not require changes.
		* Bundle versions string - This field contains a string representation of your version number. The string does not have the same restrictions as the Bundle version field.
			
2. Configure a new session to start with each log in.

    1. Locate the `didFinishLaunchingWithOptions` method in your `AppDelegate` file:
	
        * Objective-C: `AppDelegate.m` file
        * Swift: `AppDelegate.swift` file
			 
	2. Start the {{site.data.keyword.mqa}} session.
	
		* Objective-C

			1. Start the new session in a method within your `applicationDelegate` method, such as the `didFinishLaunchingWithOptions` method. You can find your delegate by opening the folder with the same name as your project in the Project Navigator. Look for the `projectDelegate.m` file.
            
			2. Add the following code inside the `didFinishLaunchingWithOptions` method before the line with `return YES;`:

				```
				// Starts a quality assurance session using a 
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. Replace the *Your_Application_Key* variable with your application key from {{site.data.keyword.mqa}}.
               Tip: You can find your app key in the {{site.data.keyword.mqa}} web pane under App Settings.
                    
		* Swift

			1. Locate the ```didFinishLaunchingWithOptions``` method in the `AppDelegate.swift` file.
                    
			2. Add the following code inside the method before the line that reads ```return true```, where *Your_Application_Key* is a valid key for your app:

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. Define whether to use preproduction mode or production mode. For information about the differences between preproduction and production mode, see [Differences between preproduction and production modes ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window} in IBM Knowledge Center.

		* Objective-C
				
			1. Locate the `didFinishLaunchingWithOptions` method.
			
			2. Add one of the following lines of code inside the didFinishLaunchingWithOptions method before the line with `return YES;`:
					 
			To use preproduction mode, add this line of code: 
					   
				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}
					   
			To use production mode, add this line of code: 
					   
				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}
				
				**Objective-C complete example**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Override point for customization after application launch.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Starts a quality assurance session using a placeholder key
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Enables the quality assurance application crash reporting 
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}
                       
        * Swift

			1. In the AppDelegate.swift file, search for the `didFinishLaunchingWithOptions` method.
			
			2. Add the following lines to your `didFinishLaunchingWithOptions` method before the line that reads ```return true```:
			        
				```
				//Set the SDK mode Market vs QA for Production 
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}
			
			An example of the code is: 

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Set the SDK mode Market vs QA for Production 
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
					
				// Override point for customization after 
				   application launch.
				return true
				```
				{: codeblock}
						
				**Swift complete example**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Override point for customization after application launch.
					//Set the Shake Device option to true or false. If this is not explicitly set, the Shake Device is enabled by default. 
					MQALogger.settings().reportOnShakeEnabled = true
					//Set the SDK mode Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Start the MQA session with the specified app key
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Enables MQA crash reporting to catch uncaught exceptions
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}
					  
3. Run your app to make sure that {{site.data.keyword.mqa}} starts when the app starts.
					  
4. Continue with the steps on the [Getting started with {{site.data.keyword.mqa}}](index.html) page.
		
# Related Links
{: #rellinks notoc}

## Related Links
{: #general notoc}
* [Getting started with {{site.data.keyword.mqa}}](index.html){:new_window}
