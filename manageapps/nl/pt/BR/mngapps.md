---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Detalhes do app
{: #manageapps}

O painel Apps no console do {{site.data.keyword.Bluemix}} fornece informações de resumo para os aplicativos criados. As informações de resumo incluem o nome, ícone, URL, tempo de execução, status de execução e instâncias de serviço que estão ligadas ao app. 
{:shortdesc}

No painel Apps, é possível visualizar o status de cada aplicativo.

**Interrompido ou desconhecido (cinza)**

  Seu app está interrompido ou o status é desconhecido. O ícone cinza indica que o app está interrompido ou o status é desconhecido.

**Em execução (verde)**

  Seu app está em execução. O ícone verde indica que o app está iniciado e todas as instâncias estão em execução.

*Número* **em execução (amarelo)**

  O app está iniciado, mas nem todas as instâncias estão em execução. O ícone amarelo indica que menos de 100% das instâncias estão em execução. O número de instâncias que estão em execução e o número de instâncias que
falharam são exibidos.

**Não em execução (vermelho)**

  Seu app não está em execução. O ícone vermelho indica que o app está iniciado, mas nenhuma instância está em execução.

Para visualizar mais informações sobre um app, clique no nome para abrir a página Visão geral do app.

Quando um app é implementado, é possível iniciar, parar, reiniciar ou (no caso de aplicativos da web) modificar o número de instâncias e a quantia de memória que é usada pelo app. No momento, para aplicativos da web, o {{site.data.keyword.Bluemix_notm}} não escala automaticamente o app com base em sua carga, então deve-se gerenciar esse aspecto sozinho.

Os aplicativos poderão ser
reimplementados se uma atualização for feita. O mecanismo para atualizar o app é o mesmo mecanismo que é usado para implementá-lo originalmente. {{site.data.keyword.Bluemix_notm}} para todas as instâncias em execução
e as substitui por novas instâncias automaticamente.
