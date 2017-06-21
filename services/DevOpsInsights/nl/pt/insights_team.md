---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Dinâmica De time
{: #gettingstarted}

O {{site.data.keyword.DRA_full}} Team Dynamics emprega análise de codificação social para identificar o nível de interação entre os membros da equipe para que a equipe possa corrigir práticas não produtivas. 
{:shortdesc}

Depois de abrir o {{site.data.keyword.DRA_short}} por meio de sua cadeia de ferramentas, clique em **Team Dynamics**. Daí, é possível selecionar uma categoria de analítica para pesquisar detalhadamente os hábitos e as práticas de colaboração de sua equipe. O que cada conjunto de dados indica pode variar de equipe para equipe e será possível realizar drill down em cada visualização para ajuda e orientação.  

## Categorias de Dados

Os dados que o {{site.data.keyword.DRA_short}} usa para preencher seus painéis são extraídos automaticamente do repositório de controle de fonte de sua equipe. É possível obter mais informações sobre o que os dados significam e como podem ser aplicados a seu projeto clicando em **Informações** ou **Orientação** em qualquer gráfico.

### Codificação social

O gráfico Codificação social mostra as conexões entre os contribuidores de seu projeto em uma maneira visual, altamente interativa. Cada nó no gráfico representa um desenvolvedor. O tamanho de um nó é escalado logaritmicamente para as contribuições de um desenvolvedor para um projeto. As linhas entre os nós indicam colaboração; quanto mais grossa for uma linha, mais dois desenvolvedores colaboraram no período selecionado. 

Cada nó recebe a cor azul e vermelha para diferentes graus. Azul indica quantas linhas de código um contribuidor incluiu como uma parte do número total de linhas que o contribuidor acessou. Vermelho indica quantas linhas de código um contribuidor removeu. Um contribuidor que só incluiu código seria totalmente azul, enquanto um contribuidor que incluiu e removeu um número igual de linhas seria metade azul e metade vermelho. 

### Autores

A categoria Autores fornece o número de confirmações, mudanças de linha e mudanças de arquivo por contribuidor de repositório. Embora algo como o número total de linhas codificadas não deva ser usado para determinar a contribuição líquida de um membro da equipe para um projeto, essas informações podem ser úteis para líderes e gerentes de equipe. Um membro da equipe que contribua com um número extenso de mudanças de linha pode estar sobrecarregado, representar um gargalo em seus processos ou codificar em um estilo mais detalhado em comparação com outros membros da equipe. 
