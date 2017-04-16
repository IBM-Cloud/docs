---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Fluxos do Decahose e do PowerTrack {: #decahose_powertrack}

O {{site.data.keyword.twittershort}} fornece acesso aos fluxos do
Decahose e do PowerTrack do Twitter, com base na inscrição do plano do {{site.data.keyword.Bluemix_notm}}. 
Ambos os fluxos entregam
feeds em tempo real e características diferentes para atender suas necessidades.
{:shortdesc}

O fluxo do Decahose é uma amostragem aleatória de 10% do Twitter Firehose. Os tweets são derivados do Twitter em tempo real e o fluxo é determinado pelos algoritmos de amostragem do Twitter. Para a maioria das análises estatísticas, uma amostra aleatória de 10% é suficientemente precisa. Os dados do Decahose são indexados para um período de 2 anos, portanto, as respostas às consultas podem não retornar tweets anteriores a 2 anos. O acesso ao Decahose está disponível no Plano grátis e no Plano de entrada, enquanto que o acesso ao fluxo do PowerTrack é exclusivo aos usuários do Plano de entrada.

O fluxo do PowerTrack oferece o benefício adicional de filtrar tweets recebidos com base em um filtro baseado em regras definidas pelo usuário conhecido como uma faixa. Como um usuário do Plano de Entrada, é possível
criar até 1.000 regras por conta. Para a filtragem avançada, múltiplas faixas podem ser combinadas para formar uma faixa agregada. As seguintes seções descrevem estados,
propriedades e ações suportadas de faixas que podem ser executadas nas faixas, como editar, excluir e
mais.

**Nota**: a indexação do fluxo do PowerTrack limita-se a 1 milhão de tweets por mês do calendário. Quando o limite é atingido, a indexação para o mês para. No início do mês seguinte, será possível
reativar suas faixas; elas não são ativadas automaticamente. Para maximizar o uso do fluxo,
o gerenciamento apropriado de suas faixas é altamente recomendável. Por exemplo, faixas redundantes podem tornar-se inativas.

## Tipos de faixas {: #track_types}

Os usuários do Plano de Entrada podem criar faixas customizáveis para filtrar mensagens coletadas no
fluxo de dados do PowerTrack.  O {{site.data.keyword.twittershort}}
suporta os seguintes dois tipos de faixas.

<dl>
<dt>Regra</dt>
<dd>Todas as mensagens coletadas nesta faixa corresponde a, ao menos, uma das regras associadas
à faixa. É possível incluir, editar e excluir regras neste tipo de faixa.

A [sintaxe de Regras GNIP PowerTrack](http://support.gnip.com/apis/powertrack2.0/rules.html) completa nas faixas baseadas em regra. Todas as consultas devem se adequar à {{site.data.keyword.twittershort}} [Linguagem de consulta](twitter_rest_apis.html#querylanguage "Linguagem de consulta").
</dd>

<dt>Agregado</dt>
<dd>Uma combinação de duas ou mais faixas de regra ou agregadas. As faixas agregadas são usadas para o agrupamento arbitrário
de diversas faixas. É possível incluir ou excluir faixas individuais de um tipo de faixa agregada. As regras individuais não podem ser incluídas em faixas agregadas; em vez disso, use uma faixa de regra para esse propósito. As faixas agregadas não têm um estado, mas suas faixas de regra constituinte são
**Ativa** ou **Inativa**.</dd>
</dl>

## Propriedades da faixa {: #track_properties}
As faixas contêm as seguintes propriedades. Algumas propriedades não se aplicam a ambas as faixas, baseadas em regras e agregadas. Por exemplo, a propriedade de regras não se aplica a faixas agregadas.

<dl>
<dt>createdDate</dt>
<dd>Indica quando a faixa foi criada; especificada como `YYYYMMDDHHMM`.</dd>

<dt>endDate</dt>
<dd>Indica quando a faixa para de coletar mensagens. O valor especificado deve estar no futuro e seguir um destes formatos: `YYYY-MM-DD` ou `YYYY-MM-DDTHH:MM:SSZ`. Especificar uma data no passado retorna um erro HTTP 400.

Esta propriedade não se aplica a faixas agregadas.</dd>

<dt>id</dt>
<dd>Uma referência de ID exclusivo designada a uma faixa mediante a criação. O ID é representado em um formato de sequência GUID (por exemplo, 3F2504E0-4F89-41D3-9A0C-0305E82C3301) para faixas de regra e agregadas.</dd>

<dt>name</dt>
<dd>O nome descritivo da faixa. A exclusividade dessa propriedade não é garantida.</dd>

<dt>rules</dt>
<dd>Uma matriz de regras, incluindo palavras-chave de consulta e outros parâmetros que definem os filtros de faixa. Essa propriedade se aplica a faixas baseadas em regras, mas não se aplica a faixas agregadas.</dd>

<dt>state</dt>
<dd>Deve ser **Ativo** ou **Inativo**. Uma faixa ativa coleta mensagens, enquanto uma faixa inativa não. É possível mudar o estado de uma faixa a qualquer momento.

Esta propriedade não se aplica a faixas agregadas.</dd>

<dt>trackIds</dt>
<dd>Uma matriz de IDs de faixa. Essa propriedade se aplica somente a faixas agregadas.</dd>

<dt>type</dt>
<dd>Indica se o tipo de faixa é **Regra** ou **Agregado**.

Para obter mais informações sobre as propriedades da faixa, incluindo operações de faixa e esquema do modelo, consulte a documentação da API REST do {{site.data.keyword.twittershort}}.</dd>
</dl>

