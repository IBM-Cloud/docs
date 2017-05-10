---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Resolução de problemas do {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipelinets}


Aqui estão algumas respostas a perguntas comuns sobre o uso do {{site.data.keyword.GlobalizationPipeline_short}}. 
{:shortdesc}


## O nome do meu app não foi traduzido corretamente
{: #problem1}

As traduções geradas de algumas sequências não foram o que era esperado.
{:shortdesc}

Quando um arquivo de recursos é traduzido, as sequências que contêm nomes de produto ou outros nomes próprios podem não ser traduzidas corretamente.
{: tsSymptoms}

Outras vezes, nomes de produto ou nomes próprios não são traduzidos corretamente em outros idiomas, especialmente se o nome contiver palavras reais. Quando esses tipos de palavras ou frases são traduzidos, dependendo do significado dessas palavras em um idioma específico, o texto traduzido pode ter um significado diferente do nome em inglês.
{: tsCauses}

Teste a tradução de nomes de produto antes de usá-los e, se encontrar problemas, modifique o texto ou a tradução adequadamente. Para obter dicas de estilo de composição ao usar tradução de máquina, consulte [Dicas de tradução de máquina](./tips.html#globalizationpipeline_tips).
{: tsResolve}



## Eu não consigo fazer upload de um arquivo de recursos
{: #problem2}

O arquivo de recursos que eu estou tentando fazer upload não é aceito.
{:shortdesc}

Ao incluir um arquivo de recursos em um novo pacote configurável de tradução ou atualizar um arquivo de recursos existente a ser traduzido, eu recebo um erro.
{: tsSymptoms}

O {{site.data.keyword.GlobalizationPipeline_short}} só aceita arquivos de recursos destes tipos: Java™ .properties, JSON e AMD I18N.
{: tsCauses}

Assegure-se de que o arquivo de recursos que está sendo transferido por upload seja de um desses tipos.
{: tsResolve}
* Java .properties
* JSON
* AMD I18N



## Eu não consigo fazer upload de meu arquivo de recursos porque ele é muito grande
{: #problem3}

O arquivo de recursos que eu estou tentando fazer upload não é aceito.
{:shortdesc}

Ao incluir ou atualizar um arquivo de recursos para um projeto de tradução, um erro está ocorrendo porque uma parte do arquivo é muito grande.
{: tsSymptoms}

O {{site.data.keyword.GlobalizationPipeline_short}} só pode aceitar arquivos de recursos que atendam a determinados requisitos de tamanho.
{: tsCauses}

Assegure-se de que o arquivo de recursos esteja em conformidade com as diretrizes a seguir:
{: tsResolve}
* Cada chave pode ter no máximo 256 caracteres.
* Cada valor pode ter no máximo 2048 caracteres.
* Cada projeto de tradução pode ter no máximo 500 pares de chave/valor.
* Um arquivo de recursos não pode ter mais de 2 MB.




## O espaçamento em volta das variáveis contidas nas sequências não é consistente
{: #problem5}

O espaçamento usado em volta das variáveis após a tradução nem sempre é o mesmo.
{:shortdesc}

O espaçamento usado em volta das variáveis contidas nas sequências nem sempre é consistente de idioma para idioma após a tradução.
{: tsSymptoms}

Os mecanismos de tradução de máquina são projetados para funcionar com língua natural e nem sempre poderão reconhecer ou saber como tratar sintaxe específica usada pelas linguagens de programação. Como resultado, o tratamento de sintaxe combinada com texto simples pode variar.
{: tsCauses}

O {{site.data.keyword.GlobalizationPipeline_short}} atualmente reconhece o padrão "{}" comumente usado para representar variáveis e preservará o formato original do conteúdo.
{: tsResolve}
