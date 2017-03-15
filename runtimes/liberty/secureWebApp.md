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

A security vulnerability can be exploited by various security attacks. An attack might steal credentials, cause loss of data and function, disrupt  services, and cause serious damage to the reputation and revenue of a business. Cross-Site-Scripting, XSS, is one of the common security vulnerabilities found in most web applications that must be avoided.

Instead of having to learn the theory of XSS attacks and remedial techniques before starting to develop your web application, this [secure starter application](https://github.com/IBM-Bluemix/java-secure-app) includes coding examples of key secure coding practices that prevent XSS so you can get started developing while learning and applying the XSS prevention techniques.

## How to use the secure sample app
{: #how}

Use the [secure starter application](https://github.com/IBM-Bluemix/java-secure-app) as a starting point for new Liberty application development. Learn the XSS countermeasure code in the app and apply it to the operations of the application API. The countermeasures will help prevent malicious user input from causing damage to your application both on the server and browser, mitigate the XSS attacks, or prevent them altogether.

Download this secure starter application, build and deploy it on Bluemix or locally the same way as you do with the [getting-started-java](https://github.com/IBM-Bluemix/get-started-java) sample application.  See  [Getting started with Liberty on Bluemix](getting-started.html) for more information.  For example, use the steps that follow to clone, build and run the app.

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
View the app at http://localhost:9080/GetStartedSecureJava/

## More Info
{: more}
The secure starter application contains **BadServlet.java**.  This is an example of insecure code that developers may write if care is not taken.

The secure starter application also contains **GoodServlet.java** which includes a number of good secure coding practices such as input validation, output encoding, secure Http Header settings, and Content Security Policy. These are key countermeasures against XSS. Applying them can also mitigate other vulnerabilities such as some injection and directory traversal.

Refer to the [XSS Prevention Cheat Sheet ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.owasp.org/index.php/XSS){: new_window} to learn more about XSS and its countermeasures.
