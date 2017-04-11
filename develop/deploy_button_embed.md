---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-21"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Embedding a Deploy to {{site.data.keyword.Bluemix_notm}} iFrame flow
{: #embed-d2bm-iframe}


You can embed the Deploy to {{site.data.keyword.Bluemix_notm}} flow as an iFrame into many kinds of content that support markup. For example, you can embed the iFrame into readme files, blogs, articles, and web pages.

{: shortdesc}

The iFrame flow is useful when you want to maintain your company branding. When people click your embedded iFrame, they stay in your content instead of being redirected to the bluemix.net website. If you're not concerned with company branding, you can insert a standard [Deploy to {{site.data.keyword.Bluemix_notm}} button](/docs/develop/deploy_button.html) into your content instead of the iFrame.

##Steps in the iFrame flow {: #iframe-steps}

1. If you do not have an active {{site.data.keyword.Bluemix_notm}} account, you create a trial account.

2. You can select a region, organization (org), space, and app name. The suggested app name is constructed from the previous app name, your user name, and the time.

3. The master branch of the original public Git repository is cloned into a new, private {{site.data.keyword.jazzhub_short}} project with a new Git repository.

4. If the app requires a build file, the build file is detected automatically and the app is built.

5. The app is deployed to your {{site.data.keyword.Bluemix_notm}} org.

##Example of the iFrame flow {: #iframe-example}

<p>
The <a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="(Opens in a new tab or window)">IBM
Bluemix D2BM iFrame Sample<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a> provides an iFrame flow example for a public Git repository.<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="Deploy to Bluemix iFrame flow sample" /></div>
</p>

<p>
To view the source for this sample, click <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="(Opens in a new tab or window)">source<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>.
</p>

##Embedding the iFrame flow {: #embed-iframe}  

<ol>
<li>Load the JavaScript utility from <a class="xref" href="https://bluemix.net/deploy/embed.js" target="_blank" title="(Opens in a new tab or window)">https://bluemix.net/deploy/embed.js<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>. This utility depends on jQuery and is loaded by adding the following script tag to your document:
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> Instantiate the <code>DeployToBluemixIFrame</code> constructor by using these arguments:

<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">The ID of the domNode where you want to insert the iFrame into your content.</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">This argument is called when the iFrame flow is completed or if an error occurs. The argument responds with the result. The following code snippet shows a successful result callback:</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">The object that contains the input parameters to the widget. These parameters are available:

<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">The Git repository to use as the source for cloning and deployment. This value is required.</dd>

<dt class="pt dlterm">app_name</dt>
<dd class="pd">The default app name to use as the specified value in the <strong>app_name</strong> field within the iFrame. This value is optional.</dd>


<dt class="pt dlterm">region_id</dt>
<dd class="pd">The ID of the default target region. For example: <code>ibm:yp:us-south</code>. This value is optional.</dd>

<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">The guid of the default target org. To find this value, click <strong>Manage Organizations</strong> > <i>organization_name</i>. The URL for the org contains the guid for that org. This value is optional.</dd>

<dt class="pt dlterm">space_guid</dt>
<dd class="pd">The guid of the default target space. To find this value, click <strong>Manage Organizations</strong> > <i>space_name</i>. The URL for the space contains the guid for that space. This value is optional.</dd>

<dt class="pt dlterm">auto_login</dt>
<dd class="pd">Specifies whether the iFrame automatically logs the user in. The default value is <code>true</code>. This value is optional.</dd>

<dt class="pt dlterm">width</dt>
<dd class="pd">The width of the iFrame. This value is optional. The default value is <code>620</code>.</dd>

<dt class="pt dlterm">height</dt>
<dd class="pd">The height of the iFrame. This value is optional. The default value is <code>470</code>.</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**Tip:** To minimize interaction with the iFrame, you can prefill the **app_name**, **region_id**, **organization_guid**, **space_guid**, and **auto_login** fields.
