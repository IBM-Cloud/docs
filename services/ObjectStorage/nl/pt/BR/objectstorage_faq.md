---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Perguntas frequentes {: #faq}

Esta FAQ fornece respostas às perguntas comuns sobre o serviço {{site.data.keyword.objectstorageshort}}.
{: shortdesc}


## Quais contas e planos de pagamento posso usar para o {{site.data.keyword.objectstorageshort}}? {: #account-payment}

O serviço {{site.data.keyword.objectstorageshort}} oferece duas opções de plano, Free e Standard. A [precificação](https://www.ibm.com/cloud-computing/bluemix/pricing/) varia dependendo do plano escolhido.

<table>
<caption> Tabela 1. Comparação dos planos Grátis e Padrão</caption>
  <tr>
    <th> Plano grátis </th>
    <th> Plano padrão </th>
  </tr>
  <tr>
    <td> Permite que exista somente uma instância de serviço por vez em uma organização do {{site.data.keyword.Bluemix_notm}} </td>
    <td> Instâncias de serviço ilimitadas </td>
  </tr>
  <tr>
    <td> Disponível para todos </td>
    <td> Disponível somente para contas pagas do {{site.data.keyword.Bluemix_notm}} e usuários internos da IBM </td>
  </tr>
  <tr>
    <td> Free </td>
    <td> Pague conforme o uso ou planos de pagamento de assinatura </td>
  </tr>
  <tr>
    <td> Inclui um limite de uso de armazenamento introdutório de 5 GB </td>
    <td> Armazenamento ilimitado </td>
  </tr>
</table>

**Atenção**: os usuários que trabalham com uma conta para teste
do {{site.data.keyword.Bluemix_notm}} podem usar o plano Free. Depois que o
tempo da sua avaliação expirar, a instância de serviço do
{{site.data.keyword.objectstorageshort}} associada será desativada, significando
que você não conseguirá acessar a conta de armazenamento. Após 30 dias, sua conta do
{{site.data.keyword.Bluemix_notm}} será limpa e todos os dados excluídos. Para
evitar a perda de dados, faça upgrade para uma
[Conta do {{site.data.keyword.Bluemix_notm}} paga](/docs/admin/account.html) assim que for possível.

## Como mudar meu plano? {: #changeplan}  
É possível fazer upgrade de instâncias criadas por meio de Beta ou no plano Grátis para o plano Padrão. A organização associada deve ser uma conta paga do {{site.data.keyword.Bluemix_notm}}. As
contas para teste com instâncias de armazenamento de objeto não podem ser atualizadas
para o plano Standard e não é possível fazer downgrade das instâncias no plano Standard para
outros planos. Ao fazer upgrade, sua instância de serviço e dados do cliente são movidos para o novo plano.

Para fazer upgrade:
1.	Na interface com o usuário do {{site.data.keyword.objectstorageshort}}, clique em **Plano**.
2.	Selecione **Padrão** como o novo plano e, em seguida, clique em **Salvar**.

É possível também [mudar seu plano de pagamento](/docs/pricing/index.html#changing) usando a interface da linha de comandos.

## Como serei encarregado e cobrado pelo meu uso do {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

O serviço do {{site.data.keyword.objectstorageshort}} cobra somente pelo que você usa.  Não há taxas nem compromissos para começar a usar o serviço. Você não é
cobrado por solicitações de API ou tráfego de rede de dados de entrada.

O {{site.data.keyword.objectstorageshort}} é faturado com base no seu uso de armazenamento dentro do ciclo de faturamento. Isso inclui todos os dados do objeto em contêineres que você criou dentro da organização do {{site.data.keyword.Bluemix_notm}}.

Um encargo de Transferência de dados de saída se aplica sempre que os dados são
lidos de qualquer contêiner de objeto por meio da rede pública. Toda a largura de banda
que é consumida no ciclo de faturamento é faturada como Largura de banda de saída pública.

Ao final do ciclo de faturamento, o {{site.data.keyword.Bluemix_notm}} fatura automaticamente o uso durante esse período. É possível visualizar seus encargos para o período atual de faturamento via relatório do {{site.data.keyword.Bluemix_notm}}.

## A minha região do {{site.data.keyword.Bluemix_notm}} e a minha região de
armazenamento são a mesma coisa? {: #region}

O serviço {{site.data.keyword.objectstorageshort}} suporta as regiões de
armazenamento Dallas e Londres. Essas regiões de armazenamento são independentes da região do {{site.data.keyword.Bluemix_notm}}, como sul do EUA e Reino Unido, na qual a instância de serviço {{site.data.keyword.objectstorageshort}} foi criada. Se
você criar uma instância na região Sul dos EUA do {{site.data.keyword.Bluemix_notm}}, será possível ler e gravar dados na região de armazenamento Dallas ou Londres. A região de armazenamento assume o padrão com base em sua região do {{site.data.keyword.Bluemix_notm}}. É possível alternar regiões selecionando outra região na lista suspensa na UI.
