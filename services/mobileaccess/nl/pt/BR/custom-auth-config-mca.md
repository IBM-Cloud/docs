---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

# Configurando o {{site.data.keyword.amashort}} para autenticação customizada
{: #custom-dash}


Para usar autenticação customizada com seu app móvel, deve-se registrar uma região de autenticação customizada e a URL base de seu provedor de identidade customizado no painel do serviço {{site.data.keyword.amashort}}.

## Antes de Começar
{: #custom-dash-begin}
Você deve ter:
* Uma instância de um serviço
{{site.data.keyword.amafull}}.
* Um aplicativo do provedor de identidade customizado.

## Configure a autenticação customizada no painel do {{site.data.keyword.amafull}}
{: #custom-dash-config}
Use o painel do {{site.data.keyword.amafull}} para configurar a autenticação customizada.

1. Abra o seu serviço no painel do {{site.data.keyword.amafull}}.
1. Na guia **Gerenciar**, acione
**Autorização**.
1. Expanda a seção **Customizado**.
1. Insira o **Nome do domínio**,
**URL do provedor de identidade customizado**. O valor **URIs de redirecionamento de aplicativo da
web** é necessário somente para aplicativos da web.

## Próximas etapas
{: #next-steps}
* [Configurando a autenticação customizada para Android](custom-auth-android.html)
* [Configurando a autenticação customizada para iOS](custom-auth-ios-swift-sdk.html)
* [Configurando a autenticação customizada para Cordova](custom-auth-cordova.html)
