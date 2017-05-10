---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acessando mais recursos de gerenciamento de API
{: #upgrade}

O gerenciamento de API permite controlar taxas de chamada, OAuth e analítica de visualização. É possível ter maior controle de gerenciamento sobre as APIs fazendo upgrade para o serviço {{site.data.keyword.apiconnect_full}}. O serviço {{site.data.keyword.apiconnect_short}} fornece mais opções de políticas de segurança e maior controle sobre os limites de taxa. Além disso, você será capaz de configurar um Portal do Desenvolvedor completamente customizável para que seja possível socializar suas APIs e se envolver com a comunidade do desenvolvedor. Outros benefícios incluem:
* Gerenciamento do Ciclo de Vida
* APIs compostas
* Integração de Serviços da Web
* Mediação de protocolo
* Geração de API do esquema
* Desenvolvimento de microsserviços

Migrar para o serviço {{site.data.keyword.apiconnect_short}} é fácil e você não precisa recriar nenhuma das APIs que estão sendo gerenciadas com o gerenciamento de API.

## Migrando APIs para o {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

Se você decidir fazer upgrade para o {{site.data.keyword.apiconnect_full}}, será necessário migrar suas APIs do gerenciamento de API para o serviço {{site.data.keyword.apiconnect_short}} concluindo as etapas a seguir para cada uma de suas APIs: 

1. Faça download do documento Swagger para a API por meio do gerenciamento de API.
    1. Abra seu app e selecione **Gerenciamento de API**.
	2. Selecione a guia **API Explorer**. Uma lista de suas APIs que estão relacionadas a esse projeto é exibida.
    2. Faça download do documento Swagger para sua API selecionando o ícone ao lado do nome da API.
2. Crie e prepare a instância do {{site.data.keyword.apiconnect_short}}. 
    1. Crie uma instância do serviço {{site.data.keyword.apiconnect_short}} por meio do catálogo do {{site.data.keyword.Bluemix_notm}}.
	2. Selecione seu plano.
	3. Selecione **+Incluir** para criar um catálogo.
	4. Insira um nome de Exibição e um nome para seu catálogo e selecione **Incluir**.
	5. Selecione o catálogo que você criou.
3. Importe o documento Swagger para sua instância do {{site.data.keyword.apiconnect_short}} concluindo as etapas a seguir:
	1. No painel do serviço {{site.data.keyword.apiconnect_short}}, selecione **Navegar para... (>>)** > **Rascunhos** no menu.
	2. Selecione a guia APIs.
	3. Selecione **+Incluir** > **Importar API de um arquivo ou URL**.
	4. Localize e selecione o arquivo Swagger que você transferiu por download do gerenciamento de API. Selecione **Abrir**.
	5. Selecione **Importar** para importar sua API para o serviço {{site.data.keyword.apiconnect_short}}.
4. Especifique as configurações para sua API.
    1. Selecione **Criar produto**.
	2. Selecione o produto que você criou para visualizar suas configurações.
	3. Configure o limite de taxa para a API.
	4. Configure a camada para a API.
5. Inclua o terminal para a API, se necessário.
    1. Selecione a API.
	2. Selecione a guia Conjunto.
	3. Inclua o terminal, se ele ainda não estiver especificado.
	
 Depois de migrar suas APIs, você será capaz de acessar todos os recursos de gerenciamento de API abrindo o tile do serviço {{site.data.keyword.apiconnect_short}} e também por meio do Painel do {{site.data.keyword.Bluemix_notm}}. 

 
