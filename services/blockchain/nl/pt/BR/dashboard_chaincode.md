---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Chaincode
{: #v10_dashboard}
Última atualização: 16 de março de 2017
{: .last-updated}

Chaincode é um software (atualmente gravado em Go ou Java) que encapsula a lógica de negócios e as instruções transacionais
para criar e modificar ativos. Ele é executado em um contêiner do docker associado a qualquer peer que precise interagir com ele.  
{:shortdesc}

O Chaincode primeiro é instalado no sistema de arquivos de um peer e, em seguida, instanciado em um canal. A etapa de instanciação envolve
a inicialização de pares de valores de chave e a implementação do contêiner de chaincode. Qualquer peer que deseje interagir com um
chaincode deve ter o código-fonte instalado em seu sistema de arquivos e um contêiner de chaincode em execução. No entanto, se um peer
desejar usar o mesmo aplicativo de chaincode em múltiplos canais, ele precisará apenas de uma única instância do contêiner.  

A **Figura 8** mostra a visão geral da instalação do chaincode:

![Rede de Blockchain](images/chaincode_install_overview.png "Instalação do Chaincode")
*Figura 8. Visão Geral da Instalação do Chaincode*

* Use o menu suspenso e selecione um peer no qual instalar o chaincode.  
* Clique no botão **Instalar Chaincode** no lado direito de sua tela; isso abrirá um novo painel.

A **Figura 9** mostra a janela de instalação do chaincode:

![Rede de Blockchain](images/chaincode_install.png "Instalação do Chaincode")
*Figura 9. Janela de Instalação do Chaincode*

* Preencha os campos para ID do Chaincode e Versão do Chaincode. Conheça os esquemas de nomenclatura, pois essas sequências serão usadas em apps clientes para interagir com chaincodes específicos.
* Clique no botão Procurar e navegue por seu sistema de arquivos local até onde sua origem do chaincode está armazenada. Selecione um ou mais arquivos para instalar em seu peer.  **Nota**: é recomendável fazer upload apenas do chaincode gravado em Go ou Java.  

Assim que um chaincode tiver sido instalado no sistema de arquivos de um peer, ele deverá ser instanciado em um canal. Esta etapa de instanciação chama a função `init` para executar qualquer inicialização necessária do chaincode. Muitas vezes isso envolve a configuração dos pares de valores de chave que constituem o estado geral inicial do chaincode.

A **Figura 10** mostra a janela de instanciação do chaincode: 

![Rede de Blockchain](images/chaincode_instantiate.png "Instanciação de Chaincode")
*Figura 10. Janela de Instanciação do Chaincode*

Observe que os pares de valores de chave estão sendo configurados com a sequência - `["a","b","200","250"]` - e que há uma janela para selecionar o canal para instanciação. Este exemplo mostra um chaincode denominado `end2end` instalado em `fabric-peer1a` e instanciado em um canal denominado `mychannel`:

A combinação de instalação/instanciação é um recurso poderoso, pois permite que um peer interaja com o mesmo contêiner de chaincode em múltiplos canais. O único pré-requisito é que a origem de chaincode real seja instalada no sistema de arquivos do peer. Dessa forma, se um pedaço de chaincode comum estivesse sendo usado em vários canais, um peer precisaria apenas de um único contêiner de chaincode para executar leituras/gravações em todos os livros razão do canal. Essa abordagem leve se mostra benéfica para o desempenho e o rendimento computacionais à medida que as redes são escaladas e os aplicativos de chaincode se tornam mais elaborados.    
