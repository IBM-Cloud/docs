---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Gerenciando classificadores com o kit de ferramentas
{: #managing-toolkit}

É possível gerenciar seus dados de treinamento e classificadores usando o aplicativo da web {{site.data.keyword.nlclassifierfull}} Toolkit. O kit de ferramentas fornece uma visualização unificada de todos os classificadores que estão em execução na mesma instância de serviço do {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Esta é uma liberação beta do kit de ferramentas. A versão beta desse kit de ferramentas poderá não ser suportada após uma nova liberação ou depois que o kit de ferramentas sair do status beta. Não use o kit de ferramentas para uso de produção.

A interface da web do kit de ferramentas simplifica o modo de treinamento e teste de um classificador. Os especialistas de seu domínio podem usar o kit de ferramentas para destacar a qualidade de seus dados de treinamento.

## Obtendo Acesso
{: #getting-access}

É possível localizar um link para o kit de ferramentas na página de painel de serviço do {{site.data.keyword.Bluemix_notm}} para sua instância do {{site.data.keyword.nlclassifiershort}}.

### Acessando o kit de ferramentas sozinho

Para localizar o link para o kit de ferramentas, siga estas etapas para chegar ao painel de **serviço** do {{site.data.keyword.Bluemix_notm}}:

1. Abra o quadro do serviço {{site.data.keyword.nlclassifiershort}} efetuando login no [Painel do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/dashboard/services){: new_window}.

	-  Na área **Serviços**, clique no quadro do serviço {{site.data.keyword.nlclassifiershort}} para abrir o painel da instância. (Se você não tiver um quadro de serviço, [crie uma instância ![Ícone de link externo](../../icons/launch-glyph.svg)](https://console.{DomainName}/catalog/services/natural-language-classifier/){: new_window} do serviço {{site.data.keyword.nlclassifiershort}}.)
1. No painel de serviço, clique em **Acessar o kit de ferramentas beta**.

	Marque a URL para obter facilidade de acesso ao kit de ferramentas mais tarde.
 {: tip}

### Fornecendo acesso ao kit de ferramentas para outros

É possível permitir que outros usem seu kit de ferramentas, incluindo-o no {{site.data.keyword.Bluemix_notm}}.

1.  No {{site.data.keyword.Bluemix_notm}}, clique em **Conta > Convidar membros da equipe**.
1.  Selecione a organização que contém seu serviço classificador e clique em **Avançar**.
1.  Selecione o espaço que contém seu serviço classificador.
1.  Selecione a função de espaço **Desenvolvedor**. Para obter detalhes sobre funções, veja [Gerenciando membros da equipe e funções](/docs/admin/users_roles.html).
1.  Insira o endereço de e-mail do usuário e clique em **Enviar**.
1.  Em um e-mail separado, envie a URL de seu kit de ferramentas (que você marcou anteriormente) para os usuários.

## Utilizações de Exemplo
{: #example-uses}

Nesses exemplos, você cria e modifica dados de treinamento, testa um classificador interativamente ou por meio de um conjunto de dados de teste, além de atualizar dados de treinamento dos resultados.

### Criar dados de treinamento no kit de ferramentas

Familiarize-se com o kit de ferramentas do {{site.data.keyword.nlclassifiershort}} criando um pequeno conjunto de dados de treinamento com o kit de ferramentas.

Antes de ser possível criar um classificador, você precisa de dados de treinamento. É possível criar os dados digitando textos e classes ou é possível fazer upload de seus dados de treinamento de um arquivo CSV que corresponda ao [formato de arquivo](/docs/services/natural-language-classifier/using-your-data.html).
1. Na página **Dados de treinamento** do kit de ferramentas, inclua um texto. Se não puder pensar em nada, inclua "Onde está o ATM mais próximo?". 
1. Designe uma classe ao texto digitando nele. Para o exemplo de ATM, digite "local".
1. Continue incluindo textos e classes em seus dados de treinamento. É possível designar classes a textos das maneiras a seguir:
	-   Selecione uma classe clicando nela e, em seguida, clique em **Incluir texto**. Ou selecione um texto e, em seguida, clique em **Designar classes**.
	-   Selecione uma classe e, em seguida, arraste um texto para ela. Ou selecione um texto e, em seguida, arraste uma classe para ele.

	É possível trabalhar em mais de uma classe ou texto de cada vez pressionando Ctrl e clicando no texto ou na classe (pressione Command em um Mac). Experimente-os.
1. Depois de ter trabalhado com seus dados de treinamento por um tempo, clique em **Fazer download de dados de treinamento** para salvar os dados como um backup.

	Também é possível fazer upload desse arquivo no kit de ferramentas para trabalhar com os dados de treinamento novamente mais tarde.
 {: tip}
1. Quando você tiver designado classes a pelo menos cinco textos, será possível criar um classificador usando esses dados de treinamento. Clique em **Criar classificador**. O {{site.data.keyword.watson}} começa a treinar o classificador.

### Testar seu classificador e atualizar os dados de treinamento

Depois que um classificador é treinado e fica disponível, é possível verificar como ele classifica os textos que ainda não viu. É possível testar vários textos e melhorar os dados de treinamento, incluindo as respostas incorretas ou de baixa confiança.

1.  Na página **Classificadores**, clique em **Testar e melhorar o desempenho** para o classificador que você deseja testar.
1.  Na página **Melhorar o desempenho**, insira um texto que não esteja em seus dados de treinamento e clique em **Classificar**. O {{site.data.keyword.watson}} retorna classes relevantes e seus níveis de confiança.
1.  Inclua mais textos para testar o desempenho.
1.  Revise as respostas. Sinalize ou aprove os resultados que você deseja incluir nos dados de treinamento:
	- Se a classificação não estiver correta, sinalize o resultado.
	- Se a resposta estiver correta, mas a confiança for baixa, inclua-a nos dados de treinamento clicando em **Aprovar**.
1.  Clique em **Incluir nos dados de treinamento** para incluir as respostas aprovadas e sinalizadas nos dados de treinamento.
1.  Na página **Dados de treinamento**, revise e atualize as classes que estão designadas aos textos sinalizados.
1.  Para atualizar seu classificador com esses novos dados de treinamento, você criará outro. Clique em **Criar classificador**. Depois de treinado, teste o novo classificador para ver como ele melhorou.

### Fazer upload dos dados para testar seu classificador

Inserir textos para classificar um por um é efetivo para testes rápidos. No entanto, se você tiver um *conjunto de testes*, será possível fazer upload do conjunto para o kit de ferramentas para classificar vários ao mesmo tempo. Um conjunto de testes é um grupo de textos de exemplo que não estão nos dados de treinamento. Use o conjunto para verificar o desempenho do classificador.

1.  Crie um arquivo de conjunto de testes:
	- O arquivo pode usar o mesmo formato dos dados de treinamento (ou seja, ele pode incluir as classes corretas) ou incluir apenas textos, um em cada linha. Certifique-se de que os textos (e as classes) sigam os requisitos do [formato de arquivo](/docs/services/natural-language-classifier/using-your-data.html).
    -   Salve o arquivo com uma extensão `.csv`.
1.  Na página **Classificadores**, clique em **Testar e melhorar o desempenho** para o classificador que você deseja testar.
1.  Na página **Melhorar o desempenho**, clique em **Usar dados de teste**. O {{site.data.keyword.watson}} faz upload dos dados, classifica cada texto e retorna uma resposta.
1.  Compare as respostas com a classificação correta e também verifique a baixa confiança.
1.  Melhore os dados de treinamento incluindo mais exemplos. Não inclua exemplos que existirem em seu conjunto de testes se desejar continuar usando-o para avaliar o desempenho do classificador.
