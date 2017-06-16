---



copyright:

  years: 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Mudando seu plano
{: #changing}

É possível mudar seu plano de serviço no {{site.data.keyword.Bluemix_notm}} no Painel de serviço, se mudanças de plano estiverem ativadas para esse serviço.

Apenas determinados serviços oferecem a possibilidade de mudança de plano de serviço. Se mudanças de plano estiverem ativadas para o serviço, o Painel de serviço exibirá uma opção **Plano** na navegação. Cada serviço terá um conjunto diferente de etapas subsequentes se você mudar o seu plano.

1. Para mudar seu plano, no Painel de serviço, clique em **Plano**. Normalmente, é possível fazer upgrade do plano ou reduzi-lo.
2. Depois de mudar o plano, você deverá executar um conjunto de etapas subsequentes. As etapas serão diferentes dependendo do tipo de mudança de plano e do serviço. Por exemplo, se
tiver reduzido o plano, talvez precise remontar seu app. Ou, caso tenha feito upgrade do
plano, talvez seja necessário remontar o app e tomar ações adicionais.<br/><br/>Para remontar seu app, acesse o Painel do {{site.data.keyword.Bluemix_notm}} e localize o app ao qual o serviço está ligado. No menu do app, selecione **Reiniciar app**.<br/><br/>Outras ações de etapa subsequente dependem do serviço. Veja as ações específicas na tabela a seguir.

|Serviço |	Informações|
|--------|-------------|
|Presence Insights 	|Se você tiver um plano Lite e exceder os abonos grátis, uma mensagem 403 é exibida ou registrada para indicar que você não está mais autorizado e que a sua instância de serviço está desativada. Ademais, as chamadas API REST do POST serão
rejeitadas com a resposta 403.<br/><br/>Se o serviço estiver desativado porque o abono grátis foi excedido, será necessário fazer upgrade de um plano Lite para um plano Pago. O seu serviço será reativado em 2 horas.<br/><br/>Se você tiver um plano Pago, será possível reduzi-lo para o plano Lite, desde que seu uso permaneça dentro do abono do plano Lite para eventos e armazenamento total.<br/><br/>Ao fazer upgrade ou reduzir seu plano, você não precisará remontar ou reiniciar seus apps.|
{:caption="Tabela 9. Etapas seguintes para mudar seu plano" caption-side="top"}

##Mudando o seu plano através da interface de linha de comandos

Opcionalmente, é possível mudar o seu plano de serviço usando a interface da linha de comandos.
Para atualizar o plano de serviço, insira o comando a seguir:
```
cf update-service <nome_do_serviço> [-p <novo_plano>]
```
