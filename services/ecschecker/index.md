# Getting started with Digital Content Checker (Experimental)
*Last Updated: 18 April 2016*

IBM® Digital Content Checker for Bluemix™ provides the ability to automatically
check EPUB and HTML content for accessibility-compliance issues. You can scan
content via two interfaces:
* A web console, which you can access when managing your apps and services in the Bluemix™
  Dashboard. The web console allows you to scan an individual HTML or EPUB file and obtain
  a report.
* A REST API that can be used to integrate checking capabilities into your applications
  and workflows.

The Digital Content Checker provides two rule sets:
* Web Content Accessibility Guidelines v2.0 AA (WCAG 2.0 AA)
* IBM Accessibility Rule Set - Includes all of the rules of the WCAG 2.0 AA set
  and additional rules designed by IBM for new web standards such as ARIA and HTML5.

To add the Digital Content Checker to your space and bind it to an application,
refer to [Adding a service to your application](https://new-console.ng.bluemix.net/docs/manageapps/mngapps.html).

### Using the Digital Content Checker web console

After binding the Digital Content Checker with your application, you will find the web
console in the Services section of your Application's Dashboard. 

Browse for the file you
wish to scan and choose from the provided rule sets on the initial screen. If you submit
an EPUB document, the Digital Content
Checker will provide reports on all of the HTML content within the EPUB
document. If you submit other documents, the Digital Content Checker
will attempt to parse the document as an HTML file and provide the
resulting report. You can filter the report in the web console or
download a CSV file for processing outside of Bluemix™.

### Using the Digital Content Checker REST service

To bind the service to your application and see how to access VCAP_SERVICES,
see [Adding a service to your application](https://new-console.ng.bluemix.net/docs/manageapps/mngapps.html).

VCAP_SERVICES will contain content similar to the following:

```
{
  "ecs-checker": [
    {
      "name": "Digital Content Checker-ss",
      "label": "ecs-checker",
      "plan": "ecs-checker-free",
      "credentials": {
        "userid": "00000000-0000-0000-0000-000000000000",
        "password": "00000000-0000-0000-0000-000000000000",
        "url": "https://ecs-checker.mybluemix.net:443/api",
        "instanceId": "00000000-0000-0000-0000-000000000000"
      }
    }
  ]
}
```
Using these parameters, you can submit content to the checker using one of the POST
interfaces documented in the [REST API](https://ecs-checker.mybluemix.net/docs/swagger_dcc.html).
For example, using Basic authentication with the provided {userid} and {password}, POST an EPUB to 
```
https://ecs-checker.mybluemix.net:443/api/{instanceId}/validate/epub?policies=IBM_DCP080115
```

###Using the Batch Scan Tool

The Batch Scan tool acts as a local scan client that will test static HTML and
EPUB content on your local machine. This tool is intended for use with high
volume, repeated scans of static content, such as might occur with scans
performed during automated documentation builds.


####Installing the Batch Scan Tool

Use the following directions to install the Batch Scan Tool on a Windows
machine.

**Step 1**: Download the install ZIP file
Create a directory (i.e. C:\AccessibilityTools\DCC ) on your local
machine and download the latest Batch Scan tool ZIP file into this directory.

https://ecs-checker.mybluemix.net/priv/dist/dccbatch.zip

**Step 2**: Extract the Batch Scan Tool files from the ZIP file
Extract the ZIP file contents into the C:\AccessibilityTools\DCC
directory.  The ZIP file contains JAR files, a test file, and configuration
files.

**Step 3**: Download a Bluemix configuration file
From the Digital Content Checker console in Bluemix, you will find a link at
the top of the page to "Download Tool Configuration", which will provide you
with a "dashboard-config.json" file that is unique to your Bluemix instance
of the Digital Content Checker. Place this in the Batch Scan Tool directory
(e.g., c:\AccessibilityTools\DCC\BatchScanTool).

**Step 4**: Verify installation
The package has a test file that you can use to verify that everything was
installed correctly.  To verify the installation, open a Windows command prompt
and issue the following commands:

1.  cd C:\AccessibilityTools\DCC\BatchScanTool
    This will change your working directory to the directory where the Batch
    Scan tool JAR files are installed.
     
2. `java -jar dccbatch.jar -c config.properties`
 
 This will execute the Batch Scan Tool using the default config.properties
    file.  The config.properties file is configured to point to the directory
    where the sample files are located.

    Note: This assumes you have a Java JRE installed and its location is in 
    your Windows PATH.


The test files will be scanned and a message will appear indicating:
```
4 Violation, 1 Potential Violation, 0 Recommendation, 0 Potential Recommendation, 0 Manual Check
Completed scans of 0 epub and 1 html files.
```
To review the detailed report, open the report.csv file located in the 
C:\AccessibilityTools\DCC\ScanOutput directory.

####Configuring the Batch Scan Tool

For the Batch Scan tool, you can specify options either in a configuration file
or from the command line.  Configuration file parameters override default values 
and command line parameters override both.

To customize the Batch Scan tool, copy and rename the config.properties to your 
installation needs.  The config.properties file contains detailed information 
about each supported parameter.  So, please refer to that file for the specifics 
for each parameter.  Here are some of the more important parameters:

    --configFile, -c
    Used to specify your custom configuration file.

    --policies
    Indicates which ruleset(s) should be used during processing.  Always try to 
    use the latest version of a ruleset so issues can be found early.

    --inputFile, -f
    Used to specify the files that need to be processed.  It can be a directory, 
    individual file, individual URL, or a file that contains a list of files,
    directories, or URLs.  For a file that contains a list of files, directories,
    or URLs, each entry needs to reside on a separate line.

    --outputFile, -o
    The name of the output file report.

    --numThreads
    The number of scan engine threads that the engine should use during the scan
    process

    --levels
    Comma separated list of filter levels.  Only message types listed in this 
    list will appear in the output file report.  Violations are always reported.
    Some groups require potential violations and manual filters to be selected.
    The problem with selecting the manual option is that it checks for certain
    technologies being used in your content.  If the technology is detected, it
    provides a message stating that additional testing is required.  This could
    cause important violations or potential violations issues to be drowned out
    by all of the manual messages.  For instance, all topics generated by ID
    Workbench use cascading style sheets.  One manual check is to determine if
    cascading style sheets are being used and issue a message about making sure
    the page is readable without cascading style sheets.  So, if you are testing
    500 topics, you will get this message 500 times.  Only use the manual option
    if you want to know what additional testing you need to perform on your
    content.  But for normal processing, only set the potentialviolation option.

It is recommended that you set the following parameters in your version of the 
config.properties file.  These options shouldn't need to change very often when 
you run the Batch Scan tool:

*   policies
*   showPolicies
*   inputExt
*   outputFormat
*   levels
*   showProps
*   numThreads


If you plan to process multiple directories, it is best to set the inputFile and 
outputFile parameters on the command line.  This way you can change the settings 
each time you run the Batch Scan tool.

####Running the Batch Scan Tool

Assumes the Batch Scan tool is installed in the C:\AccessibilityTools\DCC
directory and you created a custom configuration called my-config.properties and
stored it in the same directory.

To view the list of all supported parameters and usage statement, use the 
following command:

```
java -jar C:\AccessibilityTools\DCC\BatchScanTool\dccbatch.jar --help
```

To get a list of all of the rulesets supported on the RPT server, use the 
following command:
```
java -jar C:\AccessibilityTools\DCC\BatchScanTool\dccbatch.jar -c C:\AccessibilityTools\DCC\my-config.properties --showPolicies true
```

Here is how an invocation of the Batch Scan tool would look if you specified the 
inputFile and outputFile parameters on the command line:
```
java -jar C:\AccessibilityTools\DCC\BatchScanTool\dccbatch.jar -c C:\AccessibilityTools\DCC\my-config.properties -o C:\AccessibilityTools\DCC\ScanOutput\myreport.csv -f C:\AccessibilityTools\DCC\ScanInput
```

###Digital Content Checker overview

The Digital Content Checker can be integrated into your content development processes in a variety
of ways. Some examples of how the checker has been used include:
* Added to a rich text editor such as CKEditor™, enabling content authors to 
obtain feedback about the accessibility of the content they are developing
* Used as feedback into a content development workflow to ensure that automated accessibility
checking is part of the review and approval process
* Called from build scripts to check EPUBs as part of a DevOps automated testing process
* Integrated into tools such as Firebug to provide developers with information about the 
compliance of web applications.

># Related Links {:class="linklist"}
>## SDK {:id="sdk"}
>* [dccbatch.zip](https://ecs-checker.mybluemix.net/priv/dist/dccbatch.zip)
>
># Related Links {:class="linklist"}
>## API Reference {:id="api"}
>* [API Documentation](https://ecs-checker.mybluemix.net/docs/swagger_dcc.html) 
>
# Related Links {:class="linklist"}
>## Related Links {:id="general"}  
>* [IBM Accessibility Web Checklist](http://www-03.ibm.com/able/guidelines/web/accessweb.html)
>* [Web Content Accessibility Guidelines](http://www.w3.org/TR/WCAG20/)
>* [IBM Accessibility](http://www.ibm.com/able)
>
>{:elementKind="article" id="rellinks"}
