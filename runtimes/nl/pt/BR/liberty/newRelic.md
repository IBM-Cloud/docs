---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Usando o New Relic
{: #new_relic}

*Última atualização: 23 de março de 2016*

New Relic é um serviço de terceiro que fornece
métricas de monitoramento para o seu aplicativo. Para obter mais
informações sobre o serviço que o New Relic oferece, consulte [New
Relic](http://newrelic.com/java).

De acordo com esta [documentação de instalação manual do agente Java](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation), os aplicativos Java que devem ser monitorados usando o serviço New Relic geralmente precisam ser empacotados e configurados com um agente New Relic e uma chave de licença da conta. No ambiente do IBM Bluemix, um contrato de licença e uma conta do New Relic podem ser obtidos criando uma instância de serviço no IBM Bluemix. Os aplicativos Java podem então ser ligados à instância do serviço New Relic e o buildpack do Liberty configura automaticamente o aplicativo que está pronto para ser monitorado pelo serviço New Relic.
Especificamente,
o buildpack:

* fornece ao aplicativo um agente do New Relic.
* obtém o nome do aplicativo e a chave de licença a partir das variáveis do ambiente de aplicativos VCAP_APPLICATION e VCAP_SERVICES.
* configura as propriedades e o modelo de configuração que é necessário pelo agente do
New Relic.

Consulte a configuração de amostra que é gerada pelo buildpack
do Liberty para o aplicativo:

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: #codeblock}

## Incluir um novo serviço New Relic
{: #add_new_relic}

Para que um aplicativo Java existente seja monitorado com o New Relic no IBM Bluemix, siga estas etapas.
1. Crie uma instância do serviço New Relic no IBM Bluemix.
```
    $ cf create-service newrelic standard mynewrelic
```
{: #codeblock}

2. Implemente seu aplicativo no IBM Bluemix com o serviço New Relic.  Veja o manifest do aplicativo
de amostra a seguir:
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. Acesse o painel do New Relic para seu aplicativo diretamente a partir do painel do IBM Bluemix de seu aplicativo.

### Incluir um serviço New Relic fornecido pelo usuário
{: #add_user_provided_new_relic}

Se você tiver uma conta e uma chave de licença existente do New Relic, poderá ligar o serviço
New Relic existente ao seu aplicativo usando um "serviço fornecido pelo usuário".

1. Crie uma instância de serviço fornecida pelo usuário usando sua chave de licença
existente.  Por exemplo, se a sua chave de licença existente for 1234567, será possível usar a CLI do CF para "create-user-provided-service" e fornecer a chave de licença 1234567 no prompt como a seguir:
```
    $ cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
```
{: #codeblock}

2. Implemente seu aplicativo no IBM Bluemix com a instância do serviço New Relic fornecida pelo usuário.  A seguir
está um manifest do aplicativo de amostra que usa uma instância do serviço New Relic
fornecida pelo usuário:
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. Acesse o painel do New Relic para visualizar as métricas do aplicativo.

A configuração automática do serviço New Relic é diferente da configuração automática de outros serviços, pois ela é um serviço gerenciado por
contêiner que é disponibilizada por meio da estrutura do buildpack.  Como ela é disponibilizada por meio
da estrutura, a configuração automática desse serviço difere de outros serviços de três maneiras:
* Fazer opt-out não é uma opção.
* A integração de serviço depende do agente do New Relic, um agente Java. Portanto, ela é configurada por meio de opções Java, em vez de variáveis de nuvem no arquivo server.xml.
* A configuração depende de VCAP_SERVICES e VCAP_APPLICATION.

# rellinks
## geral
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
