---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Comparison of Cloudant and CouchDB API endpoints

This section provides a simple list of the Cloudant (![Cloudant Logo](../images/verySmallCloudant.png)),
CouchDB 2.0 (![CouchDB 2.0 Logo](../images/verySmallCouchDB2.png)),
and CouchDB 1.6 (![CouchDB 1.6 Logo](../images/verySmallCouchDB1.png)) API endpoints and the methods for accessing them,
showing you which endpoints are present in each service.
{:shortdesc}

Some CouchDB endpoints do not have Cloudant equivalents,
because it would not be meaningful.
Similarly,
some Cloudant endpoints do not have CouchDB equivalents.

For more information about a given endpoint on a service,
click the corresponding icon.

<table border='1'>

<tr>
<td><code>GET&nbsp;/</code><p>
<a href='advanced.html#get-/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#get--' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Meta information about the cluster.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_active\_tasks</code><p>
<a href='active_tasks.html#active-tasks' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#get--\_active\_tasks' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--\_active\_tasks' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>List running tasks.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_all\_dbs</code><p>
<a href='database.html#get-databases' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#get--\_all\_dbs' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--\_all\_dbs' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>List all the databases in the instance.</td>
</tr>
<tr>
<td><code>POST&nbsp;/\_api/v2/api\_keys</code><p>
<a href='authorization.html#creating-api-keys' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Generate an API key.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_api/v2/db/{db}/\_security</code><p>
<a href='authorization.html#viewing-permissions' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Who has permissions to read, write, and manage the database.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/\_api/v2/db/{db}/\_security</code><p>
<a href='authorization.html#modifying-permissions' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Modify who has permissions to read, write, and manage a database. Assign an API key.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_api/v2/monitoring/{endpoint}</code><p>
<a href='monitoring.html#monitoring-metrics-overview' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Monitor a specific cluster aspect.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_api/v2/user/config/cors</code><p>
<a href='cors.html#reading-the-cors-configuration' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Current CORS configuration.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/\_api/v2/user/config/cors</code><p>
<a href='cors.html#setting-the-cors-configuration' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Changes the CORS configuration.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_api/v2/user/virtual\_hosts</code><p>
<a href='vhosts.html#listing-virtual-hosts' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>List all virtual hosts.</td>
</tr>
<tr>
<td><code>POST&nbsp;/\_api/v2/user/virtual\_hosts</code><p>
<a href='vhosts.html#creating-a-virtual-host' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Create a virtual host.</td>
</tr>
<tr>
<td><code>DELETE&nbsp;/\_api/v2/user/virtual\_hosts</code><p>
<a href='vhosts.html#deleting-a-virtual-host' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Delete a virtual host.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_config</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/configuration.html#config' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the server configuration.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_config/{section}</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/configuration.html#config-section' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the configuration for the specified section.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_config/{section}/{key}</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/configuration.html#get--\_config-section-key' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the configuration value of a specific key within a configuration section.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/\_config/{section}/{key}</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/configuration.html#put--\_config-section-key' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Update a configuration value. The new value should be supplied in the request body in the corresponding JSON format.</td>
</tr>
<tr>
<td><code>DELETE&nbsp;/\_config/{section}/{key}</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/configuration.html#delete--\_config-section-key' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Delete a configuration value.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_db\_updates</code><p>
<a href='advanced.html#get-/\_db\_updates' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#get--\_db\_updates' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--\_db\_updates' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>List all database events in the instance.<p>In Cloudant the endpoint is only available to dedicated customers. Its documentation references additional query params (limit, since, descending) and an additional feed type value (normal) For CouchDB, its documentation references an additional feed type value (eventsource)</p></td>
</tr>
<tr>
<td><code>GET&nbsp;/\_log</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--\_log' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the log. Equivalent to accessing the local log file of the corresponding instance.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_membership</code><p>
<a href='advanced.html#get-/\_membership' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#membership' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>List the names of nodes in the cluster. Active clusters are indicated in the cluster\_nodes field, while all\_nodes has all nodes.</td>
</tr>
<tr>
<td><code>POST&nbsp;/\_replicate</code><p>
<a href='replication.html#the-/\_replicate-endpoint' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#post--\_replicate' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#post--\_replicate' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Request, configure, or stop, a replication operation.<p>Cloudant documentation references additional request body fields (selector, since\_seq).</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/\_replicator</code><p>
<a href='replication.html#the-/\_replicator-database' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/replication/replicator.html' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/replication/replicator.html' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Trigger a replication.<p>Cloudant documentation references additional request body fields (selector, since\_seq).</p></td>
</tr>
<tr>
<td><code>PUT&nbsp;/\_replicator</code><p>
<a href='replication.html#the-/\_replicator-database' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/replication/replicator.html' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/replication/replicator.html' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Trigger a replication.<p>Cloudant documentation references additional request body fields (selector, since\_seq).</p></td>
</tr>
<tr>
<td><code>DELETE&nbsp;/\_replicator</code><p>
<a href='replication.html#the-/\_replicator-database' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/replication/replicator.html' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/replication/replicator.html' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Cancel an ongoing replication<p>Cloudant documentation references additional request body fields (selector, since\_seq).</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/\_restart</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#post--\_restart' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Restart the instance. You must be authenticated as a user with administration privileges.</td>
</tr>
<tr>
<td><code>POST&nbsp;/\_search\_analyze</code><p>
<a href='search.html#testing-analyzer-tokenization' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Test the results of analyzer tokenization by posting sample data.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_session</code><p>
<a href='authentication.html#cookie-authentication' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/authn.html#get--\_session' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/authn.html#get--\_session' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Returns information about the authenticated user.<p>CouchDB documentation references an additional query param (basic).</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/\_session</code><p>
<a href='authentication.html#cookie-authentication' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/authn.html#post--\_session' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/authn.html#post--\_session' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Initiate a new session for the specified user credentials. Cookie based user login.<p>CouchDB documentation references an additional query param (next).</p></td>
</tr>
<tr>
<td><code>DELETE&nbsp;/\_session</code><p>
<a href='authentication.html#cookie-authentication' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/authn.html#delete--\_session' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/authn.html#delete--\_session' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Closes user's session. Logout cookie based user.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_stats</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--\_stats' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the statistics for the running server.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_utils</code><p>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#get--\_utils' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--\_utils' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Access the built-in Fauxton administration interface.</td>
</tr>
<tr>
<td><code>GET&nbsp;/\_uuids</code><p>
<a href='advanced.html#get-/\_uuids' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#uuids' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#uuids' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Request one or more Universally Unique Identifiers (UUIDs).</td>
</tr>
<tr>
<td><code>GET&nbsp;/favicon.ico</code><p>
<a href='http://docs.couchdb.org/en/2.0.0/api/server/common.html#get--favicon.ico' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/server/common.html#get--favicon.ico' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the binary content for the favicon.ico site icon.</td>
</tr>
<tr>
<td><code>HEAD&nbsp;/{db}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/common.html#head--db' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/common.html#head--db' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the HTTP Headers containing a minimal amount of information about the specified database.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}</code><p>
<a href='database.html#read' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/common.html#get--db' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/common.html#get--db' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get information about the specified database.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/common.html#post--db' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/common.html#post--db' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Create a new document in the specified database, using the supplied JSON document structure.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}</code><p>
<a href='database.html#create' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/common.html#put--db' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/common.html#put--db' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Create a new database.<p>Database names must start with a lowercase letter and contain only the following characters: Lowercase characters (a-z), Digits (0-9), Any of the characters \_, $, (, ), +, -, and /</p></td>
</tr>
<tr>
<td><code>DELETE&nbsp;/{db}</code><p>
<a href='database.html#deleting-a-database' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/common.html#delete--db' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/common.html#delete--db' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Delete the specified database, and all the documents and attachments contained within it.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_all\_docs</code><p>
<a href='database.html#get-documents' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/bulk-api.html#get--db-\_all\_docs' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/bulk-api.html#get--db-\_all\_docs' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>List all the documents in a database.<p>CouchDB documentation references additional query params (end\_key, endkey\_docid, end\_key\_doc\_id, stale, start\_key, startkey\_docid, start\_key\_doc\_id, update\_seq).</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_all\_docs</code><p>
<a href='database.html#get-documents' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/bulk-api.html#post--db-\_all\_docs' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/bulk-api.html#post--db-\_all\_docs' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>List all the documents in a database.<p>CouchDB documentation references additional query params (end\_key, endkey\_docid, end\_key\_doc\_id, stale, start\_key, startkey\_docid, start\_key\_doc\_id, update\_seq).</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_bulk\_docs</code><p>
<a href='document.html#bulk-operations' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/bulk-api.html#post--db-\_bulk\_docs' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/bulk-api.html#post--db-\_bulk\_docs' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Create and update multiple documents at the same time within a single request.<p>CouchDB documentation references an additional request object field (new\_edits).</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_bulk\_get</code><p>
<!-- <a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a> -->
<a href='http://docs.couchdb.org/en/2.0.0/' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>Get multiple documents in a single request.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_changes</code><p>
<a href='database.html#get-changes' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/changes.html#get--db-\_changes' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/changes.html#get--db-\_changes' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>List of changes made to documents in the database, including insertions, updates, and deletions.<p>CouchDB includes query params (attachments, att\_encoding\_info, last-event-id, view). Also filtering using a selector is new in CouchDB 2.0.</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_changes</code><p>
<a href='database.html#using-post-to-get-changes' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/changes.html#post--db-\_changes' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/changes.html#post--db-\_changes' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>List of changes made to documents in the database, including insertions, updates, and deletions.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_compact</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/compact.html#post--db-\_compact' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Request compaction of the specified database.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_compact/{ddoc}</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/compact.html#post--db-\_compact-ddoc' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Compact the view indexes associated with the specified design document.</td>
</tr>
<tr>
<td><code>HEAD&nbsp;/{db}/\_design/{ddoc}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#head--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#head--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the HTTP Headers containing a minimal amount of information about the specified design document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#get--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#get--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the contents of the design document specified with the name of the design document and from the specified database from the URL.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/\_design/{ddoc}</code><p>
<a href='design_documents.html#creating-or-updating-a-design-document' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#put--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#put--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Create a new named design document or create a new revision of the existing design document.<p>Cloudant documentation references an additional request body field (indexes) CouchDB documentation references additional request body fields (language, options).</p></td>
</tr>
<tr>
<td><code>DELETE&nbsp;/{db}/\_design/{ddoc}</code><p>
<a href='design_documents.html#deleting-a-design-document' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#delete--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#delete--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Delete the specified document from the database.</td>
</tr>
<tr>
<td><code>COPY&nbsp;/{db}/\_design/{ddoc}</code><p>
<a href='design_documents.html#copying-a-design-document' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#copy--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#copy--db-\_design-ddoc' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Copy an existing design document to a new or existing one.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_geo\_info/{index}</code><p>
<a href='cloudant-geo.html#obtaining-information-about-a-cloudant-geo-index' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Obtain information about a geospatial index.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_geo/{index}</code><p>
<a href='cloudant-geo.html#querying-a-cloudant-geo-index' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Query a geo index.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_info</code><p>
<a href='design_documents.html#retrieving-information-about-a-design-document' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#get--db-\_design-ddoc-\_info' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#get--db-\_design-ddoc-\_info' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Obtain information about the specified design document, including the index, index size, and current status of the design document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_list/{func}/{other-ddoc}/{view}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#get--db-\_design-ddoc-\_list-func-other-ddoc-view' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#get--db-\_design-ddoc-\_list-func-other-ddoc-view' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the list function for the view function from the other design document.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_design/{ddoc}/\_list/{func}/{other-ddoc}/{view}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#post--db-\_design-ddoc-\_list-func-other-ddoc-view' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#post--db-\_design-ddoc-\_list-func-other-ddoc-view' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the list function for the view function from the other design document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_list/{func}/{view}</code><p>
<a href='design_documents.html#list-functions' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#get--db-\_design-ddoc-\_list-func-view' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#get--db-\_design-ddoc-\_list-func-view' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the list function for the view function from the same design document.<p>The result of a list function is not stored. This means that the function is executed every time a request is made.</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_design/{ddoc}/\_list/{func}/{view}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#post--db-\_design-ddoc-\_list-func-view' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#post--db-\_design-ddoc-\_list-func-view' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the list function for the view function from the same design document.</td>
</tr>
<tr>
<td><code>ANY&nbsp;/{db}/\_design/{ddoc}/\_rewrite/{path}</code><p>
<a href='design_documents.html#rewrite-rules' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/rewrites.html#any--db-\_design-ddoc-\_rewrite-path' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/rewrites.html#any--db-\_design-ddoc-\_rewrite-path' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Rewrite the specified path by rules defined in the specified design document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_search\_info/{index}</code><p>
<a href='search.html#search-index-metadata' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Obtain information about a search specified within a given design document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_search/{index}</code><p>
<a href='search.html#queries' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Query an index.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_design/{ddoc}/\_search/{index}</code><p>
<a href='search.html#posting-search-queries' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
</p></td><td>Query an index.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_show/{func}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#get--db-\_design-ddoc-\_show-func' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#get--db-\_design-ddoc-\_show-func' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the show function for null document.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_design/{ddoc}/\_show/{func}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#post--db-\_design-ddoc-\_show-func' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#post--db-\_design-ddoc-\_show-func' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the show function for null document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_show/{func}/{docid}</code><p>
<a href='design_documents.html#show-functions' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#get--db-\_design-ddoc-\_show-func-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#get--db-\_design-ddoc-\_show-func-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the show function for the specified document.<p>The result of a show function is not stored. This means that the function is executed every time a request is made.</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_design/{ddoc}/\_show/{func}/{docid}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#post--db-\_design-ddoc-\_show-func-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#post--db-\_design-ddoc-\_show-func-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Apply the show function for the specified document.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_design/{ddoc}/\_update/{func}</code><p>
<a href='design_documents.html#update-handlers' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#post--db-\_design-ddoc-\_update-func' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#post--db-\_design-ddoc-\_update-func' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Execute the update function on server side for null document.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/\_design/{ddoc}/\_update/{func}/{docid}</code><p>
<a href='design_documents.html#update-handlers' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/render.html#put--db-\_design-ddoc-\_update-func-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/render.html#put--db-\_design-ddoc-\_update-func-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Execute the update function on server side for the specified document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/\_view/{view}</code><p>
<a href='creating_views.html#using-views' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/views.html#get--db-\_design-ddoc-\_view-view' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/views.html#get--db-\_design-ddoc-\_view-view' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Execute the view function from the specified design document.<p>CouchDB documentation references additional query params (conflicts, end\_key, end\_key\_doc\_id, attachments, att\_encoding\_info, sorted, start\_key, start\_key\_doc\_id, update\_seq). CouchDB 2.0 added sorted parameter not available in CouchDB 1.6.</p></td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_design/{ddoc}/\_view/{view}</code><p>
<a href='creating_views.html#querying-a-view-using-a-list-of-keys' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/views.html#post--db-\_design-ddoc-\_view-view' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/views.html#post--db-\_design-ddoc-\_view-view' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Execute the view function from the specified design document.<p>CouchDB documentation references additional query params (conflicts, end\_key, end\_key\_doc\_id, attachments, att\_encoding\_info, sorted, start\_key, start\_key\_doc\_id, update\_seq).</p></td>
</tr>
<tr>
<td><code>HEAD&nbsp;/{db}/\_design/{ddoc}/{attname}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#head--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#head--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the HTTP headers containing a minimal amount of information about the specified attachment.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_design/{ddoc}/{attname}</code><p>
<a href='attachments.html#read' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#get--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#get--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the file attachment associated with the design document.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/\_design/{ddoc}/{attname}</code><p>
<a href='attachments.html#create-/-update' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#put--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#put--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Upload the supplied content as an attachment to the specified design document.</td>
</tr>
<tr>
<td><code>DELETE&nbsp;/{db}/\_design/{ddoc}/{attname}</code><p>
<a href='attachments.html#delete' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/ddoc/common.html#delete--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/ddoc/common.html#delete--db-\_design-ddoc-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Delete the attachment of the specified design document.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_ensure\_full\_commit</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/compact.html#post--db-\_ensure\_full\_commit' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/compact.html#post--db-\_ensure\_full\_commit' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Commit any recent changes to the specified database to disk.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_explain</code><p>
<a href='cloudant_query.html#explain-plans' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/find.html#post--db-\_explain' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>Identify which index is being used by a particular query.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_find</code><p>
<a href='cloudant_query.html#finding-documents-using-an-index' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/find.html#post--db-\_find' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>Find documents using a declarative JSON querying syntax.<p>Cloudant documentation references additional request body fields (r, bookmark)</p></td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_index</code><p>
<a href='cloudant_query.html#list-all-cloudant-query-indexes' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/find.html#get--db-\_index' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>List indexes.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_index</code><p>
<a href='cloudant_query.html#creating-an-index' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/find.html#post--db-\_index' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>Create a new index.</td>
</tr>
<tr>
<td><code>DELETE&nbsp;/{db}/\_index/\_design/{ddoc}/{type}/{name}</code><p>
<a href='cloudant_query.html#deleting-an-index' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/find.html#delete--db-\_index-designdoc-json-name' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>Delete an index.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_local/{docid}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/local.html#get--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/local.html#get--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the specified local document.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/\_local/{docid}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/local.html#put--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/local.html#put--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Store the specified local document.<p>Local documents are not replicated to other databases.</p></td>
</tr>
<tr>
<td><code>DELETE&nbsp;/{db}/\_local/{docid}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/local.html#delete--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/local.html#delete--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Delete the specified local document.</td>
</tr>
<tr>
<td><code>COPY&nbsp;/{db}/\_local/{docid}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/local.html#copy--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/local.html#copy--db-\_local-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Copy the specified local document.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_missing\_revs</code><p>
<a href='advanced.html#get-/$db/missingrevs' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/misc.html#post--db-\_missing\_revs' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/misc.html#post--db-\_missing\_revs' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the document revisions from the given list that do not exist in the database.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_purge</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/misc.html#post--db-\_purge' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Remove the references to deleted documents from the database.</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_revs\_diff</code><p>
<a href='advanced.html#post-/$db/\_revs\_diff' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/misc.html#post--db-\_revs\_diff' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/misc.html#post--db-\_revs\_diff' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Given a set of document/revision IDs, return the subset of those that do not correspond to revisions stored in the database.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_revs\_limit</code><p>
<a href='advanced.html#get-/$db/\_revs\_limit' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/misc.html#get--db-\_revs\_limit' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/misc.html#get--db-\_revs\_limit' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Get the number of document revisions tracked.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/\_revs\_limit</code><p>
<a href='advanced.html#put-/$db/\_revs\_limit' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/misc.html#put--db-\_revs\_limit' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/misc.html#put--db-\_revs\_limit' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Set the maximum number of document revisions tracked.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_security</code><p>
<a href='authorization.html#viewing-permissions' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/security.html#get--db-\_security' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/security.html#get--db-\_security' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the current security object from the specified database.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/\_security</code><p>
<a href='authorization.html#modifying-permissions' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/database/security.html#put--db-\_security' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/security.html#put--db-\_security' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Set the security object for the given database.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/\_shards</code><p>
<a href='advanced.html#get-/$db/\_shards' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
</p></td><td>Return information about the shards in the cluster</td>
</tr>
<tr>
<td><code>POST&nbsp;/{db}/\_view\_cleanup</code><p>
<a href='http://docs.couchdb.org/en/1.6.0/api/database/compact.html#post--db-\_view\_cleanup' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Remove view index files that are no longer required by as a result of changed views within design documents.</td>
</tr>
<tr>
<td><code>HEAD&nbsp;/{db}/{docid}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/common.html#head--db-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/common.html#head--db-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the HTTP Headers containing a minimal amount of information about the specified document.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/{docid}</code><p>
<a href='document.html#read' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/common.html#get--db-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/common.html#get--db-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the document specified by the docid from the specified db.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/{docid}</code><p>
<a href='document.html#update' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/common.html#put--db-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/common.html#put--db-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Create a new named document or create a new revision of the existing document.</td>
</tr>
<tr>
<td><code>DELETE&nbsp;/{db}/{docid}</code><p>
<a href='document.html#delete' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/common.html#delete--db-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/common.html#delete--db-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Mark the specified document as deleted.</td>
</tr>
<tr>
<td><code>COPY&nbsp;/{db}/{docid}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/common.html#copy--db-docid' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/common.html#copy--db-docid' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Copy an existing document to a new or existing document.</td>
</tr>
<tr>
<td><code>HEAD&nbsp;/{db}/{docid}/{attname}</code><p>
<a href='https://docs.cloudant.com/' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/attachments.html#head--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/attachments.html#head--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the HTTP headers containing a minimal amount of information about the specified attachment.</td>
</tr>
<tr>
<td><code>GET&nbsp;/{db}/{docid}/{attname}</code><p>
<a href='attachments.html#read' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/attachments.html#get--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/attachments.html#get--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Return the file attachment associated with the document.</td>
</tr>
<tr>
<td><code>PUT&nbsp;/{db}/{docid}/{attname}</code><p>
<a href='attachments.html#create-/-update' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/attachments.html#put--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/attachments.html#put--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Upload the supplied content as an attachment to the specified document.</td>
</tr>
<tr>
<td><code>DELETE&nbsp;/{db}/{docid}/{attname}</code><p>
<a href='attachments.html#delete' target='_blank'><img src='../images/verySmallCloudant.png' alt='Cloudant'/></a>
<a href='http://docs.couchdb.org/en/2.0.0/api/document/attachments.html#delete--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB2.png' alt='CouchDB 2.0'/></a>
<a href='http://docs.couchdb.org/en/1.6.0/api/document/attachments.html#delete--db-docid-attname' target='_blank'><img src='../images/verySmallCouchDB1.png' alt='CouchDB 1.6'/></a>
</p></td><td>Delete the attachment associated with the specified doc.</td>
</tr>
</table>