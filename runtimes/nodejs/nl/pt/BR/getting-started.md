---

copyright:
  years: 2017
lastupdated: "2017-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}


# Introdução ao Node.js no Bluemix

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}! Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo esse guia, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados do {{site.data.keyword.Bluemix}} em seu app.

## Pré-requisito
{: #prereqs}

Você precisará das contas e ferramentas a seguir:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Nó ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://nodejs.org/en/){: new_window}


## 1. Clone o app de amostra
{: #clone}

Primeiro, clone o repositório GitHub do app de amostra Node.js *hello world*.
  ```
git clone https://github.com/IBM-Bluemix/get-started-node
  ```
  {: pre}

## 2. Execute o app localmente
{: #run_locally}

Use o gerenciador de pacote npm para instalar dependências e executar seu app.

1. Na linha de comandos, mude o diretório para onde o app de amostra está localizado.
  ```
cd get-started-node
  ```
  {: pre}

1. Instale as dependências listadas no arquivo [package.json ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.npmjs.com/files/package.json) para executar o app localmente.  
  ```
npm install
  ```
  {: pre}

1. Execute o app.
  ```
npm start  
  ```
  {: pre}

É possível visualizar seu app em http://localhost:3000.

Use [nodemon](https://nodemon.io/) para reinicialização automática do aplicativo em mudanças no arquivo.
{: tip}


## 3. Prepare o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-node`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedNode` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras. Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência. [Saiba mais...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Implemente o app
{: #deploy}

É possível usar o Cloud Foundry CLI para implementar apps no {{site.data.keyword.Bluemix_notm}}.

Execute o comando a seguir para configurar seu terminal de API, substituindo o valor *API-endpoint* pelo terminal de API de sua região.
   ```
cf api <API-endpoint>
   ```
   {: pre}

|Terminal de API                            |Região          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | SUL dos EUA       |
| https://api.eu-gb.bluemix.net  | United Kingdom |
| https://api.au-syd.bluemix.net | Sydney         |

Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}.

  ```
cf login
  ```
  {: pre}

No diretório *get-started-node*, envie seu app por push para o {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

A implementação de seu aplicativo pode levar alguns minutos. Quando a implementação for concluída, você verá uma mensagem informando que o app está em execução. Visualize o app na URL listada na saída do comando push ou visualize o status de implementação do app e a URL, executando o comando a seguir:
  ```
cf apps
  ```
  {: pre}

É possível solucionar problemas de erros no processo de implementação usando o comando `cf logs <Your-App-Name> --recent`.
{: tip}

## 5. Inclua um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados NoSQL nesse aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione seu aplicativo clicando em seu nome na coluna **Nome**.
2. Clique em **Conexões** e, em seguida, em **Conectar novo**.
2. Na seção **Dados e Analytics**, selecione `Cloudant NoSQL DB` e, em seguida, crie o serviço.
3. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte. [Saiba mais...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Use o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Criaremos um arquivo JSON que armazenará as credenciais dos serviços que o aplicativo usará. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente `VCAP_SERVICES`.

1. No diretório `get-started-node`, crie um arquivo chamado `vcap-local.json` com o conteúdo a seguir:
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. Em seu navegador, acesse o {{site.data.keyword.Bluemix_notm}} e selecione **Aplicativos > _your app_ > Conexões > Cloudant > Visualizar credenciais**.

3. Copie e cole apenas a `URL` das credenciais no campo `URL` do arquivo `vcap-local.json`, substituindo **CLOUDANT_DATABASE_URL**.

4. Execute seu aplicativo localmente.
  ```
npm start  
  ```
  {: pre}

  Visualize seu app local em http://localhost:3000. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Os nomes que você incluir de qualquer um dos apps aparecerão em ambos quando os navegadores forem atualizados.

Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}
