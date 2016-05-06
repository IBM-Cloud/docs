---

copyright:
  years: 2015, 2016
  
---

# Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata
{: #custom-dash}
Per utilizzare l'autenticazione personalizzata con la tua applicazione mobile, devi registrare un'area di autenticazione personalizzata e l'URL di base del tuo provider di identità personalizzato nel dashboard del servizio {{site.data.keyword.amashort}}.

## Prima di cominciare
{: #custom-dash-begin}
* Leggi [Introduzione](getting-started.html).
* Proteggi la tua applicazione di backend con l'SDK server {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi [Protezione delle risorse](protecting-resources.html).
* Fai in modo che ci sia un'applicazione del provider di identità personalizzato in esecuzione.

## Configura l'autenticazione personalizzata nel dashboard {{site.data.keyword.Bluemix}}
{: #custom-dash-config}
Utilizza il dashboard {{site.data.keyword.amashort}} per configurare l'autenticazione personalizzata.

1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix}}.

1. Fai clic su **Opzioni mobili** e annota la tua **Rotta** (`applicationRoute`) e il tuo **GUID applicazione** (`applicationGUID`). Questi valori ti servono quando inizializzi l'SDK.

1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.

1. Fai clic sul tile **Custom**.

1. Immetti il nome dell'area di autenticazione (**Realm name**) e l'URL di base (**Base URL**) del tuo provider di identità personalizzato e salva le tue modifiche.

## Fasi successive
{: #next-steps}
* [Configurazione dell'autenticazione personalizzata per Android](custom-auth-android.html)
* [Configurazione dell'autenticazione personalizzata per iOS](custom-auth-ios.html)
* [Configurazione dell'autenticazione personalizzata per Cordova](custom-auth-cordova.html)
