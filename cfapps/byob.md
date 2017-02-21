---



copyright:

  years: 2015，2017

lastupdated: "2016-03-15"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Using community buildpacks

If you can't find a starter in the {{site.data.keyword.Bluemix}} Catalog that provides the runtime you want, you can bring an external buildpack to {{site.data.keyword.Bluemix_notm}}. You can specify a custom, Cloud Foundry-compatible buildpack when you deploy your app by using the cf push command.
{:shortdesc}

External buildpacks are provided by the Cloud Foundry community for you to use as your own buildpacks. Before you deploy your app to {{site.data.keyword.Bluemix_notm}}, make sure that you install the cf command line interface.

**Note:** External buildpacks are not provided by IBM; therefore, you might need to contact the Cloud Foundry community for support.

## Built-in community buildpacks

In {{site.data.keyword.Bluemix_notm}}, you can use built-in buildpacks that are provided by the Cloud Foundry community. To see built-in community buildpacks, run the cf buildpacks command:

```
cf buildpacks
Getting buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
For the same runtime or framework, IBM-created buildpacks take precedence over the community ones. If you want to use the community buildpack to overwrite the IBM-created buildpack, you must specify the buildpack by using the -b option with the cf push command.
<p>For example, you can use the community buildpack for Java™ web apps:</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>You can also use the community buildpack for Node.js app:</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>For a runtime or framework that is not supported by IBM-created buildpacks but is supported by built-in community buildpacks, you do not have to use the -b option with the cf push command.</p><p>For example, for Ruby apps, there are no IBM-created buildpacks. You can use the built-in community buildpack by entering the following command:</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## External buildpacks

You can use external or custom buildpacks in {{site.data.keyword.Bluemix_notm}}. You must specify the URL of the buildpack with the -b option, and specify the stack with the `-s` option on the **cf push** command. For example, to use an external community buildpack for static files, run the following command

```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

Another example is that if you do not want to use the built-in community buildpack for Ruby apps, you can use an external buildpack by entering the following command:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

You can also use a custom buildpack for your application. For example, to use an open source PHP buildpack that is provided by the Cloud Foundry community, when you deploy your PHP app to Bluemix, enter the following command to specify the Git repository URL of the buildpack:

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

It is also possbile to edit your project's `manifest.yml` file to add a `buildpack` line:

```
buildpack: https://github.com/cloudfoundry/python-buildpack.git
```
{:pre}


## Specifying the Java buildpack version

<ul>
<li>
Use the <strong>cf set-env</strong> command. For example, enter the following command to set the Java version to 1.7.0:
<pre class="pre"><code>cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &apos;{jre: { version: 1.7.0_+ }}&apos;</code></pre>
<p>Then, restage your app to make the change effective:</p>
<pre class="pre"><code>cf restage app_name</code></pre>
</li>
<li>
Use the <code>manifest.yml</code> file. You can add the environment variable and the value that you want to specify directly to the file. For detailed information, see <a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">Environment variables</a>.</li></ul>
