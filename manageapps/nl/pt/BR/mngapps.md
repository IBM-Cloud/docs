---

copyright:
  years: 2015, 2017
lastupdated: "2015-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gerenciando aplicativos
{: #manageapps}

É possível usar o Painel na interface com o usuário do {{site.data.keyword.Bluemix}} para visualizar e gerenciar seus aplicativos e serviços, além de monitorar o uso de recursos usando os calibradores de cota.
{:shortdesc}

A seção do aplicativo no Painel fornece informações de resumo dos aplicativos criados. As informações de resumo incluem nome, ícone, URL, tempo de
execução e status de execução do aplicativo e das instâncias de serviço que estão ligadas
ao aplicativo. São usadas cores diferentes para indicar o status de execução de cada
aplicativo.

**Interrompido ou desconhecido (cinza)**

  Seu app está interrompido ou o status é desconhecido. O ícone cinza indica que o aplicativo está interrompido ou o status é desconhecido.

**Em execução (verde)**

  Seu app está em execução. O ícone verde indica que o aplicativo está iniciado e todas as instâncias estão em execução.

*Número* **em execução (amarelo)**

  O app está iniciado, mas nem todas as instâncias estão em execução. O ícone amarelo indica que menos de 100% das instâncias estão em execução. O número de instâncias que estão em execução e o número de instâncias que
falharam são exibidos.

**Não em execução (vermelho)**

  Seu app não está em execução. O ícone vermelho indica que o aplicativo foi iniciado, mas nenhuma instância está em execução.

No Catálogo do {{site.data.keyword.Bluemix_notm}}, é possível visualizar os serviços e os iniciadores disponíveis. É possível selecionar um iniciador
para criar um aplicativo, ligar um serviço e gerenciar o aplicativo. Depois que um serviço é ligado a um aplicativo, é possível gerenciar as
instâncias de serviço existentes que estão ligadas ao aplicativo atual e criar instâncias
de serviço para o aplicativo. Também é possível desvincular ou excluir a instância de
serviço de um aplicativo ou escolher um plano de serviço diferente.

Para visualizar
mais informações sobre um aplicativo, clique no quadrado para abrir a página Visão Geral do app.

**Nota:** é possível visualizar recursos de uma organização por vez somente. Se você for membro de múltiplas organizações, poderá comutar entre as organizações clicando no ícone
**ALTERAR ORGANIZAÇÃO** ao lado da organização atual que é exibida no cabeçalho do painel.

Quando
um aplicativo é implementado, é possível iniciar, parar, reiniciar, ou (no caso de aplicativos da web) modificar o
número de instâncias e a quantidade de memória usada pelo aplicativo. Nesse momento, para aplicativos da web, o
{{site.data.keyword.Bluemix_notm}} não escala
automaticamente seus aplicativos com base na carga deles, de modo que você mesmo deve
gerenciar esse aspecto.

Os aplicativos poderão ser
reimplementados se uma atualização for feita. O mecanismo para atualizar o aplicativo é o
mesmo utilizado para implementá-lo originalmente. {{site.data.keyword.Bluemix_notm}} para todas as instâncias em execução
e as substitui por novas instâncias automaticamente.
