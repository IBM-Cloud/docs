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

# Authorized curl: `acurl`

_(This guide is based on a Blog article by Samantha Scharr: [
"Authorized curl, a.k.a. acurl" ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/blog/authorized-curl-a-k-a-acurl/){:new_window},
originally published November 27, 2013.)_

`acurl` is a handy alias that allows you to `curl` Cloudant commands to URLs
without having to enter your username and password for every request.
That means a simple `GET` to a database no longer needs to be written as
`https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com/foo`
but instead you can just use `https://$ACCOUNT.cloudant.com/foo`.

Not only does this cut down on annoyingly long URLs,
but the `acurl` alias is also more secure.
It prevents someone from reading your password over your shoulder as you type,
and importantly,
it makes sure your password isn’t sent in plain text over the network by enforcing HTTPS.

All it takes is three simple steps:

1.	[Encode username and password](#encode-username-and-password).
2.	[Create an alias](#create-an-alias)
3.	[Activate the alias](#activate-the-alias).

## Encode username and password

First we base64-encode your Cloudant username and password.
This gives us a base64 character sequence as output.

The command to base64-encode some data is similar to the following example:

```python
python -c 'import base64; print base64.urlsafe_b64encode("$ACCOUNT:$PASSWORD")'
```
{:codeblock}

We assume that the output is called `<OUTPUT-OF-BASE64>`.

For example,
if you use the command:

```python
python -c 'import base64; print base64.urlsafe_b64encode("$ACCOUNT:$PASSWORD")'
```
{:codeblock}

You then get the following output:

```
bXl1c2VybmFtZTpteXBhc3N3b3Jk
```
{:codeblock}

>	**Note**: Remember that your password is still stored in plain text on your computer;
	base64-encoding is _not_ encryption.
	If you use base64-encode on the same character sequence,
	you always get the same corresponding character output sequence.

## Create an alias

Now we create an alias for `curl` that includes these credentials so we don’t have to enter them
every time we write a `curl` command.

Add the following line to your `~/.bashrc` or `~/.bash_profile`:

```sh
alias acurl="curl -s --proto '=https' -g -H 'Authorization: Basic <OUTPUT-OF-BASE64>'"
```
{:codeblock}

This alias adds an Authorization header instead of including the
authorization credentials in the URL you enter on the command line.
It also forces the use of HTTPS which we strongly recommend over plain HTTP
as it encrypts your data and credentials in transit and helps you be sure you’re connecting to Cloudant systems.

## Activate the alias

Now start a new shell or run `source ~/.bash_profile` (or `~/.bashrc` if you used that) to make the alias functional.

## Testing `acurl`

Now let's make sure everything is set up correctly.
Go ahead and run:

```sh
acurl https://$ACCOUNT.cloudant.com/_all_dbs
```
{:codeblock}

If you get the list of your databases back,
awesome!
`acurl` is set up and ready to go.

Happy coding!