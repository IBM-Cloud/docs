---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-22"

---
<!-- Copyright info and last updated date at top of file: REQUIRED
    The copyright and lastupdated info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    The value "lastupdated" must be followed by a machine date in quotes in the following format: "YYYY-MM-DD"
    The value for "years" must be indented 2 spaces under "copyright", followed by "lastupdated" which should start on its own non-indented line.

-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Ports used in Cloud Automation Manager
<!-- for example, Uploading your data -->
{: #cam_local_ports}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Because firewall is disabled, knowledge of ports is not required for this Beta release. However, in the following table you can see the list of node and container ports that are used in this Beta release of Cloud Automation Manager. 
{:shortdesc}

#Node and container ports

Name of the microservice| Container port | Node port
------------------------|----------------|-----------
k8_dashboard | 80 | 30001
nodePort_proxy | NA | 30000
nodePort_dashboard | NA | 30001
nodePort_iaas |NA | 30002
nodePort_tenant | NA | 30003
nodePort_bmx_catalog | NA | 30004
nodePort_composer_api | NA | 30005
nodePort_portal_api | NA | 30006
a8-controller | 8080 | NA
a8-registry | 8080 |NA
cam-auth-service | 9443 |NA
cam-catalog | 4100 |30004
cam-iaas | 4000 |30002
cam-identity-mgmt | 4300 |NA
cam-mongo | 27017 | NA
cam-orchestration | 8000 |NA
cam-portal-api | 4000 |30006
cam-portal-ui | 39002 |NA
cam-proxy | 30000 | NA
cam-service-composer-api | 4000 | NA
cam-service-composer-ui | 39002 | NA
cam-tenant-api | 4500 | 30003
cam-ui-basic | 39002 | NA
cam-ui-connections | 39010 | NA
cam-ui-instances | 39008 | NA
cam-ui-templates | 39004 | NA
provider-terraform-local | 7000 | NA
redis | 6379 | NA
