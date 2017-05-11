---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciar APIs
{: #manage_apis}

Depois de integrar sua API para que seja gerenciada e monitorada pelo sistema de gerenciamento de API, é possível visualizar e modificar as configurações da API. Se você não tiver integrado sua API, deverá integrar uma concluindo o procedimento em [Criando APIs por meio de ações do {{site.data.keyword.openwhisk_short}}](manage_openwhisk_apis.html). 

Para gerenciar as configurações para sua API, conclua as etapas a seguir:

Se você tiver criado uma nova API e ela já estiver aberta na interface, será possível ignorar as três primeiras etapas.

1. Selecione a API que você deseja gerenciar selecionando uma ação no Painel de serviço do {{site.data.keyword.openwhisk_short}}, se as informações para sua API ainda não forem exibidas.
2. Selecione a guia **APIs**, se necessário.
3. Selecione a API que você deseja gerenciar, se necessário. Quando uma conexão é estabelecida, as seleções a seguir estão disponíveis para você visualizar e atualizar:
    * Resumo
    * Definição
    * Compartilhamento
    * Explorador de API
4. Selecione a régua de controle Expor API Gerenciada para ativá-la e expor sua API. Nota: algumas das configurações não podem ser configuradas quando a API não está exposta.  

## Resumo de configurações para APIs
{: #overview_api}

A guia Resumo é selecionada por padrão quando você seleciona uma API e é dividida em duas seções:
* Propriedades - Na seção Propriedades é possível visualizar as informações a seguir:
    * Informações básicas sobre sua API
	* Diretivas de segurança
	* Informações de limite de taxa
    * Detalhes do compartilhamento
* Seção Analítica e Criação de Log - Na seção Analítica e Criação de Log, é possível visualizar as estatísticas a seguir:
	* Número de respostas e o tempo médio de resposta durante o último intervalo de tempo especificado
    * Número de chamadas de API por minuto no formato de gráfico
    * Últimas 100 respostas na tabela Log de Resposta
	
O gráfico *Respostas* mostra uma representação rápida de quantas respostas a API recebeu e o detalhamento do status das respostas. Isso pode ajudá-lo a determinar se você está recebendo a maioria das respostas de erro. A maioria das respostas de erro pode indicar que você tem mais tráfego do que o permitido em suas configurações de taxa. É possível ver um detalhamento numérico das respostas por código de resposta ao passar o mouse sobre o ícone de informações. Os códigos de resposta a seguir são comuns:
* 200  OK
* 201  Criado
* 302  Localizado
* 304  Não Modificado
* 400  Solicitação Inválida
* 401  Desautorizado
* 403  Proibido
* 500  Erro do Servidor Interno
* 503  Serviço Indisponível

A tabela Log de Resposta contém detalhes individuais das últimas 100 respostas. É possível classificar as informações de acordo com as entradas em uma coluna selecionando o título da coluna. É possível procurar por entradas específicas na tabela Log de Resposta usando a barra *Procurar respostas*. Mais informações estão disponíveis para um evento selecionando-o ou selecionando **Visualizar Detalhes** na lista de menu de opções (três pontos verticais) que está ao lado da entrada.


## Editando configurações da API
{: #settings_api}

Na guia **Definição**, é possível atualizar informações básicas sobre sua API. Essas informações incluem a documentação, o nome e a URL base. Use a seção Segurança e Limitação de Taxa para especificar um limite de chamada e de intervalo para assegurar que seja feita apenas certa quantidade de chamadas por segundo, minuto ou hora. Você também pode requerer autenticação para criar chamadas de API para evitar o uso indesejado de seus dados ou para reunir estatísticas sobre a API.

Para mudar as configurações para uma API, conclua as etapas a seguir:

1. No painel de gerenciamento de API, clique na guia **Definição**.
2. É possível nomear ou atualizar o nome de sua API e importar uma definição de API na seção Informações da API.
3. Na seção Segurança e Limitação de Taxa, é possível atualizar as políticas a seguir:
    * Requerer chave API - Especifica se a chamada da API pode ser processada apenas quando a chave API correta é fornecida. A configuração padrão não requer uma chave adicional.
    * Método de segurança - Quando a opção da chave API é selecionada, especifica se o processamento da API requer apenas a chave API ou requer a chave API e o segredo da API.
    * Local da chave API e do segredo - Dependendo de sua configuração para o método, especifica como as informações de segurança da API são incluídas na chamada. Os nomes de chamada especificam como as informações de segurança são identificadas.
    * Limitar taxa de chamada da API - Configura o número de chamadas de API que são permitidas durante um intervalo de tempo especificado, com a opção de configurar isso para cada chave. Observe que é usado um tipo burst de método de limitação de taxa. A taxa média das chamadas de API é calculada pelo intervalo de tempo total especificado na taxa. Se a taxa de chamadas de API durante um intervalo exceder a taxa média das chamadas de API, poderá haver um período de chamadas negadas até o limite de tempo que você especificou na taxa.   
    * Provedor OAuth - Assegura que os usuários com os parâmetros de segurança corretos possam acessar suas APIs impingindo OAuth por meio de credenciais de login sociais de provedores como Google, Facebook, IBM e GitHub.
4. Ativar CORS - Solicitações de Origem Cruzada (CORS) permite algumas solicitações limitadas por meio de um domínio diferente.
5. Clique em **Salvar**.

## Compartilhando APIs
{: #share_api}

É possível compartilhar APIs com outros usuários dentro ou fora de sua organização do {{site.data.keyword.Bluemix_notm}}.

Ao compartilhar suas APIs com outros, dentro ou fora de sua organização do {{site.data.keyword.Bluemix_notm}}, é possível criar chaves para suas APIs. Cada API gerenciada suporta 5 chaves que podem ser criadas e designadas a essa API. Ao enviar uma chave exclusiva a um indivíduo ou empresa, você pode rastrear algumas estatísticas sobre como essa API é usada. Por exemplo, é possível rastrear o número de chamadas para sua API por essa pessoa ou empresa.

Também é possível limitar o número de chamadas na chave, desativar uma chave ou limitar as chamadas por meio de uma chave. Isso pode ser útil durante o teste, o balanceamento de carga, a monetização ou para tratar algumas situações de segurança.  

1. No painel de gerenciamento de API, clique na guia **Compartilhamento**.
2. Dentro da área "Compartilhamento dentro da Organização do {{site.data.keyword.Bluemix_notm}}", selecione **Compartilhar API com todos os usuários em minha organização do Bluemix** se você deseja que sua API esteja disponível para outros com acesso à sua organização do {{site.data.keyword.Bluemix_notm}}. Isso deve ser selecionado para gerar uma chave.
3. Clique em **Criar Chave API** para criar uma chave exclusiva para sua API. A caixa de diálogo Criar Chave API é exibida. A chave API é gerada automaticamente.
4. Use a chave API para determinar qual usuário está acessando a API enviando uma chave exclusiva ao usuário. O gateway pode determinar qual chave (e cliente) está gerando a chamada.
5. Clique no ícone **Menu** (três pontos verticais) ao lado da chave para Editar ou Excluir essa chave API.

Na seção Compartilhamento fora da organização do {{site.data.keyword.Bluemix_notm}}, é possível compartilhar sua API com usuários que não possuem uma conta do {{site.data.keyword.Bluemix_notm}}. Esse método de compartilhamento fornece um link direto para visualizar as informações sobre a API no Explorador de API. A API contém um botão para executar a API na visualização Explorador de API. Para solicitar um link para sua API, conclua as etapas a seguir:

1. Dentro da seção "Compartilhamento fora da organização do {{site.data.keyword.Bluemix_notm}}". Clique em **Criar Chave API**. A caixa de diálogo Criar Chave API é exibida. Observe que o usuário tem um segredo que você não pode controlar.
2. Forneça um nome exclusivo para a chave API.
3. Selecione **Criar chave**. 
4. Envie o Link do Portal da API ao cliente sem uma conta do {{site.data.keyword.Bluemix_notm}}. A chave API e o segredo (se ele for usado) são incluídos no link, portanto, ainda é possível determinar qual chave gerou o link.
  
O link da documentação da API abre a API na guia **Explorador de API**.

## Visualizando e testando com o Explorador de API
{: #explore_api}

Selecione a guia Explorador de API para visualizar o HTML gerado por meio de seu doc. Swagger. 

O Explorador de API mostra todas as ações da API e documentação que se aplicam à API. É possível visualizar as operações e ações, suas descrições e testar a API da IU. Também é possível fazer download do documento Swagger para reutilizar seu conteúdo.

Para testar a API, conclua as etapas a seguir:
1. *Exemplos* é selecionado por padrão. Isso mostra um exemplo do código para a API selecionada.
2. Mude o formato de exemplo, se necessário, selecionando uma linguagem do menu ao lado da linguagem especificada. 
3. Selecione **Testar**.
4. Selecione **Chamar operação**. 

A resposta para a solicitação é exibida.   
