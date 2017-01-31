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

# CouchApps

Cloudant can host raw file data,
like images,
and serve them over HTTP,
meaning it can host all the static files necessary to run a website,
and host them just like a web server.
{:shortdesc}

Because these files would be hosted on Cloudant,
the client-side JavaScript could access Cloudant databases.
An application built this way is said to have a two-tier architecture,
consisting of the client - typically a browser - and the database.
In the CouchDB community,
this is called a CouchApp.

Most web apps have three tiers:
the client,
the server,
and the database.
Placing the server inbetween the client and the database can help with authentication,
authorization,
asset management,
leveraging third-party web APIs,
providing particularly sophisticated endpoints,
etc.
This separation allows for added complexity without conflating concerns,
so your client can worry first and last about data presentation,
while your database can focus on storing and serving data.

CouchApps shine in their simplicity,
but frequently a web app will need the power of a 3-tier architecture.
When is each appropriate?

## A CouchApp is appropriate if...

-   Your server would have only provided an API to Cloudant anyway.
-   You're OK using Cloudant's
    [cookie-based authentication](../api/authentication.html).
-   You're OK using Cloudant's [`_users` and `_security`](../api/authorization.html)
    databases to manage users and permissions.
-   You don't need to schedule cronjobs or other regular tasks.

To get started with CouchApps,
read [Managing applications on Cloudant ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/blog/app-management/){:new_window}.

## A 3-tier application is appropriate if...

-   You need finer-grained permissions than the `_security` database
    allows.
-   You need an authentication method other than Basic auth or cookie
    authentication, such as Oauth or a 3rd-party login system.
-   You need to schedule tasks outside the client to run regularly.

You can write your server layer using whatever technologies work best
for you.
A list of libraries for working with Cloudant is [available](../libraries/index.html).
