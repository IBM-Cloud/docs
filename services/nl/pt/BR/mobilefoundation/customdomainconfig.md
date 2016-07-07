---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando o domínio customizado do servidor {{site.data.keyword.mobilefoundation_short}}
{: #configcustomdomain}

*Última atualização: 15 de junho de 2016*
{: .last-updated}

O {{site.data.keyword.mobilefoundation_short}} provisiona um {{site.data.keyword.mfserver_short_notm}} no {{site.data.keyword.containerlong}} como um grupo de contêiner. O grupo de contêiner será mapeado para uma URL que tem os nomes de domínio baseados na **Região** do {{site.data.keyword.Bluemix_notm}}. Também é possível configurar seu próprio domínio customizado.
{:shortdesc}

Um grupo de contêiner é criado com uma URL ou uma rota que tem os nomes de domínio padrão baseados na `Region` do {{site.data.keyword.Bluemix_notm}}.

*Tabela 1. Nomes de domínio de aplicativo baseados na
'Region' no {{site.data.keyword.Bluemix_notm}}*

  |Domínio |  Região  |    
  |:----- | :----- |    
  |`mybluemix.net` | Dallas, EUA  |    
  |`eu-gb.mybluemix.net` | Londres, Reino Unido  |    
  |`au-syd.mybluemix.net`  | Sydney, Austrália |  

Para ser capaz de usar seu próprio domínio, você precisará configurar o domínio customizado executando as etapas a seguir:

1.	Crie uma instância {{site.data.keyword.mfserver_short_notm}} criando a instância de serviço {{site.data.keyword.mobilefoundation_short}} escolhendo um dos planos suportados.

+ Inclua o domínio customizado que você gostaria de usar na `Organization` do {{site.data.keyword.Bluemix_notm}}. Acesse **Gerenciar organizações > DOMÍNIOS > INCLUIR DOMÍNIO** para incluir seu próprio domínio.

+ Configure uma rota para o grupo de contêiner usar seu domínio customizado.

+ Acesse o provedor DNS de seu domínio e inclua uma entrada CNAME, que roteará o tráfego de seu domínio para a rota padrão do {{site.data.keyword.Bluemix_notm}}, em que o grupo de contêiner está em execução.

+ Se quiser configurar `https` para seu domínio customizado, faça upload do certificado SSL para seu domínio no {{site.data.keyword.Bluemix_notm}}. Para fazer isso, acesse **Gerenciar organizações > DOMÍNIOS**, selecione o domínio customizado para o qual você deseja configurar o certificado SSL, clique em **Fazer upload de certificado** para fazer upload do certificado SSL para seu domínio. Consulte [Certificados SSL e Domínios customizados do Bluemix](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/), para obter mais informações.
