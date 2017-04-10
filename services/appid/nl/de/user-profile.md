---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Benutzerprofile interpretieren
{: #user-profile}

Ein Benutzerprofil ist eine Entität, die von {{site.data.keyword.appid_short}} gespeichert und verwaltet wird. Das Profil enthält die Attribute und Identität eines Benutzers. Es kann anonym oder mit einer Identität verknüpft sein, die von einem Identitätsprovider verwaltet wird.
{:shortdesc}

{{site.data.keyword.appid_short_notm}} bietet eine API an, um sich entweder anonym oder über eine Authentifizierung mit einem OpenId Connect (OIDC)-Identitätsproviders anzumelden, siehe [Identitätsprovider konfigurieren](/docs/services/appid/identity-providers.html#setting-up-idp). Der API-Endpunkt des Benutzerprofilattributs ist eine Ressource, die durch den Zugriffstoken geschützt ist, der beim Anmelde- und Berechtigungsprozess von {{site.data.keyword.appid_short_notm}} generiert wird.


## Benutzerattribute speichern, lesen und löschen
{: #storing-data}



{{site.data.keyword.appid_short_notm}} stellt eine <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/" target="_blank">REST-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> für die Durchführung von CRUD-Operationen für Benutzerattribute sowie ein SDK für <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> sowie <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">mobile Swift-Clients <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> bereit.


## OAuth-Identität
{: #oauth}

Beim Aufrufen der OAuth-Anmelde-API, werden in {{site.data.keyword.appid_short_notm}} OAuth 2.0- und OIDC-Protokolle verwendet, um den Aufrufenden mit einem ausgewählten Identitätsprovider zu berechtigen und authentifizieren. Nach der Authentifizierung wird die Identität einem {{site.data.keyword.appid_short_notm}}-Benutzerdatensatz zugeordnet. {{site.data.keyword.appid_short_notm}} gibt ein Zugriffstoken, mit dem auf die Benutzerattribute zugegriffen werden kann, sowie ein Identitätstoken zurück, das die Identitätsinformationen enthält, die vom Identitätsprovider bereitgestellt werden. Von jedem Client aus, der mit derselben Identität authentifiziert wird, kann auf denselben Benutzerdatensatz mit dessen Attributen zugreifen.


## Anonymer Benutzer
{: #anonymous}

Wenn Sie sich anonym anmelden, erstellt {{site.data.keyword.appid_short_notm}} einen Ad-hoc-Benutzerdatensatz, der als anonym markiert wird. {{site.data.keyword.appid_short_notm}} gibt an den Aufrufenden Token für den anonymen Zugriff und Identitätstoken zurück. Bei der Verwendung des Tokens für einen anonymen Zugriff kann die Benutzeranwendung Attribute erstellen, lesen, aktualisieren und löschen, die im Benutzerdatensatz gespeichert sind. Ein Entwickler kann beispielsweise eine Anwendung erstellen, in der ein Benutzer sofort Artikel in den Warenkorb legen kann, ohne sich vorher anzumelden.


## Identifizierte Benutzer
{: #identified}

Ein anonymer Benutzer mit einer Identität, die von einem Identitätsprovider bereitgestellt wird, kann zu einem identifizierter Benutzer werden. Der Ablauf für den Übergang von einem anonymen zu einem identifizierten Benutzer enthält die folgenden Schritte:

* Der Entwickler übergibt das anonyme Zugriffstoken an die Anmelde-API.
* {{site.data.keyword.appid_short_notm}} authentifiziert den Aufrufenden mit dem Identitätsprovider.
* {{site.data.keyword.appid_short_notm}} sucht den anonymem Benutzerdatensatz, der durch das Zugriffstoken definiert wird, und weist ihn der Identität zu.

    **Note**: Dem anonymen Benutzerdatensatz kann die Identität kann nur zugewiesen werden, wenn die Identität noch keinem anderen Benutzer zugewiesen wurde. Wenn die Identität bereits einem anderen {{site.data.keyword.appid_short_notm}}-Benutzer zugewiesen wurde, enthalten die Zugriffs- und Identitätstoken Informationen zu diesem Benutzer und stellen Zugriff auf dessen Attribute bereit. Mit dem neuen Zugriffstoken ist kein Zugriff auf den vorherigen anonymen Benutzer und dessen Attributen möglich. So lange der Token noch nicht abgelaufen ist, kann auf die Informationen über das anonyme Zugriffstoken zugegriffen werden. Der Entwickler kann auswählen, ob die anonymen Attribute des anonymen und bekannten Benutzers zusammengeführt werden sollen.

* Die neuen Zugriffs- und Identitätstoken, die von {{site.data.keyword.appid_short_notm}} empfangen wurden, weisen auf den bekannten Benutzer. Die Identitätstoken enthalten die öffentlichen Informationen, die vom Identitätsprovider empfangen werden.
* Die anonymen Token werden für den Benutzer ungültig.

Die Attribute, die zu diesem Benutzer enthalten sind, während dieser anonym war, sind mit dem neuen Zugriffstoken zugänglich. Neue Token können hinzugefügt, geändert oder gelöscht werden. Der Benutzer und dessen Attribute werden ab jetzt aufgelöst und sind zugänglich, wenn sie sich mit derselben Identität bei einem beliebigen Client anmelden.


## Datentrennung und -verschlüsselung
{: #data}

{{site.data.keyword.appid_short_notm}} speichert und verschlüsselt die Attribute von Benutzerprofilen. Als Multi-Tenant-Service besitzt jeder Tenant einen designierten Verschlüsselungsschlüssel. Die Benutzerdaten in jedem Tenant werden nur mit dem Schlüssel des Tenants verschlüsselt.

{{site.data.keyword.appid_short_notm}} stellt sicher, dass die privaten Daten vor dem Speichern verschlüsselt werden.
