---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Troubleshooting for {{site.data.keyword.mqa}} 
{: #tsmqa}
Here are the answers to several common questions about using {{site.data.keyword.mqa}}. 
{:shortdesc}

## JavaScript hybrid build fails
{: #ts_js_build_fail}

Your JavaScript hybrid {{site.data.keyword.mqa}} application build fails, even though the JavaScript&tm; hybrid SDK for IBM MobileFirst Platform Foundation component is in the app, and the required code is added.


When you try to run your {{site.data.keyword.mqa}} application build, the build fails. 
{: tsSymptoms notoc} 


1. The Android and iOS platform-specific hybrid SDK components are not installed in the project.
2. The Android and iOS platform-specific hybrid SDK components that are installed are not compatible with the installed JavaScript SDK component.
3. The native Android SDK, native iOS SDK, or both, are installed, but the Android and iOS platform-specific hybrid SDK components are not installed.
{: tsCauses notoc} 
 

Some suggestions for resolving this problem include the following steps:
{: tsResolve notoc}
  1.  Ensure that you installed all of the required Android and iOS platform-specific hybrid SDK components and each required native Android SDK or native iOS SDK for the platforms that your app supports. 
  2. Ensure that your Android and iOS platform-specific hybrid SDK components are the same major version number as the JavaScript component, or higher, up to the next major version. The following table contains examples:
  
| JavaScript component version | Platform-specific component version | Compatible? |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | Yes |
| 1.2.3 | 1.2.1 | No |
| 1.2.3 | 1.3.2 | Yes |
| 1.2.3 | 2.0.0 | No |

  3. Ensure that you installed the Android and iOS platform-specific hybrid SDK components. While the native Android SDK and native iOS SDK are required if your app runs on those platforms, the hybrid applications must also have the Android and iOS platform-specific hybrid SDK components installed for each platform.

  
## Cannot open sentiment analysis or distribute test apps
{: #ts_sent_fail}

You cannot open sentiment analysis or distribute your test app.

You cannot open sentiment analysis or distribute your test app because your browser is blocking pop-up windows.
{: tsSymptoms notoc} 

Mobile Quality Assurance uses pop-up windows and cookies to communicate with the Mobile Quality Assurance server.
{: tsCauses notoc}


To establish communication between Mobile Quality Assurance and the Mobile Quality Assurance server, you might need to configure your browser settings to allow pop-up windows and cookies. For example, when you click an option from the user interface, such as the Sentiment Score, Mobile Quality Assurance might be prevented from communicating with the server. Sentiment analysis cannot be displayed if pop-up windows and cookies are blocked. For more information about how to configure your browser settings, see the documentation for your specific browser. 
{: tsResolve notoc}


## Cannot run expired application
{: #ts_app_expired}

You cannot run your Mobile Quality Assurance application.

When you try to run your Mobile Quality Assurance application, you see the following message: Your application has expired and cannot be run at this time.
{: tsSymptoms notoc} 

Your application is marked as disabled in the Mobile Quality Assurance Builds page.
{: tsCauses notoc}


Check the Mobile Quality Assurance Builds page to ensure that none of the applications are marked as disabled. Typically, applications are marked as disabled to inform testers (through the application itself) to not use a specific version of the build. For more information about the settings in the Mobile Quality Assurance Builds page, see Managing builds in IBM Knowledge Center. 
{: tsResolve notoc}

