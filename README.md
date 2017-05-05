# docs
IBM Bluemix product documentation.

The docs repo is for the product content for IBM Bluemix that is authored in Markdown. The Bluemix *production* doc app builds all Markdown source from this location for all regions.

Each directory in the docs repo must synch with the overall architecture of the Bluemix doc app.

## How to suggest changes or updates to Bluemix documentation

All you need is a GitHub ID, and you can suggest edits and changes to Bluemix docs. A Bluemix team member will review any pull requests, and merge all or parts of your suggested changes as quickly as possible.
To make your changes:

    1. Fork the project or create a branch right from the repository.
    2. Edit files.
    3. When your changes are complete, send a pull request from your branch with your changes.
    4. Wait for a Bluemix team member to review your changes and merge all or parts of your suggested changes
    5. After you are notified of your changes, tidy up your branches using the delete button in the pull request or on the branches page.

For more detailed information on how to contribute content to Bluemix documentation, see the following flow:
https://help.github.com/articles/github-flow-in-the-browser/


## Authoring Bluemix content in Markdown

Purpose
-----------
Markdown is a lightweight markup language with plain text formatting syntax designed so that it can be converted to HTML.

The Markdown used for Bluemix is based on GitHub-flavored Markdown. The following resources can be helpful in coding the markup for you content:
* https://help.github.com/articles/markdown-basics/
* https://help.github.com/articles/github-flavored-markdown/

Bluemix has designed a parser that transforms Markdown into HTML5. Because the syntax available in standard Markdown is limited, the Bluemix team has developed Extensions to provide an enhanced authoring experience. These extensions provide key features available in DITA today, adding, for example, the ability to use metadata attributes and content references in Markdown. This document provides instructions for using these extensions.

Before you begin
-----------

### Markdown Editors
There are many free Markdown editors available, however, not all editors will honor the syntax used by Bluemix extensions. Notepad ++ is free, compatible, and also supports YAML, which is used to define content reference keywords.

# Mappings between DITA, MarkDown, and HTML 5

|     Element     |   XDITA   |   HDITA     | MarkDown (Git flavored)  |   HTML 5      |
|-----------------|-----------|-------------|--------------------------|---------------|
| **container**    | `<topic>` | `<article>` | `No equivalent `           | `<article>`   |
| **title**       | `<title>` |`<h1>...<h6>`| `# ## ### ####`          | `<h1>...<h6> `|
|**short description**|`<shortdesc>`|`<p>`|`No equivalent, first thing under the title must be a paragraph of text`|`<p>`|
|**body**|`<body>`|`No equivalent (ignored)`|`No equivalent`|`--`|
| **section** | `<section>` | `<section>` | `No equivalent` | `<section>` |
| **unordered list** | `<ul>` | `<ul>` | `*` or `-`<br/><br/>**Note**: Nested lists need to be indented four spaces or a tab, and mixing ordered and unordered lists does not work (use html)| `<ul><li></li></ul>` |
| **ordered list** | `<ol>` | `<ol>` | `1.`<br>  `2.`<br> `3.` <br/><br/>**Note**: Nested lists need to be indented four spaces or a tab, and mixing ordered and unordered lists does not work (use html)   | `<ol><li></li></ol>`|
| **list item** | `<li>` | `<li>` | `use the appropriate list type; nested lists are supported:`<br> `1. Item 1`<br>&nbsp;`1. A corollary to the above item.`<br>&nbsp;`2. Yet another point to consider.`<br>`2. Item 2`<br>&nbsp;`* A corollary that does not need to be ordered.`<br> &nbsp;&nbsp;` * This is indented four spaces, because it's two spaces further than the item above.`<br>&nbsp;&nbsp; `* You might want to consider making a new list.`<br>`3. Item 3`| `<ol>`<br>`<li>`<br>`<ol>`<br>`<li>`<br>`<li>`<br>`</ol>`<br>`<li>`<br>`<ul>`<br>`<li>`<br>`<li>`<br>`</ul>`<br>`<li>`<br>`</ol>` |
| **definition list** | `<dl>` | `<dl>` | `No equivalent` | `<dl>` |
| **definition list entry** | `<dlentry>` | `No equivalent (ignored)` | `No equivalent` | `--` |
| **term** | `<dt>` | `<dt>` | `no equivalent` | `<dt>` |
| **definition** | `<dd>` | `<dd>` | `No equivalent` | `<dd>` |
| **paragraph** | `<p>` | `<p>` | No equivalent, Paragraphs in Markdown are just one or more lines of consecutive text followed by one or more blank lines. | `<p>` |
| **code** | `<pre>` | `<pre>` | ```` ```code``` ```` | <pre class="codeblock"><code> |
| **syntax highlighting** | | | ```` ``` ```` <br>`ruby`<br>`require 'redcarpet'<br>markdown = Redcarpet.new("Hello World!")`<br>`puts markdown.to_html`<br> ```` ``` ```` | need to look into this one...or if the Bluemix usage of the Highlighter for Dojo and use the css styles from the highlighter.js removes the need to set a codeLanguage <br> [Languages supported] (https://github.com/github/linguist/blob/master/lib/linguist/languages.yml) |
| **table** | | | `Header 1`  `|` `Header 2` <br> ------------- `|` ------------- <br> `Content`  `|` `Content` <br> `Content`  `|` `Content` <br> **Notes**: <br>1. Your cells do not need to line up on the page in Markdown when editing. <br>2. Tables in Markdown do not support explicit line breaks. To cheat, you can use the `<br>` HTML tag. | `<table>`<br>`<thead>`<br>`<tr>`<br>`<th>Header 1</th>`<br>`<th>Header 2</th>`<br>`</tr>`<br>`</thead>`<br>`<tbody>`<br>`<tr>`<br>`<td>`<br>`Content</td>`<br>`<td>Content</td>`<br>`</tr>`<br>`</tbody>`<br>`</table>` | 
| **italics** | `<i>` |  | `*italic*` | `<em>` | 
| **bold** | `<b>` |  | `**bold**` | `<strong>` |	
| **strikethrough** |  |  | `~~strikethrough~~` | `<del>` |
| **monospace** |  |  |``monospace`` | `<code>` | 	
| **links** | | | You can create an inline link by wrapping link text in brackets `( [ ] )`, and then wrapping the link in parenthesis `( ( ) )`. <br><br> GFM will autolink standard URLs, so if you want to link to a URL (instead of setting link text), you can simply enter the URL and it will be turned into a link to that URL. <br><br>**Note**: to create an external link that opens in a new window, place the following attribute defintion at the top of your file: `{:new_window: target="_blank"}` and then use the following attribute after your link `[link](url){: new_window}` | `<a href="https://www.link.com">Link Text</a>` |	
| **blockquote** |  |  |`In the words of Abraham Lincoln:`<br>`> Pardon my french` | `<blockquote>`<br>`<p>text</p>`<br>`</blockquote>` |	
| **image** |  |  | `![alt text for my graphic](images/image_name.jpg)` | `<p><img src="images/1.png" alt="alt text"></p>` |
| **video** |  |  | `<video width="400px" controls>`<br>`<source src="mov_bbb.mp4" type="video/mp4">`<br>`<source src="mov_bbb.ogg" type="video/ogg">`<br>`Your browser does not support HTML5 video.`<br>`</video>` | `<video width="400px" controls>`<br>`<source src="video/BlueMix Mobile Data iOS Demo v2.mp4" type="video/mp4">`<br>`Your browser does not support HTML5 video.`<br>`</video>` |	
| **keywords** | `<prolog>`<br>`<metadata>`<br>`<keywords>`<br>`<indexterm>`<br>`keyword`<br>`</indexterm>`<br>`</keywords>`<br>`</metadata>`<br>`</prolog>` | | `currently not available` | `<meta name="keywords" content="keyword">` |	
| **metadata** |  |  | `{{site.data.product.bluemix}}` | `data-hd-metadata` |		
| **comments** |  |  | `<!-– comment -->` | `<!-– comment -->` |	
| **mdash** |  |  | `no equivalent` | `&mdash;` |	

# Mappings for how to code in DITA vs Markdown

|  Dita Element     |   HTML 5 output from Dita  |   How to code in Markdown    | HTML 5 output from Markdown  |
|-----------------|-----------|-------------|-------------------|
| **codeblock**    | `<pre class="codeblock">` | ```` ```code``` ```` <br>`{: codeblock}`<br>**Note:** This requires the following attribute definition available in the attribute definition template: `{:codeblock: .codeblock} ` | `<pre class="codeblock">`<br>`<code>code</code>`<br>`</pre>`|
| **pre**    | `<pre class="pre">` | ```` ```code``` ```` <br>`{: pre}`<br>**Note:** This requires the following attribute definition available in the attribute definition template: `{:pre: .pre} ` | `<pre>`<br>`<code>code</code>`<br>`</pre>`|
| **systemoutput**    | `<samp class="ph systemoutput">` | ```` `systemoutput` ```` | `<code>systemoutput</code>`|	
| **codeph**    | `<samp class="ph codeph">` | ```` `codeph` ```` | `<code>codeph</code>`|			
| **userinput**    | `<kbd class="ph userinput">` | ```` `userinput` ```` | `<code>userinput</code>`|	
| **screen**    | `<pre class="pre screen"><code>screen</code></pre>` | ```` ```code``` ```` <br>`{: screen} `<br>**Note:** This requires the following attribute definition available in the attribute definition template: `{:screen: .screen} ` | `<pre class="screen">`<br>`<code>code</code>`<br>`</pre>`|
| **cmdname**    | `<span class="keyword cmdname">cmdname</span>` | `**cmdname**` | `<strong>cmdname</strong>`|
| **varname**    | `<span class="keyword varname">varname</span>` | `*varname*` | `<em>varname</em>`|
| **option**    | `<span class="keyword option">option</span>` | ```` `option` ```` | `<code>option</code>`|			
| **parml**    | `<dl class="parml"><dt class="pt dlterm">pt</dt>`<br>`<dd class="pd">pd</dd>`<br>`</dl>` | `**title**`<br>definition  | `<p><strong>parameter title</strong>`<br>`Definition of the parameter</p>`|			
| **uicontrol**    | `<span class="ph uicontrol">uicontrol</span>` | `**uicontrol**` | `<strong>uicontrol</strong>`|
| **menucascade**    | `<span class="ph uicontrol">uicontrol &gt; uicontrol</span>` | `**uicontrol &gt; uicontrol**` | `<strong>uicontrol &gt; uicontrol</strong>`|
| **apiname**    | `<span class="keyword apiname">apiname</span>` | ```` `apiname` ```` | `<code>apiname</code>`|	
| **filepath**    | `<span class="ph filepath">filepath</span>` | ```` `filepath` ```` | `<code>filepath</code>`|
| **shortdesc**    | `<shortdesc>	<p class="shortdesc">	` | This is a shortdesc paragraph<br>`{: shortdesc} `<br>**Note:** This requires the following attribute definition available in the attribute definition template: `{:shortdesc: .shortdesc}` | `<p class="shortdesc">`|
| **term**    | `<span class="ph term">term</span>` |`*term*` | `<em>term</em>`|

# Bluemix special mappings for how to code in DITA vs Markdown

|  Dita Element     |   HTML 5 output from Dita  |   How to code in Markdown    | HTML 5 output from Markdown  |
|-----------------|-----------|-------------|-------------------|
| **Bluemix Messages**<br>msg<br><br>msgBody<br><br>msgID<br><br>msgPrefix<br><br>msgNumber<br><br>msgSuffix<br><br>msgExplanation<br><br>msgUserResponse    | `<section class="section section msgExplanation">Explanation:`<br><br>`<section class="section section msgUserResponse">Action:` | ```` `msgph` ```` <br><br> `>`msgblock of text<br>`>`this is more text<br>`>`and some more text<br><br>`## BXNUI0001E`<br>`**The attempt to determine whether a session exists failed.**`<br><br>For instructions to fix this problem, see this `[troubleshooting topic](https://www.ng.bluemix.net/docs/troubleshoot/index-gentopic3.html#tr_err)`. | `<code>msgph</code>`<br>`<h2 id="bxnui0001e">BXNUI0001E</h2>`<br>`<p><b>The attempt to determine whether a session exists failed.</b></p>`<br>`<p>For instructions to fix this problem, see this <a href="https://www.ng.bluemix.net/docs/troubleshoot/index-gentopic3.html#tr_err">troubleshooting topic</a>.</p>`|	
| **DITA troubleshooting specialization**<br><br>tsSymptom<br><br>tsCauses<br><br>tsResolve | `<section class="section tsSymptoms">What's happening`<br><br>`<section class="section tsCauses">Why it's happening`<br><br>`<section class="section tsResolve">How to fix it` | This is the "What's happening" paragraph <br>`{: tsSymptoms}`<br>This is the "Why it's happening" paragraph <br>`{: tsCauses}`<br>This is the "How to fix it" paragraph <br>`{: tsResolve}`<br><br>**Note:** This requires the following attribute definitions available in the attribute definition template: <br>`{:tsSymptoms: .tsSymptoms}`<br>`{:tsCauses: .tsCauses}`<br>`{:tsResolve: .tsResolve}` | `<p class="tsSymptoms">This is the "What's happening" paragraph</p>`<br><br>`<p class="tsCauses">This is the "Why it's happening" paragraph</p>`<br><br>`<p class="tsResolve">This is the "How to fix it" paragraph</p>`<br><br> |	
| **Bluemix Runtime Classes**<br>[More Information](https://www.ng.bluemix.net/docs/starters/rt_landing.html)<br> | `<ul class="runtimeIconList">`<br>`<p class="runtimeIcon">`<br>`<p class="runtimeTitle">`<br>`<p class="runtimeLink">` | `*list item 1`<br>`*list item 2`<br>`{: runtimeIconList}` <br><br>Paragraph of text<br>`{: runtimeIcon}`<br><br>Paragraph of text<br>`{: runtimeTitle}`<br><br>Paragraph of text<br>`{: runtimeLink}`<br><br>**Note:** This requires the following attribute definitions available in the attribute definition template: <br>`{:runtimeIconList: .runtimeIconList}`<br>`{:runtimeIcon: .runtimeIcon}`<br>`{:runtimeTitle: .runtimeTitle}`<br>`{:runtimeLink: .runtimeLink}`  | `<ul class="runtimeIconList">`<br>`<li>list item 1</li>`<br>`<li>list item 2</li></ul>`<br><br>`<p class="runtimeIcon">Paragraph of text</p>`<br>`<p class="runtimeTitle">Paragraph of text</p>`<br>`<p class="runtimeLink">Paragraph of text</p>`|
| **Bluemix Related Links** <br><br>`id="rellinks"`<br>id of wrapper tag of all related links section<br><br> `id='general'`<br>id of RELATED LINKS<br><br>`id='api'`<br>id of API REFERENCE<br><br>`id='samples'`<br>id of TUTORIALS AND SAMPLES<br><br>`id='buildpacks'`<br>id of COMPATIBLE RUNTIMES<br><br>`id='sdk'`<br>id of SDK REFERENCE  | `<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks"><h2 class="topictitle2" id="d68e338">Related links</h2>`<br>`<aside>`<br>`<div class="linklist" id="general"><h3 class="linklistlabel">Related Links</h3>`<br>`<ul><li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/doc/personality-insights" rel="external" title="(Opens in a new tab or window)">Detailed Documentation</a></li>`<br>`<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/personality-insights.html" rel="external" title="(Opens in a new tab or window)"><span class="keyword">Personality Insights</span> home page</a></li>`<br>`<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/watson/" rel="external" title="(Opens in a new tab or window)">Watson developer cloud community</a></li>`<br>`</ul></div>`<br><br>`<div class="linklist" id="samples"><h3 class="linklistlabel">Tutorials and Samples</h3>`<br>`<ul><li><img src="./sout.gif" alt=""><a href="https://watson-pi-demo.mybluemix.net/" rel="external" title="(Opens in a new tab or window)">Live Demo</a></li>`<br>`<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/doc/personality-insights/index.html#sampleApp" rel="external" title="(Opens in a new tab or window)">Sample Application source and instructions</a></li>`<br>`<li><img src="./sout.gif" alt=""><a href="https://github.com/watson-developer-cloud/nodejs-wrapper" rel="external" title="(Opens in a new tab or window)">Client-side library for Watson in Node.js</a></li>`<br>`<li><img src="./sout.gif" alt=""><a href="https://github.com/watson-developer-cloud/java-wrapper" rel="external" title="(Opens in a new tab or window)">Client-side library for Watson in Java</a></li>`<br>`</ul></div>`<br><br>`<div class="linklist" id="api"><h3 class="linklistlabel">API Reference</h3>`<br>`<ul><li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/apis/#!/personality-insights" rel="external" title="(Opens in a new tab or window)">REST API</a></li>`<br>`</ul></div>`<br>`</aside></article>` | `# rellinks`<br><br>`## samples`<br>`* [link text](http://URL)`<br>`* [link text](http://URL)`<br><br>`## sdk`<br>`* [link text](http://URL)`<br>`* [link text](http://URL)`<br><br>`## api`<br>`* [link text](http://URL)`<br>`* [link text](http://URL)`<br><br>`## buildpacks`<br>`* [link text](http://URL)`<br>`* [link text](http://URL)`<br><br>`## general`<br>`* [link text](http://URL)`<br>`* [link text](http://URL)` | `<h1 id="rellinks">rellinks</h1>`<br>`<h2 id="samples">samples</h2>`<br>`<ul>`<br>`<li>`<br>`<li>`<br>`</ul>`<br><br>`<h2 id="sdk">sdk</h2>`<br>`<ul>`<br>`<li>`<br>`<li>`<br>`</ul>`<br><br>`<h2 id="api">api</h2>`<br>`<ul>`<br>`<li>`<br>`<li>`<br>`</ul>`<br><br>`<h2 id="buildpacks">buildpacks</h2>`<br>`<ul>`<br>`<li>`<br>`<li>`<br>`</ul>`<br><br>` <h2 id="general">general</h2>`<br>`<ul>`<br>`<li><a href="http://www.softlayer.com/security">Soflayer Security Compliance</a></li>`<br>`<li><a href="/docs/services/SingleSignOn/index.html">Getting started with Single Sign On</a></li>`<br>`</ul>` |
| **Bluemix Context Switching**<br><br>`data-hd-programlang="languagecode"`<br>`//programming language and OS`<br>`csAllProgramlangs: [`<br>`{key:"generic", label:"Generic"},`<br>`{key:"java", label:"Java"},`<br>`{key:"ruby", label:"Ruby"},`<br>`{key:"c#", label:"C#"},`<br>`{key:"objectc", label:"Objective C"},`<br>`{key:"python", label:"Python"},`<br>`{key:"javascript", label:"JavaScript"},`<br>`{key:"php", label:"PHP"},`<br>`{key:"swift", label:"Swift"}`<br>`   ],`<br>`csAllOperatingsystems: [`<br>`{key:"generic", label:"Generic"},`<br>`{key:"ios", label:"iOS"},`<br>`{key:"android", label:"Android"}`<br>`   ],` | `<pre class="codeblock"`<br>`data-hd-programlang="javascript"><code>&lt;script&gt;`<br><br>`var setup = {`<br>`applicationId:'&lt;<var class="keyword varname">applicationId</var>&gt;',`<br>`applicationRoute:'&lt;<var class="keyword varname">applicationRoute</var>&gt;',`<br>`applicationSecret:'&lt;<var class="keyword varname">applicationSecret</var>&gt;'`<br>`}`<br><br>`IBMBluemix.initialize(setup);`<br>`&lt;/script&gt;</code>`<br>`</pre>`<br><br>`<pre class="codeblock" data-hd-operatingsystem="ios"><code>[IBMBluemix initializeWithApplicationId: <var class="keyword varname">applicationId</var> andApplicationSecret: <var class="keyword varname">applicationSecret</var> andApplicationRoute: <var class="keyword varname">applicationRoute</var>]</code></pre>` | `<!-- Attribute definitions -->`<br>`{:javascript: #javascript .ph data-hd-programlang='javascript'}`<br>`{:java: #java .ph data-hd-programlang='java'}`<br>`{:ruby: #ruby .ph data-hd-programlang='ruby'}`<br>`{:shortdescription: .shortdesc}`<br><br>`<!-- Applying the above definitions to inline code tags and paragraph tags -->`<br>`You can use the `Node.js`{: javascript} `Java`{: java} `Ruby`{: ruby} sample application to try the RabbitMQ service.`<br>`{: shortdescription}`<br><br>**Note:** This requires attribute definitions available in the attribute definition template. | `<p class="shortdesc">You can use the <code id="javascript" class="ph" data-hd-programlang="javascript">Node.js</code> <code id="java" class="ph" data-hd-programlang="java">Java</code> <code id="ruby" class="ph" data-hd-programlang="ruby">Ruby</code> sample application to try the RabbitMQ service.</p>` |
| **Bluemix App Data**<br><br>`user's app related metadata: "app_name", "app_url", "service_name", "service_instance_name", "plan", "host"` | ? | ?<br>**Note:** This requires the following attribute definition available in the attribute definition template: `{:?: .?}` | ? |


# Bluemix Extensions
 The following Bluemix extensions to Markdown are supported:
 * Output all MarkDown markup to standard, valid HTML5 tags
 * Attributes
 * Addition of headers and footers to the HTML output
 * Anchor IDs Generated for all Headers
 * Content References
 * TOC file
 * Output is fully accessible
 * Additional functionality
 

### Attributes
The Bluemix Markdown parser allows you to define additional attributes in Markdown. After your attributes are defined, you can apply these values to any markdown element, like headers, paragraphs, and codeblocks. 

You can use the Bluemix attributes extension to map the following attributes to an element:
  * ID
  * Class
  * Custom value

**Note**: Attributes, when defined and applied within a Markdown file, are output by the Bluemix Markdown parser by default. No additional parameters or flags need to be passed to the parser when the command is run.
  
#### How attributes are defined in Markdown
Attributes are defined at the top of your Markdown file. Each Attribute definition must be enclosed in curly brackets { }, and must contain a unique name. While you can provide attribute definition values for ID, Class, and Custom, none of these values are required, and you can define any combination of these different attribute values. The Bluemix Attribute Definitions implimentation is based on the Kramdown / Maraku Attribute Definiton extension: (http://kramdown.gettalong.org/syntax.html#attribute-list-definitions).

For Example:
```
<!-- Attribute definition --> 
{:Name: #ID .Class Custom='custom attribute'}
<!-- Sample Attribute definition --> 
{:java: #java .ph data-hd-programlang='java'}

```

* **:Name:** is the name of the attribute. This value does not get passed through to the output, it is an internal Markdown name that is used to map the attribute definition at the top of the page to one or more uses throughout the Markdown file. This value must be surrounded by colons (: :).
* **#ID** sets a value associated with the `id` attribute. This value is optional. If I define an ID of `#java` in my attribute, and I set this attribute on a Header, the HTML5 output will produce `<h1 id="java"></h1>`. This value must begin with a pound sign (#).
* **.Class** sets a value associated with the Class attribute. This value is optional. If I define a Class of `.ph` in my attribute, and I set this attribute on a Header, the HTML5 output will produce `<h1 Class="ph"></h1>`. This value must begin with a pound period (.).
* **.Custom** sets a custom attribute value. This value is optional. If I define a Custom value of `data-hd-programlang='java'` in my attribute, and I set this attribute on a Header, the HTML5 output will produce `<h1 data-hd-programlang='java'></h1>`. 

#### How attributes are applied in Markdown
After you define your attribute at the top of your Markdown file, you can apply the attribute by adding a call to the name of your attribute to the end of the Markdown tag you want to bind your attribute to. The implimentation of Bluemix attribute usage is based on the Kramdown / Maraku Block/Span Inline Attribute Lists: http://kramdown.gettalong.org/syntax.html#inline-attribute-lists

To apply a defined attribute, call the name of the attribute surrounded by curly brackets, and pre-pended by a colon and a space: `{: Name}`

For example:
I define a short description attribute at the top of my file and then apply it to a paragraph:
```
 {:shortdescription: .shortdesc}
 
 This is a short description paragraph
 {: shortdescription}
 
```
The Markdown parser will output HTML5 that looks like this:

```
<p class="shortdesc">This is a short description paragraph</p>

```
  
#### Attributes in DITA vs Markdown  
In DITA, attributes are used to add metadata to elements. For example, you might add a `product`, `props`, or `otherprops` attribute on a phrase or paragraph element in order to associate a value with that phrase or paragraph. These values allow for filtering either during build or runtime. DITA transforms to HTML5 also apply Class attributes to HTML5 elements, and these values are used by the .CSS stylesheets at runtime to control the display.

Example of DITA attributes (from `using_rabbitmq_service.dita`):
Here we can see that the author has added a `props` attribute to 3 phrase tags, and added a unique programming language value to each `prop`.

```
<shortdesc>You can use the <ph props="programlang(javascript)">Node.js</ph> <ph
props="programlang(java)">Java</ph> <ph props="programlang(ruby)">Ruby</ph> sample
application to try the <keyword
conref="cloudoeconrefs.dita#cloudoeconrefs/rabbitmq">RabbitMQ</keyword> service.</shortdesc>

```
HTML5 output transformed with IDWB:

```
<p class="shortdesc">You can use the <span class="ph" data-hd-programlang="javascript">Node.js</span> <span class="ph" data-hd-programlang="java">Java</span> <span class="ph" data-hd-programlang="ruby">Ruby</span> sample
application to try the <span class="keyword">RabbitMQ</span> service.</p>

```

In Markdown, the Bluemix parser will apply whatever attributes you define to any of the supported Markdown elements, (For example, Header, Paragraph, Codeblock, Blockquote, Inline Code, Bold, Italics, Table, etc.). While Markdown does not support the Phrase tag, you can still bind attributes to single words or phrases by using inline tags like Code, Bold, or Italics.

The Bluemix doc framework provides runtime context switching functionality that looks for attributes on HTML5 elements and hides or displays this content depending on selections made by the user. Support for context switching in Markdown source is just one of the ways writers can use the Bluemix attribute extension. In addition, writers can add anchor IDs to multiple elements, overwrite anchor IDs on headers, add Class attributes like `shortdesc` to a paragraph to define the output as a shortdescription, as well as define their own custom attribute values on supported elements.

Example of Markdown attributes definitions and applications (from `using_rabbitmq_service.md`):
The DITA source example above from `using_rabbitmq_service.dita` is an example of a file that has been designed for context switching. When the HTML5 output is displayed at runtime in the Bluemix doc framework, if the user selects to view only Ruby, elements containing the attribute `data-hd-programlang="ruby"` will be displayed, and elements with the attribute of `data-hd-programlang` that contain anything other than `"ruby"` will be hidden. Below I have created a near-equivalent version of the DITA topic in Markdown, complete with attributes that support context switching.

```
<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:shortdescription: .shortdesc}

<!-- Applying the above definitions to inline code tags and paragraph tags --> 
You can use the `Node.js`{: javascript} `Java`{: java} `Ruby`{: ruby} sample application to try the RabbitMQ service.
{: shortdescription}

```
 
Output of HTML5 from Markdown parser: 

```
<p class="shortdesc">You can use the <code id="javascript" class="ph" data-hd-programlang="javascript">Node.js</code> <code id="java" class="ph" data-hd-programlang="java">Java</code> <code id="ruby" class="ph" data-hd-programlang="ruby">Ruby</code> sample application to try the RabbitMQ service.</p>

```

### Headers and footers
Bluemix needed to add copyright and metadata to the header of the HTML 5 output. We have standard header and footer files that are called during transformation.

#### Anchor IDs Generated for all Headers
When the Bluemix Markdown parser transforms Markdown to HTML5, it automatically binds an anchor ID to all Header elements. Any time the parser transforms a Markdown file that contains a header, the HTML5 output of that header tag will produce an `id` attribute, with a value that is unique. Unique anchor IDs on headers provide writers with the ability to link directly to a sub-topic that begins with a Header.

For example, here is a level 4 Header in Markdown: 
```
#### Content references in DITA vs Markdown
```
When the above Markdown is transformed into HTML5, the parser produces a unique id with a value that is equal to the name of the header:
```
<h4 id="content-references-in-dita-vs-markdown">Content references in DITA vs Markdown</h4>
```
**Note**: Header anchor IDs are output by the Bluemix Markdown parser by default. No additional parameters or flags need to be passed to the parser when the command is run.

#### Changing an anchor ID on a Header

The Anchor ID is bound to a header by default, and it always uses the text of the header as its name, so you can always just link to that. However, any time you want to override the anchor tag of a header, you can use an attribute. See the Attribute section above for more details on using attributes.

Example of default anchor bound to a header:

Mardown source:
`## Visualizing your data sample`

HTML5 output:
`<h2 id="visualizing-your-data-sample">Visualizing your data sample</h2>`

Example of remapping using a simple attribute (we use the ID attribute, which is mapped with the # character):

Markdown source:
```
## Visualizing your data sample
  {: #my-renamed-anchor}
```

HTML5 output:
`<h2 id="my-renamed-anchor">Visualizing your data sample</h2>`

**Note**: You could produce the same results by making an attribute definition at the top of your file, and then you would call the name of the attribute definition, like so:
```
{:myanchor: #my-renamed-anchor}

## Visualizing your data sample
  {: myanchor}
```

#### Linking to an anchor ID for a header

You can link directly to a header within a file using the header anchor ID. You can link to sub-headings; it does not need to be the top-level header. Use the automatically generated header value based on the text that is defined in the header (see Anchor IDs Generated for all Headers), or add your own anchor ID to use for linking (see Changing an anchor ID on a header). The following example for linking uses user-defined ID anchors for each header, and the goal is to provide a link to content that is further down in the same file.

```
Headings and user-defined header anchors for my file:

# Bluemix
{: #bluemix}

My short description links to the [Applications heading](filename.html#header_id).

## Services
{: #services}

## Applications
{: #applications}

I want to create a link within my short description that links to the second sub-heading, Applications. 
To do this, I would use the following format: [Link text for header](filename.html#header_id). 
For this example, I would use [Applications](readme.html#applications).
```

### Content References
The Bluemix conref extension is invoked by the parser by using the conrefFile flag: `--conrefFile=cloudoeconrefs.yml`. 
 
 >node mdProcessor.js --sourceDir=C:\pilot\sourceMD --destDir=C:\pilot\outputMD --headerFile=header.txt --footerFile=footer.txt 
 >**--conrefFile=cloudoeconrefs.yml** -overwrite
 
Conrefs are stored in `cloudoeconrefs.yml`. `cloudoeconrefs.yml` is a YAML file, and can be placed in any directory as specified in the `--conrefFile` parameter. Typically, `cloudoeconrefs.yml` can be found in `C:\Users\IBM_ADMIN\Documents\GitHub\markdownProcessor`.

Conref definitions in YAML are structured in nested keys, each key that contains a value or a subkey must be followed by a colon (:), and the next line must be indented 2 space. For example:
```
 key:
  subkey1:
    conref value 1
  subkey2:
    conref value 2
    
```
Conrefs in Markdown are called by using the following syntax: `{{site.data.key1.key2...keyN}}`
**Note:** While you can Nest keys as deep as you like in YAML, and call deeper sets of keys from markdown, Bluemix conrefs use only 2 keys. For example: `{{site.data.keyword.bluemix}}`  

#### Content references in DITA vs Markdown
In DITA, a content reference, or conref, is a way of reusing or pulling content from one file into another file; effectively making a copy during the transform. 
 
Example of conrefs sourced in DITA (stored in cloudoeconrefs.dita):
```
	<!--//Do not translate - Begin-->
	<p><keyword id="bluemix"><tm tmtype="reg" trademark="IBM">IBM</tm> <tm tmtype="tm" trademark="Bluemix">Bluemix</tm></keyword></p>
	<p><keyword id="bluemix_short"><tm tmtype="tm" trademark="Bluemix">Bluemix</tm></keyword></p>
	
```
Example of a conref being called from a DITA file (called from rails.dita):
 
```
	<p>This Ruby starter application is a boilerplate for <keyword conref="cloudoeconrefs.dita#cloudoeconrefs/bluemix_short">BlueMix</keyword> Ruby web application development.</p>	
 
```
 
In the Bluemix Markdown extension, we create a similar mechanism for reusing or pulling content from one file into another file. The extension uses YAML as a source for the conrefs.  
 
Example of conrefs sourced in YAML (stored in cloudoeconrefs.yml):
 
```
	#Bluemix conref equivalent file to cloudoeconrefs.dita

	#//Do not translate - Begin
	keyword:
	  bluemix:
	    IBM&reg; Bluemix&trade;
	  bluemix_short:
	    Bluemix&trade;
	  IBM:
	    IBM&reg;
	  cloudoe:
	    Cloud Operating Environment
	  domainname:
	    DomainName
	  Appdomainname:
	    AppDomainName
	#Service names
	  activedeployshort:
	    Active Deploy
	  amashort:
	    Advanced Mobile Access
	  activedeployshort:
	    Active Deploy
	  amashort:
	    Advanced Mobile Access

```
 
Example of conrefs called from Markdown (called from test.md):
 
```
	This is a new paragraph all about using conrefs. This word here: {{site.data.keyword.bluemix}} is actually a conref! I can use {{site.data.keyword.bluemix}} multiple times in a paragraph. 
	* I can use the full product name: {{site.data.keyword.bluemix}}
	* Or I can use the shortened product name: {{site.data.keyword.bluemix_short}}
	* {{site.data.keyword.activedeployshort}} is a Service. 
	* So is {{site.data.keyword.amashort}}
	
```

Results:
 
```
	 This is a new paragraph all about using conrefs. This word here: IBM® Bluemix™ is actually a conref! I can use IBM® Bluemix™ multiple times in a paragraph.

		I can use the full product name: IBM® Bluemix™
		Or I can use the shortened product name: Bluemix™
		Active Deploy is a Service.
		So is Advanced Mobile Access
		
```

### TOC File
In addition to the standard HTML5 output that the Bluemix Markdown parser produces from each Markdown file, the parser also produces a Table of Contents file in different formats. Each TOC file produced from a markdown topic contains a nested set of structured headers or topicrefs that match the structure of headers in the original markdown source. Each TOC header or topicref also contains a link to a corresponding header anchor ID in the HTML5 output file that was generated from the Markdown source.

By default, for each Markdown file processed by the Bluemix parser, the following files are output:

**Source:** `index.md`

**Output:**
* `index.HTML`: standard HTML5 output
* `indexTOC.md`: Markdown file with nested Headers matching each Header in index.md. Each Header contains a link to  a corresponding header anchor ID in index.HTML
* `indexTOC.HTML`: HTML file with nested Headers matching each Header in index.md. Each Header contains a link to  a corresponding header anchor ID in index.HTML
* `index.ditamap`: DITA map file with nested topicrefs matching each Header in index.md. Each topicref contains a link to  a corresponding header anchor ID in index.HTML

**Note:** Each TOC format is produced and structured following the conventions of that format. Because DITA map files enforce a strict rule where headers must be incremented by only a single level, any Headers in your markdown that skip a level, (for example, H1 to H3, skipping H2), will not produce a valid *.ditamap TOC. Header values can decrease by skipping a level, (for example, H3 to H1, skipping H2), but they cannot increase.

**Note**: TOC files are output by the Bluemix Markdown parser by default. No additional parameters or flags need to be passed to the parser when the command is run. To disable TOC files, add the following parameter: `-disableToc`

### Accessible output
We have worked to output all Markdown markup to standard and valid HTML5 tags:
* Alt text for images: Included as part of the Markdown tagging for images
* Header row in tables: Output turns the first row into `<thead>`
* Elements having a WAI-ARIA 'article' role must have a label specified with aria-label or aria-labelledby.
* Use header elements where appropriate: Pass thru HTML tagging when Markdown markup is not available, for example definition lists (dl, dt, dd)
* There must be a non-empty title element in the head of the document: For the HTML output from Markdown, the `<head>` element does not contain a `<title>` element. We added this with a header file.
* To embed a video, you must ensure that the video player is fully accessible. If you link to multimedia or video content, ensure the following are complete:
	* Where you link to your video, the player must be accessible which means using keyboard access only the user must be able to stop/start the video and turn on captions.
	* Include captioning for the video.
	* Include a text transcript for your video. This text transcript must be accessible, so you must run AVT testing on this document that is available for viewing or download. Also, included in this transcript must be the full audio description that has all on-screen actions described. For example, your video is a demo of a set of on-screen actions, so all clicks, movements, menu options, etc. must be announced. If this is not the case, a separate audio description with these plus a transcript is required. The text transcript should always include on-screen actions and the audio.
	* The content within your video should pass visual accessibility standards such a color contrast for images of text, high contrast, etc.  
	


Additional accessibility *might* be needed as content is migrated to Markdown. And, as a result, updates to the parser and/or to the markup recommendations *might* be required.

### Additional functionality
 * Copy of non-.md files: Copies (doesn't process) image files (.bmp, .jpg, .png, .gif, .SVG) and other file extensions like .html, .pdf, .json, .js
 * Recurse sub-directories: Processes all directories in the specified source directory
 * Overwrite: Addition of an overwrite flag to replace previous output
 
### Tips for avoiding common errors

1. Using HTML within your Markdown topics is allowed, and in some cases encouraged (the only way to output a definition list is by using HTML). However, if you chose to use HTML, **always ensure your HTML is well-formed**. Any tag that does not have a closing tag associated with it will break the parser, and your build will fail. For example, the only way that you can create a line break inside a table cell in Markdown is to use a break tag, however, using `<br>` will actually break the build. You must close the break tag like so: `<br/>`. If you use HTML, carefully validate that your tags are matching and that you close all open tags.
2. Avoid using `<` and `>`. For all special characters, it is recommended that you use the `&` value. For example, for `>` use `&gt;`.  All of the following special characters are also supported: (http://www.w3.org/MarkUp/HTMLPlus/htmlplus_13.html)
