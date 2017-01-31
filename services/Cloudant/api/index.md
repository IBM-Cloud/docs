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

# API Reference

The Cloudant API reference is intended to be a comprehensive and living catalog of Cloudant's capabilities.
Contributions are welcome through [Cloudant Labs on GitHub ![External link icon](../images/launch-glyph.svg "External link icon")](https://github.com/cloudant-labs/slate){:new_window}.
{:shortdesc}

## For the cURL samples

There are three ways you can supply the username and password data for a request.

1.	The `-u $USERNAME` parameter on its own causes
	cURL to ask you to enter your password interactively on the command line before performing the request.
	This option is used for the cURL examples in the Cloudant API reference.

2.	**[Caution: This option is not secure]** Entering the combination parameter `-u $USERNAME:$PASSWORD`
	as part of your command means that you are not asked to enter your password interactively.
	However,
	a plain text copy of your password appears in the terminal log.
	<br/>
	<br/>
	A safer variation of this method lets you to define a curl control file,
	containing the following details:<br/>
	`--user "$USERNAME:$PASSWORD"`<br/>
	`--globoff`<br/>
	`--proto "=https"`<br/>
	You can then define an 'alias' that enables the curl command to apply the control file,
	for example:<br/>
	`alias acurl="curl -s --config <full_path_and_name_of_config_file> "`<br/>
	Remember to exclude the control file from backups,
	as it contains the password in clear text.

3.	**[Caution: This option is not secure]** For an `https` cURL request,
	you can supply the username and password as part of the URL:<br/>
	`... https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com ...`<br/>
	However, a plain text copy of your password appears in the terminal log.

An alternative approach is to use a hashed version of your username and password combination,
and supply that data in your cURL command.
The guide on [Authorized curl](../guides/acurl.html)
explains how to create a more complex`acurl` command that makes use of this technique,
enabling you to enter commands such as:<br/>
`acurl https://$USERNAME.cloudant.com`
