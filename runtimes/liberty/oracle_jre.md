---

copyright:
  years: 2017
lastupdated: "2016-06-21"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Using Oracle JRE
{: #using_oraacle_jre}

You can run your Liberty application on Bluemix with the Oracle JRE if you choose to.  To do so you must
* host the JRE in a location that the buildpack can download it from,
* host an `index.yml` file which provides the location of the host JRE, and
* configure your application to use that JRE.

## Hosting the JRE and index.yml
{: #hosting_jre}

The Oracle JRE file must be hosted on a web server, and the Liberty buildpack must be able to download it from that server. You can host it on Bluemix itself using any of the available server facilities, or you can host it on some publicly available location.  The server must be configured with an `index.yml` file that specifies details about the JRE file. Complete the following steps to host the JRE and the `index.yml` file:
  1. Acquire the Oracle JRE.  Note that the JRE must be the version for use on a Unix 64 bit OS, and must be a `tar.gz` file.
  2. Host the JRE file in a location from which the Liberty buildpack can download it. 
  3. Ensure that you provide a `index.yml` file at the hosting location. The `index.yml` file must contain an entry consisting of the version ID of the Oracle JRE followed by a colon and the complete URL of the location of that JRE file. The format of the `index.yml` is:
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * For example:
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## Configure the app
{: #configure_app}

Two environment variables must be set on the Liberty application. The *JBP_CONFIG_OPENJDK* must be set to specify the location of the `index.yml` file and the *JVM* environment variable must bet set to *openjdk* to configure the buildpack to use an alternative JRE.

For the JBP_CONFIG_OPENJDK variable the value is
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

To set this you can issue the a command like:
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

Note that the *repository_root* URL does not include `index.yml`, but stops just prior to its location.

To set the JVM environment variable issues a command like:
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**Note**: You must restage your application after setting the environment variables.

## Confirmation
{: #confirmation}

To confirm that the expected JRE is being used, check the staging log for a message similar to the following:
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
