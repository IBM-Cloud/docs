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

Depois de integrar sua API para que seja gerenciada e monitorada pelo sistema de gerenciamento de API, é possível visualizar e modificar as configurações da API. Se você não integrou sua API, deve-se integrar uma concluindo o procedimento em [Criando APIs de ações do {{site.data.keyword.openwhisk_short}}](manage_openwhisk_apis.html). 

Para gerenciar as configurações para sua API, conclua as etapas a seguir:

Se você criou uma nova API e ela já estiver aberta na interface, será possível ignorar as três primeiras etapas.

1. Selecione a API que você deseja gerenciar selecionando uma ação no Painel do serviço {{site.data.keyword.openwhisk_short}}, se as informações para sua API já não estiverem sendo exibidas.
2. Selecione a guia **APIs**, se necessário.
3. Selecione a API que você deseja gerenciar, se necessário. Quando uma conexão é estabelecida, as seleções a seguir estão disponíveis para você visualizar e atualizar:
    * Resumo
    * Definition
    * Compartilhamento
    * Explorador de API
4. Selecione a régua de controle Expor API gerenciada para ativá-la e expor sua API. Nota: algumas das configurações não podem ser definidas quando a API não está exposta.  

## Resumo de configurações para APIs
{: #overview_api}

A guia Resumo é selecionada por padrão quando você seleciona uma API e é dividida em duas seções:
* Propriedades - Na seção Propriedades, é possível visualizar as informações a seguir:
    * Informações básicas sobre sua API
	* Diretivas de segurança
	* Informações de limite de taxa
    * Detalhes do Compartilhamento
* Seção Analítica e criação de log - na seção Analítica e criação de log, é possível visualizar as estatísticas a seguir:
	* Número de respostas e o tempo médio de resposta durante o último intervalo de tempo especificado
    * Número de chamadas API por minuto em formato gráfico
    * Últimas 100 respostas na tabela Log de resposta
	
O gráfico *Respostas* mostra uma representação gráfica de quantas respostas sua API recebeu e o detalhamento do status das respostas. Isso pode ajudá-lo a determinar se você está recebendo uma maioria de respostas de erro. A maioria de respostas de erro pode indicar que você tem mais tráfego do que é permitido em suas configurações de taxa. É possível ver um detalhamento numérico das respostas por código de resposta, passando o mouse sobre o ícone de informações. Os códigos de resposta a seguir são comuns:
* 200 OK
* 201 Criado
* 302 Localizado
* 304 Não modificado
* 400 Solicitação ruim
* 401 Desautorizado
* 403 Proibido
* 500 Erro interno do servidor
* 503 Serviço indisponível

A tabela Log de resposta contém detalhes individuais das últimas 100 respostas. É possível classificar as informações de acordo com as entradas em uma coluna selecionando o título da coluna. É possível procurar entradas específicas na tabela Log de resposta usando a barra *Procurar respostas*. Mais informações estão disponíveis para um evento selecionando-o ou selecionando **Visualizar detalhes** na lista do menu de opções (três pontos verticais) que está ao lado da entrada.


## Editando configurações da API
{: #settings_api}

Na guia **Definição**, é possível atualizar informações básicas sobre sua API. Essas informações incluem a documentação, o nome e a URL base. Use a seção Segurança e limitação de taxa para especificar um limite de chamada e intervalo para assegurar que somente uma certa quantidade de chamadas sejam feitas por segundo, minuto ou hora. Também é possível requerer autenticação para criar chamadas API para evitar uso indesejado de seus dados ou para reunir estatísticas sobre a API.

Para mudar as configurações para uma API, conclua as etapas a seguir:

1. No painel de gerenciamento de API, clique na guia **Definição**.
2. É possível nomear ou atualizar o nome de sua API e importar uma definição de API na seção Informações da API.
3. Na seção Segurança e limitação de taxa, é possível atualizar as políticas a seguir:
    * Requerer chave API - especifica se a chamada API pode ser processada somente quando a chave API correta é fornecida. A configuração padrão não requer uma chave adicional.
    * Método de segurança - quando a opção Chave API é selecionada, especifica se o processamento da API requer somente a chave API ou requer ambos, a chave API e o segredo API.
    * Local da chave e do segredo API - dependendo de sua configuração para o método, especifica como suas informações de segurança de API são incluídas na chamada. Os nomes de Chamada especificam como as informações de segurança são identificadas.
    * Limitar a taxa de chamada API - configura o número de chamadas API que são permitidas durante um intervalo de tempo especificado, com a opção de configurá-lo para cada chave. Observe que um tipo de burst do método de limitação de taxa é usado. A taxa média das chamadas API é calculada no intervalo de tempo total que você especificou na taxa. Se a taxa de chamadas de API durante um intervalo exceder a taxa média das chamadas API, pode haver um período de chamadas negadas até o limite de tempo que você especificou na taxa.   
    * Provedor OAuth - assegura que os usuários com os parâmetros de segurança corretos possam acessar suas APIs impingindo OAuth por meio das credenciais de login social de provedores como Google, Facebook, IBM e GitHub.
4. Ativar CORS - o Cross-origin requests (CORS) ativa algumas solicitações limitadas de um domínio diferente.
5. Clique **Salvar.**

## Compartilhando APIs
{: #share_api}

É possível compartilhar APIs com outros usuários dentro ou fora de sua organização do {{site.data.keyword.Bluemix_notm}}.

Ao compartilhar APIs com outros, dentro ou fora de sua organização do {{site.data.keyword.Bluemix_notm}}, é possível criar chaves para as APIs. Cada API gerenciada suporta 5 chaves que podem ser criadas e designadas a essa API. Enviando uma chave exclusiva a um indivíduo ou empresa, é possível rastrear algumas estatísticas sobre como essa API é usada. Por exemplo, é possível rastrear o número ou chamadas para a API por essa pessoa ou empresa.

Também é possível limitar o número de chamadas na chave ledisable a key ou limitar as chamadas de uma chave. Isso pode ser útil durante teste, balanceamento de carga de trabalho, monetização ou para direcionar algumas situações de segurança.  

1. No painel de gerenciamento de API, clique na guia **Compartilhamento**.
2. Na área "Compartilhamento na organização do {{site.data.keyword.Bluemix_notm}}", selecione **Compartilhar API com todos os usuários em minha organização do Bluemix** se você desejar que sua API fique disponível para outros com acesso à sua organização do {{site.data.keyword.Bluemix_notm}}. Isso deve ser selecionado para gerar uma chave.
3. Clique em **Criar chave API** para criar uma chave exclusiva para sua API. A caixa de diálogo Criar chave API é exibida. A chave API é gerada automaticamente.
4. Use a chave API para determinar qual usuário está acessando o API enviando a um usuário uma chave exclusiva. O gateway pode determinar qual chave (e cliente) está gerando a chamada.
5. Clique no ícone **Menu** (três pontos verticais) ao lado da chave para Editar ou Excluir essa chave API.

Na seção Compartilhamento fora da organização do {{site.data.keyword.Bluemix_notm}}, é possível compartilhar sua API com usuários que não têm uma conta do {{site.data.keyword.Bluemix_notm}}. Esse método de compartilhamento fornece um link direto para visualizar as informações sobre a API no API Explorer. A API contém um botão para executar a API na visualização API Explorer. Para solicitar um link para sua API, conclua as etapas a seguir:

1. Dentro da seção "Compartilhamento fora da organização do {{site.data.keyword.Bluemix_notm}}". Clique em **Criar chave API**. A caixa de diálogo Criar chave API é exibida.
     Observe que o usuário tem um segredo que não é possível controlar.
2. Forneça um nome exclusivo para a chave API.
3. Selecione **Criar chave**. 
4. Envie o Link de portal da API para o cliente sem uma conta do {{site.data.keyword.Bluemix_notm}}. A chave API e o segredo (se for usado) são incluídos no link, portanto ainda é possível determinar qual chave gerou o link.
  
O link de documentação da API abre a API na guia **API Explorer**.

## Visualizando e testando com o API Explorer
{: #explore_api}

Selecione a guia API Explorer para visualizar HTML gerado de seu doc Swagger. 

O API Explorer mostra todas as ações e documentação de API que se aplicam à API. É possível visualizar as operações e ações, suas descrições e testar a API por meio da UI. Também é possível fazer download do doc Swagger para reutilizar seu conteúdo.

Para testar a API, conclua as etapas a seguir:
1. *Exemplos* é selecionado por padrão. Isso mostra um exemplo do código para a API selecionada.
2. Mude o formato de exemplo, se necessário, selecionando um idioma no menu ao lado do idioma especificado. 
3. Selecione **Tente isso**.
4. Selecione **Chamar operação**. 

A resposta para a solicitação é exibida.   
