---

copyright:
  years: 2015, 2016
  
---

# Configurando o {{site.data.keyword.amashort}} para autenticação customizada
{: #custom-dash}
Para usar autenticação customizada com seu app móvel, deve-se registrar uma região de autenticação customizada e a URL base de seu provedor de identidade customizado no painel do serviço {{site.data.keyword.amashort}}.

## Antes de Começar
{: #custom-dash-begin}
* Leia a [Introdução](getting-started.html).
* Proteja seu aplicativo backend com o {{site.data.keyword.amashort}} Server SDK.  Para obter mais informações, veja [Protegendo recursos](protecting-resources.html).
* Tenha um aplicativo de provedor de identidade customizado em execução.

## Configure a autenticação customizada no painel do {{site.data.keyword.Bluemix}}
{: #custom-dash-config}
Use o painel do {{site.data.keyword.amashort}} para configurar a autenticação customizada.

1. Abra seu app no painel do {{site.data.keyword.Bluemix}}.

1. Clique em **Opções móveis** e anote a
**Rota** (`applicationRoute`) e o **GUID
do app** (`applicationGUID`). Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique no ladrilho **Customizado**.

1. Insira o **Nome da região** e a **URL base** de seu provedor de identidade customizado e salve as mudanças.

## Próximas Etapas
{: #next-steps}
* [Configurando a autenticação customizada para Android](custom-auth-android.html)
* [Configurando a autenticação customizada para iOS](custom-auth-ios.html)
* [Configurando a autenticação customizada para Cordova](custom-auth-cordova.html)
