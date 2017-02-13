---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

# Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata
{: #custom-dash}


Per utilizzare l'autenticazione personalizzata con la tua applicazione mobile, devi registrare un'area di autenticazione personalizzata e l'URL di base del tuo provider di identità personalizzato nel dashboard del servizio {{site.data.keyword.amashort}}.

## Prima di cominciare
{: #custom-dash-begin}
È necessario disporre di:
* Un'istanza di un servizio {{site.data.keyword.amafull}}.
* Un'applicazione provider di identità personalizzata.

## Configura l'autenticazione personalizzata nel dashboard {{site.data.keyword.amafull}}
{: #custom-dash-config}
Utilizza il dashboard {{site.data.keyword.amafull}} per configurare l'autenticazione personalizzata.

1. Apri il tuo servizio nel dashboard {{site.data.keyword.amafull}}.
1. Dalla scheda **Gestione**, attiva **Autorizzazione**.
1. Espandi la sezione **Personalizzato**.
1. Immetti **Nome realm**, **URL provider di identità personalizzato**. Il valore **I tuoi URI di reindirizzamento dell'applicazione web** è obbligatorio solo per le applicazioni web.

## Fasi successive
{: #next-steps}
* [Configurazione dell'autenticazione personalizzata per Android](custom-auth-android.html)
* [Configurazione dell'autenticazione personalizzata per iOS](custom-auth-ios-swift-sdk.html)
* [Configurazione dell'autenticazione personalizzata per Cordova](custom-auth-cordova.html)
