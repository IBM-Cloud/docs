---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando o pacote Alarme
{: #openwhisk_catalog_alarm}

O pacote `/whisk.system/alarms` pode ser usado para disparar um
acionador em uma frequência especificada. Isso é útil para configurar tarefas ou
trabalhos recorrentes, como chamar uma ação de backup do sistema a cada hora.

O pacote inclui o feed a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | pacote | - | Alarmes e utilitário periódico |
| `/whisk.system/alarms/alarm` | alimentação | cron, trigger_payload, maxTriggers | Disparar evento acionador periodicamente |


## Disparando um evento acionador periodicamente
{: #openwhisk_catalog_alarm_fire}

O feed `/whisk.system/alarms/alarm` configura o serviço de Alarme para disparar um evento acionador a uma frequência especificada. Os parâmetros são como segue:

- `cron`: Uma sequência, baseada na sintaxe crontab do UNIX, que
indica quando disparar o acionador na Hora Universal Coordenada (UTC). A sequência é composta por cinco campos separados por espaços: `X X X X X`.
Para obter mais detalhes sobre como usar a sintaxe cron, veja: http://crontab.org. Seguem alguns exemplos da frequência indicada
pela sequência:

  - `* * * * *`: na parte superior de cada minuto.
  - `0 * * * *`: na parte superior de cada hora.
  - `0 */2 * * *`: a cada 2 horas (ou seja, 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: às 9h (UTC) no oitavo dia de cada mês

- `trigger_payload`: o valor desse parâmetro torna-se o conteúdo do acionador toda vez que o acionador for disparado.

- `maxTriggers`: parar de disparar acionadores quando esse limite for atingido. O padrão é definido como 1.000.000. É possível configurá-lo como infinite (-1).

A seguir está um exemplo de criação de um acionador que será disparado uma vez a cada 2 minutos com valores `name` e `place`
no evento acionador.

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Cada evento gerado incluirá como parâmetros as propriedades especificadas no valor de `trigger_payload`. Neste caso, cada evento acionador terá os parâmetros `name=Odin` e `place=Asgard`.

**Nota**: o parâmetro `cron` também suporta uma sintaxe customizada de seis campos, na qual o primeiro campo representa
segundos. 
Para obter mais detalhes sobre como usar a sintaxe cron customizada, veja: https://github.com/ncb000gt/node-cron. 
Aqui está um exemplo usando a notação de seis campos:
  - `*/30 * * * * *`: a cada trinta segundos.

