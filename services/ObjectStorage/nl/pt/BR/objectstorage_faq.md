---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Perguntas frequentes {: #faq}

*Última atualização: 19 de outubro de 2016*
{: .last-updated}

Esta FAQ fornece respostas às perguntas comuns sobre o serviço {{site.data.keyword.objectstorageshort}}.
{: shortdesc}


## Quais contas e planos de pagamento posso usar para o {{site.data.keyword.objectstorageshort}}? {: #account-payment}

O serviço {{site.data.keyword.objectstorageshort}} oferece duas opções de plano, Free e Standard. A [precificação](https://console.ng.bluemix.net/pricing/) varia dependendo do plano escolhido.

<table>
  <tr>
    <th> Plano grátis </th>
    <th> Plano padrão </th>
  </tr>
  <tr>
    <td> Permite que exista somente uma instância de serviço por vez em uma organização do {{site.data.keyword.Bluemix_notm}} </td>
    <td> Instâncias de serviço ilimitadas</td>
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

*Tabela 1: Comparação dos planos Free e Standard*

**Atenção**: os usuários que trabalham com uma conta para teste
do {{site.data.keyword.Bluemix_notm}} podem usar o plano Free. Depois que o
tempo da sua avaliação expirar, a instância de serviço do
{{site.data.keyword.objectstorageshort}} associada será desativada, significando
que você não conseguirá acessar a conta de armazenamento. Após 30 dias, sua conta do
{{site.data.keyword.Bluemix_notm}} será limpa e todos os dados excluídos. Para
evitar a perda de dados, faça upgrade para uma
[Conta do {{site.data.keyword.Bluemix_notm}} paga](https://new-console.ng.bluemix.net/docs/admin/account.html) assim que for possível.

## Como mudar meu plano? {: #changeplan}  
É possível fazer upgrade de instâncias criadas por meio de Beta ou no plano Grátis para o plano Padrão. A organização associada deve ser uma conta paga do {{site.data.keyword.Bluemix_notm}}. As
contas para teste com instâncias de armazenamento de objeto não podem ser atualizadas
para o plano Standard e não é possível fazer downgrade das instâncias no plano Standard para
outros planos. Ao fazer upgrade, sua instância de serviço e dados do cliente são movidos para o novo plano.

Para fazer upgrade:
1.	Na interface com o usuário do {{site.data.keyword.objectstorageshort}}, clique em **Plano**.
2.	Selecione **Padrão** como o novo plano e, em seguida, clique em **Salvar**.

É possível também [mudar seu plano de pagamento](../../pricing/index.html#changing) usando a interface da linha de comandos.

## Como serei encarregado e cobrado pelo meu uso do {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

O serviço do {{site.data.keyword.objectstorageshort}} cobra somente pelo que você usa.  Não
há taxas de configuração ou compromissos para começar a usar o serviço. Você não é
cobrado por solicitações de API ou tráfego de rede de dados de entrada.

O {{site.data.keyword.objectstorageshort}} é faturado com base no seu uso de armazenamento dentro do ciclo de faturamento. Isso inclui todos os dados do objeto em contêineres que você criou dentro da organização do {{site.data.keyword.Bluemix_notm}}.

Um encargo de Transferência de dados de saída se aplica sempre que os dados são
lidos de qualquer contêiner de objeto por meio da rede pública. Toda a largura de banda
que é consumida no ciclo de faturamento é faturada como Largura de banda de saída pública.

Ao final do ciclo de faturamento, o {{site.data.keyword.Bluemix_notm}} fatura automaticamente o uso durante esse período. É possível visualizar seus encargos para o período atual de faturamento via relatório do {{site.data.keyword.Bluemix_notm}}.
