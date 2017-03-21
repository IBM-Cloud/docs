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

# Anotações em ativos do OpenWhisk

Ações, acionadores, regras e pacotes (coletivamente referidos como ativos) do OpenWhisk podem ser decorados com `anotações`. As anotações são anexadas a ativos como parâmetros com uma `key` que define um nome e um `value` que define o valor. É conveniente configurá-los na interface da linha de comandos (CLI) por meio de `--annotation` ou `-a` em forma reduzida.
{: shortdesc}

Lógica: as anotações foram incluídas no OpenWhisk para permitir a experimentação sem fazer mudanças no esquema do ativo subjacente. Até a escrita deste documento, não tínhamos definido deliberadamente quais `annotations` são permitidas. No entanto, à medida que começamos a usar as anotações mais intensamente para divulgar as mudanças de semântica, é importante que finalmente comecemos a documentá-las.

O uso mais comum de anotações até a data é documentar ações e pacotes. Você verá muitos dos pacotes no catálogo do OpenWhisk carregarem anotações, como uma descrição da funcionalidade oferecida por suas ações, quais parâmetros são necessários no tempo de ligação do pacote e quais são os parâmetros invoke-time, se um parâmetro é um "segredo" (por exemplo, senha) ou não. Nós os inventamos conforme necessário, por exemplo, para permitir a integração da UI.

Aqui está um conjunto de amostra de anotações para uma ação `echo` que retorna seus argumentos de entrada não modificados (por exemplo, `function main(args) { return args }`). Essa ação pode ser útil para registrar parâmetros de entrada, por exemplo, como parte de uma sequência ou regra.

```
wsk action create echo echo.js \
    -a description 'An action which returns its input. Useful for logging input to enable debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

As anotações que usamos para descrever os pacotes são:

- `description`: uma descrição concisa do pacote
- `parameters`: uma matriz descrevendo os parâmetros com escopo definido para o pacote (descrito mais abaixo)

Da mesma forma, para ações: 

- `description`: uma descrição concisa da ação
- `parameters`: uma matriz descrevendo as ações que são necessárias para executar a ação
- `sampleInput`: um exemplo mostrando o esquema de entrada com valores típicos
- `sampleOutput`: um exemplo mostrando o esquema de saída, geralmente para o `sampleInput`

As anotações que usamos para descrever os parâmetros incluem:

- `name`: o nome do parâmetro
- `description`: uma descrição concisa do parâmetro
- `doclink`: um link para a documentação adicional para o parâmetro (útil para tokens OAuth, por exemplo) 
- `required`: true para parâmetros necessários e false para os opcionais
- `bindTime`: true se o parâmetro deverá ser especificado quando um pacote for ligado
- `type`: o tipo do parâmetro, `password`, `array` (mas pode ser usado de modo mais abrangente)

As anotações *não* são verificadas. Portanto, embora seja possível usar as anotações para indicar se uma composição de duas ações em uma sequência é legal, por exemplo, o sistema ainda não faz isso.

## Anotações para recursos experimentais

Nós recentemente estendemos a API principal com alguns recursos experimentais. Para permitir que os pacotes e ações participem desses recursos, introduzimos três novas anotações que são semanticamente significativas. Essas anotações devem ser configuradas explicitamente como `true` para que tenham efeito. Mudar o valor de `true` para `false` excluirá o ativo anexado da API experimental. As anotações não têm significado contrário no sistema. As anotações são:

- `final`: aplica-se somente a uma ação. Isso torna todos os parâmetros de ação que já estão definidos imutáveis. Um parâmetro de uma ação transportando a anotação não pode ser substituído por parâmetros invoke-time quando o parâmetro tiver um valor definido por meio de seu pacote de fechamento ou a definição de ação.
- `web-export`: aplica-se somente a uma ação. Se presente, ela torna sua ação correspondente acessível para chamadas REST *sem* autenticação. Nós as chamamos de [*ações da web*](openwhisk_webactions.html) porque elas permitem usar ações do OpenWhisk em um navegador, por exemplo. É importante observar que o *proprietário* da ação da web incorre no custo de executá-las no sistema (ou seja, o *proprietário* da ação também possui o registro de ativações).

