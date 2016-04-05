---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Working with bundles
{: #globalizationpipeline_workingwithbundles}

*Last updated: 25 March 2016*

Each bundle contains a source file and also all of the translations that have been generated from that file.
{:shortdesc}

The source files can be of any of the following formats and must contain content in the form of key/value pairs that represent the UI strings from your app.


<table>
<thead>
<tr>
<th>File type</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td>*Java™ .properties files*</td>
<td><pre class="codeblock">
<code>
logout=Logout
back=Back
examples=Menu
home=Home
web=Web
enterprise=Enterprise
extra=Resources
about=About
settings=Settings
help=Help
support=Support
topics=Topics
appExitMsg=Are you sure you want to quit the application?
</code>
</pre>
</td>
</tr>
<tr>
<td>*AMD I18N*</td>
<td><pre class="codeblock">
<code>
/* JavaScript content from commonapp/home/nls/HomeView.js in folder common */
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
</code>
</pre>
</td>
</tr>
<tr>
<td>*JSON*</td>
<td><pre class="codeblock">
<code>
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
</code>
</pre>
</td>
</tr>
</tbody>
</table>

In addition, a source file must also adhere to these guidelines:
* Each key can be a maximum of 256 characters.
* Each value can be a maximum of 2048 characters.
* Each bundle can contain a maximum of 500 key / value pairs.
* A resource file can be no larger than 2 MB.

After you upload a resource file, its contents can be machine translated into any of the supported languages.

<table>
<thead>
<tr>
<th>Source languagese</th>
<th>Target languages</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="9">English</td>
<td>Chinese (Simplified)</td>
</tr>
<tr>
<td>Chinese (Traditional)</td>
</tr>
<tr>
<td>French</td>
</tr>
<tr>
<td>German</td>
</tr>
<tr>
<td>Italian</td>
</tr>
<tr>
<td>Japanese</td>
</tr>
<tr>
<td>Korean</td>
</tr>
<tr>
<td>Portuguese (Brazilian)</td>
</tr>
<tr>
<td>Spanish</td>
</tr>
</tbody>
</table>

**Note:** English is currently the only supported language for source files. As the {{site.data.keyword.GlobalizationPipeline_short}} service evolves, additional source and target languages will be added.

As bundles are created, they are added to the Bundles tab to make them easily accessible. From there, you can further evolve your translations.


## Selecting a bundle to work with
{: #globalizationpipeline_selectingabundle}

1. Click the **Bundles** tab to view all of the bundles that you created.
2. Click a **Bundle ID** from the list to see more details about that bundle, or click the **View the bundles detail** icon ![Select the View the bundles detail icon to open a bundle and work with its translations](images/viewProjectDetailIcon.png)	in the Actions column.

![View all of the available bundles from the Bundles tab.](images/translationBundles.png)

After you select a bundle to work with, you can view the status of its translations, add or remove languages, edit the translations, or provide updates to the resource file.

If you no longer need a bundle, you can delete it from the **Bundles** tab. All translations that are associated with the bundle are also deleted.

## Modifying bundle details
{: #globalizationpipeline_modifyingbundles}

When you open a bundle you can view all of the details about it. All of the target languages that are in the bundle are listed, along with the current translation status for each.

![The bundle details page shows information about a bundle and its translations.](images/bundleDetails.png)

The status for each language in the bundle can be In Progress, Failed, or Translated:

| Status | Description |
|--------|-------------|
| In Progress | Machine translation is still in progress. |
| Failed | An error occurred while the source file was being translated into the target language. |
| Translated | The translation to the target language is complete. |

You can update the source file that the bundle uses, add a target language to a bundle, delete a target language from a bundle, and download the generated translations for a target language.

### Update the source file that the bundle uses

1. Next to the source language, click the **Upload resources** icon ![Select this icon to upload a new resource file](images/uploadIcon.png) in the Actions column.
2. Click **Browse** and select the new resource file to upload.
3. Select the type of resource file that you are uploading
 * Java .properties file
 * AMD I18N
 * JSON
4. Click **Update** to upload the new resource file.

The key/value pairs that are in the new or updated source file are synchronized with the values that were already uploaded. Only the keys and values that are new or changed are translated after you upload the source file.

### Add a target language to a bundle

1. Click the **Add Language** list.
2. All available target languages are shown, including those that have already been selected. Select the languages to add to the bundle.
3. Click outside of the menu to close it, and then begin the translation process for the languages.

### Delete a target language from a bundle

When you delete a target language from a bundle, you remove the target language and all associated translations from the project. In the Actions column of the target language to remove, click the **Remove this target language** icon ![Select the Remove this target language trash can icon](images/trashIcon.png).

### Download the generated translations for a target language

1. In the Actions column of the target or source language to download, click the **Download the translations** icon ![Select the download icon to download the source keys or translations for a target language](images/downloadIcon.png).
2. Select a file format.
3. Click **Download**.
