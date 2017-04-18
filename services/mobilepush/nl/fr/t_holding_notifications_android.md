---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Conservation des notifications pour Android
{: #hold-notifications-android}
Dernière mise à jour : 11 janvier 2017
{: .last-updated}

Quand votre application passe en arrière-plan, vous pouvez vouloir que le service {{site.data.keyword.mobilepushshort}} conserve les notifications qui sont envoyées à cette application. Pour conserver des notifications, appelez la méthode hold() dans la méthode onPause() de l'activité qui traite les
notifications de type {{site.data.keyword.mobilepushshort}}.

```
	@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
	} 
```
	{: codeblock}
