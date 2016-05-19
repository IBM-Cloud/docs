---

copyright:

  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#Purging cache content
{: #purgecache}
*Last updated: 03 May 2016*

Use the {{site.data.keyword.cdn_short}} purge cache option to remove all or selected objects from the CDN cache. You will need to use this option every time you push a new Bluemix application or change content of an existing application.
{:shortdesc}

Select the **Operations** tab to view the purge cache option.  

**Note:**: The purge cache configuration option is displayed only after you configure domains. See [Adding the IBM CDN service to an application](cdn_add.html#add_cdn) for steps to configure a domain.

You can purge your CDN cache in two ways:

* Purge all cached web objects in the domain: Select the domain from the **Domain** drop-down, select the **Purge entire cache** check-box, and select **PURGE**.  

* Purge specific objects under the domain:  
	1. Select the domain from the **Domain** drop-down.  
	2. Enter one or more (separated by a comma) list of object paths relative from the domain root in the **Full File Path:** text box. Example: /images/logo.jpg or /video/qa.mp4, audio/training.mp3.  
	3. Select **PURGE**.

**Note:** It can take up to 5 minutes for the purge to be propagated across all cache instances around the globe.
