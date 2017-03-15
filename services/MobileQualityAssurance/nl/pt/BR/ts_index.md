---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Resolução de problemas para o {{site.data.keyword.mqa}} 
{: #tsmqa}
Aqui estão as respostas a diversas perguntas comuns sobre como usar o {{site.data.keyword.mqa}}.
{:shortdesc}

## Falha na construção híbrida de JavaScript
{: #ts_js_build_fail}

A construção do aplicativo {{site.data.keyword.mqa}} híbrido JavaScript falha, embora o componente JavaScript&tm; híbrido SDK for IBM MobileFirst Platform Foundation esteja no app e o código necessário tenha sido incluído.


Ao tentar executar a construção do aplicativo {{site.data.keyword.mqa}}, a construção falha.
{: tsSymptoms notoc} 


1. Os componentes SDK híbridos Android e iOS específicos da plataforma não são instalados no projeto.
2. Os componentes SDK híbridos Android e iOS específicos da plataforma que são instalados não são compatíveis com o componente JavaScript SDK instalado.
3. O Android SDK nativo, o iOS SDK nativo, ou ambos, são instalados, mas os componentes SDK híbridos Android e iOS específicos da plataforma não são instalados.
{: tsCauses notoc} 
 

Algumas sugestões para resolver esse problema incluem as etapas a seguir:
{: tsResolve notoc}
  1.  Assegure-se de que tenha instalado todos os componentes SDK híbridos Android e iOS específicos da plataforma necessários e cada Android SDK nativo ou iOS SDK nativo necessário para as plataformas suportadas por seu app. 
  2. Assegure-se de que seus componentes SDK híbridos Android e iOS específicos da plataforma tenham o mesmo número da versão principal que o componente JavaScript ou superior, até a próxima versão principal. A tabela a seguir contém exemplos:
  
| Versão do componente JavaScript | Versão do componente específico da plataforma | Compatível? |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | Sim |
| 1.2.3 | 1.2.1 | Não |
| 1.2.3 | 1.3.2 | Sim |
| 1.2.3 | 2.0.0 | Não |

  3. Assegure-se de que tenha instalado os componentes SDK híbridos Android e iOS específicos da plataforma. Embora o Android SDK nativo e o iOS SDK nativo sejam necessários no caso de seu app ser executado nessas plataformas, os aplicativos híbridos também deverão ter os componentes SDK híbridos Android e iOS específicos da plataforma instalados para cada plataforma.

  
## Não é possível abrir a análise de impressão ou distribuir apps de teste
{: #ts_sent_fail}

Não é possível abrir a análise de impressão ou distribuir o app de teste.

Não é possível abrir a análise de impressão ou distribuir o seu app de teste porque o navegador está bloqueando janelas pop-up.
{: tsSymptoms notoc} 

O Mobile Quality Assurance usa janelas pop-up e cookies para se comunicar com o servidor Mobile Quality Assurance.
{: tsCauses notoc}


Para estabelecer a comunicação entre o Mobile Quality Assurance e o servidor Mobile Quality Assurance, talvez seja necessário configurar as definições do navegador para permitir janelas pop-up e cookies. Por exemplo, quando você clica em uma opção da interface com o usuário, como a Pontuação de impressão, o Mobile Quality Assurance pode ficar impedido de se comunicar com o servidor. A análise de impressão não poderá ser exibida se as janelas pop-up e os cookies estiverem bloqueados. Para obter mais informações sobre como configurar as definições do navegador, consulte a documentação do seu navegador específico.
{: tsResolve notoc}


## Não é possível executar aplicativo expirado
{: #ts_app_expired}

Não é possível executar o aplicativo Mobile Quality Assurance.

Quando você tenta executar o aplicativo Mobile Quality Assurance, vê a mensagem a seguir: Seu aplicativo expirou e não pode ser executado nesse momento.
{: tsSymptoms notoc} 

Seu aplicativo está marcado como desativado na página Construções do Mobile Quality Assurance.
{: tsCauses notoc}


Verifique a página Construções do Mobile Quality Assurance para garantir que nenhum dos aplicativos fique marcado como desativado. Geralmente, os aplicativos são marcados como desativados para informar aos testadores (por meio do próprio aplicativo) para não usarem uma versão específica da compilação. Para obter mais informações sobre as configurações na página Construções do Mobile Quality Assurance, consulte Gerenciando construções no IBM Knowledge Center.
{: tsResolve notoc}

