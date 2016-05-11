---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Automatic configuration of bound services
{: #auto_config}

*Last Updated: 31 March 2016*

You can bind various services to your Liberty application. Services can be container-managed, application-managed, or both, depending on what the developer wants.

An application managed service is a service that is managed entirely by the application, without any assistance from Liberty. The application typically reads VCAP_SERVICES to obtain information about the bound service and accesses the service directly. The application provides all necessary client access code. There is no dependency on Liberty features or the server.xml file configuration. The Liberty buildpack automatic configuration does not apply to services of this type.

A container managed service is a service that is managed by the Liberty run time. In some cases, the application might look up the bound service in JNDI, while in others the service is used directly by Liberty itself. The Liberty buildpack reads VCAP_SERVICES to obtain information about the bound services. For each container managed service, the buildpack performs three functions.

* Generates [cloud variables](optionsForPushing.html#accessing_info_of_bound_services) for the bound service.
* Installs Liberty features and client access code that is required to access the bound service.
* Generates or updates server.xml file stanzas that are required by the service.

This process is referred to as automatic configuration.
The Liberty buildpack provides automatic configuration for the following service types:

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

As noted, some services can be application managed, or container managed. Mongo and SQLDB are examples of such services. By default, the Liberty buildpack assumes that these services are container managed and automatically configures them. If you want the application to manage the service, you can opt-out of automatic configuration for the service by setting the services_autoconfig_excludes environment variable. For more information, see [Opting out of service auto-configuration](autoConfig.html#opting_out).

## Installation of Liberty features and client access code
{: #installation_of_liberty_features}

When you bind to a container managed service, the service might require Liberty features to be configured in the featureManager stanza in the server.xml file. The Liberty buildpack updates the featureManager stanza and installs the required supporting binaries. If the service requires client driver jars, the jars are downloaded to a well-known location in the Liberty install.

See the documentation for the bound service type for more details.

## Generating or updating server.xml configuration stanzas
{: #generating_or_updating_serverxml}

When you push a standalone application, the Liberty buildpack generates the server.xml stanza as described in [Options for Pushing Liberty Applications](optionsForPushing.html#options_for_pushing) to Bluemix. When you push a standalone application and bind to container managed services, the Liberty buildpack generates the necessary server.xml stanzas for the bound services.

When you provide a server.xml file and bind to container managed services the Liberty buildpack:

* Generates the configuration for the bound services if the provided server.xml file does not contain configuration stanzas for the bound services.
* Updates the configuration for the bound services if the provided server.xml file contains configuration stanza for the bound services.

See the documentation for the bound service type for more details.

## Opting out of service auto-configuration
{: #opting_out}

In some cases, you might not want the Liberty buildpack to automatically configure the services that have been bound. Consider the following scenarios.

* My application uses MongoDB, but I want the application to directly manage the connection to the database. The application contains the necessary client driver jar. I do not want the Liberty buildpack to automatically configure the Mongo service.
* I am providing a server.xml file and I have provided the configuration stanzas for the SQLDB instance because I require a non-standard datasource configuration. I do not want the Liberty buildpack to update my server.xml file, but I still require the Liberty buildpack to ensure that the appropriate supporting software is installed.

To opt out of automatic service configuration, use the services_autoconfig_excludes environment variable. You can include this environment variable in a manifest.yml or set it using the cf client.

You can opt out of automatic configuration of services on a per-service-type basis. You can choose to completely opt out (as in the Mongo scenario) or opt out of only the server.xml file configuration updates (as in the SQLDB scenario). The value that you specify for the services_autoconfig_excludes environment variable is a String as shown below.

* The String can contain opt-out specifications for one or more services.
* The opt out specification for a specific service is service_type=option, where:
  * The service_type is the label for the service as displayed in VCAP_SERVICES.
  * The option is either all or config.
* If the String contains an opt-out specification for more than one service, the individual opt out specifications must be separated by a single white-space character.

More formally, the grammar of the String follows.

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**Important**: The service type that you specify must match the services label as it appears in the VCAP_SERVICES environment variable. White space is not allowed.
**Important**: No white space is allowed within a <service_type_specification>. The only allowed usage of white space is to separate multiple <service_type_specification> instances.

Use the "all" option to opt out of all automatic configuration actions for a service, as in the Mongo scenario above. Use the "config" option to opt out of only the configuration update actions as in the SQLDB scenario above.

Here are sample opt-out specifications in a manifest.yml file for the Mongo and SQLDB scenarios.

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: codeblock}

Here are examples of how to set the services_autoconfig_excludes environment variable for the application myapp by using the command-line interface.

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: codeblock}

# rellinks
## general
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
