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

# Back up your data

To protect your business from data loss and corruption,
you should backup your data.
{:shortdesc}

Two important principles help you avoid downtime and lost revenue:

-	Backup all your data regularly.
-	Check the integrity of the backups.

You can back up your data in Cloudant by using [replication](replication.html) to make a copy of your database.

But if your database is big,
or you need backups for multiple points in time,
having a complete copy of your database for each of the requirements can quickly result in significant disk usage.

An alternative is to use the IBM Cloudant Incremental Backup feature.
Incremental backups are a good solution for storing only the documents that have changed since the last backup.

>   **Note**: Daily incremental backup for Enterprise customers is currently a Beta capability.
    It is not enabled by default.

You can see more information about Incremental Backups in the topic [Back up your data](../guides/backup-guide.html).