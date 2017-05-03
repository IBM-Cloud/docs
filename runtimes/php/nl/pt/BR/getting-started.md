---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Introdução ao PHP no Bluemix
{: #getting_started}

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}! Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo esse guia, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados do {{site.data.keyword.Bluemix}} em seu app.

## Pré-requisito
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [PHP ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://php.net/downloads.php){: new_window}
* [Composer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://getcomposer.org/download/){: new_window}

## 1. Clone o app de amostra
{: #clone}

Agora você está pronto para começar a trabalhar com o app. Clone o repositório e
mude o diretório para onde o app de amostra está localizado.
  ```
git clone https://github.com/IBM-Bluemix/get-started-php
  ```
  {: pre}
  ```
cd get-started-php
  ```
  {: pre}

## 2. Execute o app localmente

Instale as dependências
```
php composer.phar install
```
{: pre}

Execute o app
  ```
php -S localhost:8000
  ```
  {: pre}

Visualize seu app em: http://localhost:8000

## 3. Prepare o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-php`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedPHP` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedPHP
   random-route: true
   memory: 128M
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras. Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência. [Saiba mais...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Implemente o app
 {: #deploy}

É possível usar a CLI do Cloud Foundry para implementar apps.

Escolha seu terminal de API
   ```
cf api <API-endpoint>
   ```
   {: pre}

Substitua o *API-endpoint* no comando por um terminal de API da lista a seguir.

|URL                             |Região          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | SUL dos EUA       |
| https://api.eu-gb.bluemix.net  | United Kingdom |
| https://api.au-syd.bluemix.net | Sydney         |

Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}

   ```
cf login
   ```
   {: pre}

 No diretório *get-started-php*, envie seu app por push para o {{site.data.keyword.Bluemix_notm}}
   ```
cf push
   ```
   {: pre}

 Isso pode levar um minuto. Se houver um erro no processo de implementação, será
possível usar o comando `cf logs <Your-App-Name> --recent` para
solucionar problemas.

 Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução. Visualize o app na URL listada na saída do comando push. Também é possível emitir o comando
  ```
cf apps
  ```
  {: pre}
para visualizar o status dos apps e ver a URL.

## 5. Inclua um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados NoSQL nesse aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Efetue login no {{site.data.keyword.Bluemix_notm}} em seu navegador. Procure o `Painel`. Selecione seu aplicativo clicando em seu nome na coluna `Nome`.
2. Clique em `Conexões` e, em seguida, em `Conectar novo`.
3. Na seção `Dados e Analytics`, selecione `Cloudant NoSQL DB` e `Criar` o serviço.
4. Selecione `Remontar` quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte. [Saiba mais...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Use o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Criaremos um arquivo json que armazenará as credenciais dos serviços que o aplicativo usará. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente VCAP_SERVICES.

1. Crie um arquivo chamado `.env` no diretório `get-started-php` com o conteúdo a seguir:
  ```
  CLOUDANT_HOST=
  CLOUDANT_USERNAME=
  CLOUDANT_PASSWORD=
  ```

2. De volta na UI do {{site.data.keyword.Bluemix_notm}}, selecione seu App -> Conexões -> Cloudant -> Visualizar credenciais

3. Copie e cole os valores dos campos `CLOUDANT_HOST`, `CLOUDANT_USERNAME` e `CLOUDANT_PASSWORD` no arquivo `.env` e salve as mudanças. O resultado será algo como:
  ```
  CLOUDANT_HOST=abc...yz.cloudant.com
  CLOUDANT_USERNAME=abc...yz
  CLOUDANT_PASSWORD=445d...d1a
  ```

4. Execute seu aplicativo localmente.
  ```
php -S localhost:8000
  ```
  {: pre}

  Visualize seu app em: http://localhost:8000. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Visualize o app {{site.data.keyword.Bluemix_notm}} na URL listada na saída do comando push acima. Os nomes que você incluir de qualquer um dos apps deverão aparecer em ambos quando os navegadores forem atualizados.

Lembre-se, se você não precisar do app em tempo real, pare-o para não incorrer em encargos inesperados.
{: tip}  
