---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre
{: #about}

O {{site.data.keyword.bplong}} pode ser usado para criar blocos de construção de infraestrutura. É possível montar serviços do {{site.data.keyword.IBM_notm}} Cloud para criar infraestrutura implementável e reutilizável.
{:shortdesc}

O {{site.data.keyword.bpshort}} usa o Terraform para simplificar o gerenciamento de infraestrutura. Por exemplo, se você quiser girar múltiplas cópias de seu serviço que usam um cluster de servidores de apps, um balanceador de carga e um servidor de banco de dados, será possível gravar um script bash para executar comandos para girar esses componentes. Mas será mais fácil, mais rápido e mais ordenado ter uma configuração com um executor que tome a configuração e a transforme em recursos reais. Com o Terraform, é possível girar vários recursos ao mesmo tempo, como um grupo coletivo, com dependências mapeadas internamente. 

## Razões para usar o {{site.data.keyword.bpshort}}
{: #reasons}

Talvez você queira usar uma infraestrutura codificada nos cenários a seguir:
{:shortdesc}

| Cenário     | Razões    |
| :------------- | :------------- |
| Você deseja recriar e reutilizar sua infraestrutura. | É possível usar o {{site.data.keyword.bpshort}} para gerenciamento de infraestrutura. Com o {{site.data.keyword.bpshort}}, é possível provisionar, modificar e destruir seus recursos programaticamente. Ao codificar e configurar os recursos, será possível desenvolver uma biblioteca de recursos que poderão ser reutilizados repetidas vezes para obter os mesmos resultados.|
| Você deseja transparência sobre a configuração de seus ambientes. | O {{site.data.keyword.bpshort}} trabalha com configurações no controle de versão, que permite colaboração, revisão e fornece uma trilha de auditoria para ver como e quando as mudanças foram feitas. Também será possível visualizar suas mudanças se você precisar recuperar uma configuração anterior. |
| Você deseja simplificar a execução de mudanças ambientais. | O {{site.data.keyword.bpshort}} segue o modelo declarativo que fornece uma fonte isolada de verdade. Ao planejar uma mudança em seu ambiente, você determina o resultado desejado. |
| Você já usa uma ferramenta de gerenciamento de configuração (CM), mas deseja uma maneira mais automatizada para configurar seus ambientes. | O {{site.data.keyword.bpshort}} pode trabalhar junto a ferramentas CM. Os ambientes implementados com o {{site.data.keyword.bpshort}} são abstrações de alto nível que podem criar recursos de infraestrutura. Em seguida, será possível usar as ferramentas CM para instalar e configurar software nos recursos provisionados pelo {{site.data.keyword.bpshort}}.  
  
## Como ele funciona
{: #how}

É possível implementar recursos para seus ambientes usando o {{site.data.keyword.bpshort}}.
{:shortdesc}

O {{site.data.keyword.bpshort}} usa o Terraform como a ferramenta subjacente para ativar a infraestrutura como código para que seja possível definir recursos do {{site.data.keyword.IBM}} Cloud como código. Os recursos em nuvem podem ser componentes diferentes de sua infraestrutura, como servidores bare metal, servidores virtuais, balanceadores de carga, componentes de rede definidos por software. 

### Configurações para definir recursos
{: #how-define}

Uma configuração ou configuração Terraform é um arquivo que define quais recursos compõem sua infraestrutura. Configurações são arquiteturas implementáveis que podem ser aplicadas a um ou mais ambientes. O diagrama a seguir mostra o que compõe uma configuração e como as peças trabalham juntas para criar um ambiente implementável no {{site.data.keyword.bpshort}}.


![{{site.data.keyword.bpshort}} diagrama de arquitetura](/images/anatomy_of_a_schematic.png)

Figura 1. Diagrama de arquitetura do {{site.data.keyword.bpshort}}

### Controle de versão para permitir colaboração
{: #how-collaborate}

As configurações são armazenadas no GitHub para que as equipes possam revisar código e colaborar. Com o GitHub, você tem uma trilha de auditoria integrada e pode visualizar um histórico completo de confirmação de mudanças que são feitas em suas configurações. É possível salvar informações de uso em arquivos leia-me para tornar a configuração compartilhável e utilizável por múltiplas equipes.

### Ambientes do {{site.data.keyword.bpshort}} para provisionar recursos
{: #how-provision}

É possível usar o {{site.data.keyword.bpshort}} para verificar seu código no GitHub e implementar recursos em um ambiente. Os ambientes podem compartilhar configurações comuns. Por exemplo, será possível girar um ambiente de QA temporário que parece de produção e derrubá-lo quando você terminar de testar. Será possível construir uma biblioteca de configurações de ambiente comuns que possam ser identificadas e procuradas por todos os usuários em sua conta do {{site.data.keyword.Bluemix_notm}}.
