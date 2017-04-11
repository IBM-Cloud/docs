---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Writing Secure Java Web Applications
{: #secure_java_web_app}

All web applications must be designed and coded with security in mind to avoid introducing severe security vulnerabilities.
{: shortdesc}

{{site.data.keyword.Bluemix}} provides a secure starter application to help you write more secure Liberty Java code and avoid most of the Cross-Site Scripting (XSS) issues. You may download this [secure starter application](https://github.com/IBM-Bluemix/java-secure-app), build it and deploy it locally and on {{site.data.keyword.Bluemix_notm}}.

## Why write secure web apps
{: #why}

A security vulnerability can be exploited by various security attacks. An attack might steal credentials, cause loss of data and function, disrupt services, and damage the reputation and revenue of a business. Cross-Site-Scripting, XSS, is one of the common security vulnerabilities found in most web applications that must be avoided.

Instead of learning the theory of XSS attacks and remedial techniques before you start  web application development, you can use this [secure starter application](https://github.com/IBM-Bluemix/java-secure-app). The secure starter application includes coding examples of key secure coding practices that prevent XSS so you can start developing while you learn and apply XSS prevention techniques.

## How to use the secure sample app
{: #how}

You can use the [secure starter application](https://github.com/IBM-Bluemix/java-secure-app) as a starting point for new Liberty application development. Start by learning the XSS countermeasure code in the app and then apply it to the operations of the application API. The countermeasures in the secure starter application help prevent malicious user input from damaging your application both on the server and browser by mitigating or preventing XSS attacks.

First, download this secure starter application, then build and deploy it on Bluemix or locally the same way as you do with the [getting-started-java](https://github.com/IBM-Bluemix/get-started-java) sample application.  Go to [Getting started with Liberty on Bluemix](getting-started.html) to learn more about building and deploying applications on Bluemix.  To get started, you can use these steps to clone, build, and run the app.

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
View the app at http://localhost:9080/GetStartedSecureJava/

## More Info
{: more}
The secure starter application contains **BadServlet.java**. This application shows an example of insecure code that developers might write if care is not taken.

The secure starter application also contains **GoodServlet.java**, which includes a number of good secure coding practices such as input validation, output encoding, secure HTTP Header settings, and Content Security Policy. These practices are key countermeasures against XSS. Applying them can also mitigate other vulnerabilities such as some injection and directory traversal.

Refer to the [XSS Prevention Cheat Sheet ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.owasp.org/index.php/XSS){: new_window} to learn more about XSS and its countermeasures.
