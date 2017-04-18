---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Manutenção
e atualização
{: #maintupdates_mf}

O {{site.data.keyword.mobilefoundation_short}} provisiona um {{site.data.keyword.mfserver_short_notm}}<!-- on {{site.data.keyword.containerlong}} as a container group-->. As
atualizações no servidor do
{{site.data.keyword.mobilefoundation_short}} são
notificadas aos usuários. É possível escolher atualizar o servidor
do {{site.data.keyword.mobilefoundation_short}} quando
for conveniente.
{:shortdesc}

## Estratégia de manutenção
{: #maintupdate_strategy_mf}

Quando houver uma atualização para o
{{site.data.keyword.mobilefoundation_short}}, o usuário será
notificado sobre a disponibilidade da atualização.  Uma notificação
será mostrada no painel da instância de serviço. O usuário pode
escolher aplicar a atualização no
{{site.data.keyword.mobilefoundation_short}} durante uma
janela de manutenção decidida por ele.

A atualização de
serviço do {{site.data.keyword.mobilefoundation_short}}
ficará disponível quando os componentes a seguir forem
atualizados.

* {{site.data.keyword.mfserver_short_notm}}.
* Versão do Liberty subjacente.
* Versão do Java Developer Kit subjacente.


## Aplicando as atualizações
{: #apply_update_mf}

A atualização para o
{{site.data.keyword.mobilefoundation_short}} pode ser
aplicada ao clicar em **Recriar**.

Ao aplicar esta atualização, a versão do servidor, conforme
visto no {{site.data.keyword.mfp_oc_short_notm}}, será
modificada para indicar a versão da atualização do servidor.

### Nota:
{: #note notoc}

* Os usuários não poderão aplicar suas próprias correções e
atualizações à sua instância de serviço do {{site.data.keyword.mobilefoundation_short}}.
* Consulte [Recriando servidor no plano do Developer](c_using_mfs_p1.html#recreate_mobilefoundation_p1) e [Recriando servidor no plano Professional 1 Application](c_using_mfs_p2.html#recreate_mobilefoundation_p2) para entender a diferença no comportamento nos planos ao clicar em **Recriar**.
