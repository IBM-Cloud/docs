{:new_window: target="_blank"}

# Perguntas frequentes {: #faq} 

*Última atualização: 18 de julho de 2016*
{: .last-updated}


## Como os preços variam dependendo do plano que eu escolher? {: #plan-price}
A precificação varia dependendo do plano escolhido. Para obter mais informações sobre precificação, consulte a [Folha de precificação do IBM Bluemix](https://console.ng.bluemix.net/pricing/){: new_window} ou use a [Calculadora](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} para obter estimativas mais detalhadas.


## Quais contas e planos de pagamento posso usar para o {{site.data.keyword.objectstorageshort}}? {: #account-payment}
O serviço {{site.data.keyword.objectstorageshort}} é fornecido com várias opções de planos. A partir de nossa liberação de disponibilidade geral, dois planos são oferecidos no momento, Padrão e Grátis. O plano Padrão está disponível somente para Contas pagas do {{site.data.keyword.Bluemix_notm}}, seja Pagamento por uso ou Assinatura, e para usuários internos da IBM. O plano Padrão inclui um Abono de crédito grátis introdutório de 5 GB no uso de armazenamento por conta.

Contas para teste que ainda estejam ativas podem usar o plano Grátis, que permite a existência de somente uma instância em uma Organização do {{site.data.keyword.Bluemix_notm}}. Depois que o tempo na avaliação do {{site.data.keyword.Bluemix_notm}} expirar, a instância de serviço associada do {{site.data.keyword.objectstorageshort}} será desativada, ou seja, a conta de armazenamento não poderá ser acessada pela interface com o usuário ou pela linha de comandos do {{site.data.keyword.Bluemix_notm}}. Depois de um período de cortesia de 30 dias, sua conta do {{site.data.keyword.Bluemix_notm}} será limpa e todos os dados excluídos. Para evitar perda de dados, recomenda-se fazer upgrade para uma Conta paga do {{site.data.keyword.Bluemix_notm}} o mais rápido possível. Para fazer upgrade de sua conta, clique no menu de gerenciamento de usuários e selecione **Conta**, que fornece instruções sobre o processo de upgrade.

## Como mudar meu plano? {: #changeplan}  
É possível fazer upgrade de instâncias criadas por meio de Beta ou no plano Grátis para o plano Padrão. A organização associada deve ser uma conta paga do {{site.data.keyword.Bluemix_notm}}. Não é possível fazer upgrade de contas para teste com instâncias do {{site.data.keyword.objectstorageshort}} para o plano Padrão, e fazer downgrade de instâncias no plano Padrão para outros planos. Ao fazer upgrade, sua instância de serviço e dados do cliente são movidos para o novo plano.

Para fazer upgrade do plano:
1.	Na interface com o usuário do {{site.data.keyword.objectstorageshort}}, clique em **Plano**.
2.	Selecione **Padrão** como o novo plano e, em seguida, clique em **Salvar**.

Também é possível mudar seu plano de pagamento usando a interface de linha de comandos. Para obter mais informações, consulte [Como mudar seu plano](../../pricing/index.html#changing).


## Como serei encarregado e cobrado pelo meu uso do {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

O serviço do {{site.data.keyword.objectstorageshort}} cobra somente pelo que você usa.  Não há taxa mínima, taxas de configuração ou compromissos para iniciar o uso do serviço. Não há cobrança por solicitação de API ou tráfego de rede por dados de entrada.

Seu uso do {{site.data.keyword.objectstorageshort}} é faturado com base no uso de armazenamento dentro do ciclo de faturamento. Isto inclui todos os dados de objeto nos contêineres que foram criados em sua conta da organização no {{site.data.keyword.Bluemix_notm}}. 

Os encargos de Transferência dos dados de saída se aplicam sempre quando dados são lidos a partir de quaisquer dos seus contêineres de objetos na rede pública. A largura da banda de saída pública é faturada para toda a largura de banda consumida no ciclo de faturamento.

Os componentes de métricas para a precificação do {{site.data.keyword.objectstorageshort}} são os seguintes:
* Uso de armazenamento  - $0.04 por GB por mês
* Transferência de dados de saída pública  - $0.09 por GB por mês 

Ao final do ciclo de faturamento, o {{site.data.keyword.Bluemix_notm}}  faturará o cliente automaticamente pelo uso no período de faturamento atual. É possível visualizar seus encargos para o período atual de faturamento via relatório do {{site.data.keyword.Bluemix_notm}}.

O plano de serviço padrão que é liberado para Londres e Dallas têm a mesma precificação.

## Como a replicação de dados é executada no {{site.data.keyword.objectstorageshort}}? {: #replication}
O serviço {{site.data.keyword.objectstorageshort}} mantém três cópias de seus dados, que são replicadas entre múltiplos nós de armazenamento. Para obter informações adicionais, consulte o documento [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

