{:new_window: target="_blank"} 

# Introdução ao {{site.data.keyword.blockstorageshort}} (Beta)

Última atualização: 29 de julho de 2016
{: .last-updated}

O {{site.data.keyword.blockstoragefull}} fornece acesso ao armazenamento de nível de bloco para cargas de trabalho e tempos de execução com transação intensa que precisam de armazenamento persistente. É possível usar o serviço {{site.data.keyword.blockstorageshort}} para gerenciar ciclos de vida do volume, anexar volumes ao IBM Virtual Servers e criar capturas instantâneas dos volumes de armazenamento de bloco.

Antes de iniciar, revise as informações a seguir.

* O serviço {{site.data.keyword.blockstorageshort}} é suportado somente em um contexto desvinculado. 
* O IBM {{site.data.keyword.virtualmachinesshort}} deve ter sido criado para anexar volumes de armazenamento de bloco. Para saber mais sobre como usar volumes de armazenamento de bloco com o IBM {{site.data.keyword.virtualmachinesshort}}, consulte [Volumes de armazenamento de bloco e IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS). 

Conclua estas etapas para obter uma introdução ao
{{site.data.keyword.blockstorageshort}}:

1. Criar um volume.
   
   Abra o serviço {{site.data.keyword.blockstorageshort}}.

   b. Clique em **Criar** para iniciar o diálogo **Criar volume**.

   c. Forneça o tamanho do volume desejado. Números decimais não são aceitos. O tamanho é limitado pela cota que foi designada para sua organização.
   
   d. Forneça um nome. O nome é somente para propósitos de exibição.
   
   e. Opcionalmente, forneça uma descrição mais detalhada do volume.
   
   f. Clique em **Criar** para enviar as informações e fechar o diálogo.

  A criação de um volume pode consumir algum tempo.

2. Anexar um volume a um servidor virtual.

   Abra o serviço {{site.data.keyword.blockstorageshort}}.
   
   b. Selecione um volume na lista de volumes disponíveis.
   
   c. Clique em **Anexar**.
   
   d. No diálogo Anexar, selecione uma instância de um servidor virtual na lista suspensa. 
   
   e. Opcionalmente, especifique o dispositivo a ser usado para anexar esse volume. Se você não especificar o dispositivo, o sistema selecionará automaticamente o primeiro dispositivo disponível no servidor virtual.
   
   f. Clique em **Anexar** para enviar as informações e fechar o diálogo.
   
   O volume está listado na tabela de volumes anexados com as
informações sobre a instância do servidor virtual. O servidor virtual agora pode usar o dispositivo para persistir dados. 
 
O que Vem em Seguida?

Prepare o volume para uso. Para obter mais informações, consulte [Preparando volumes](../BlockStorage/blockstorage_preparingvolume.html).

# Links relacionados
{: #rellinks}

## Tutoriais e Amostras
{:id="samples"}

* [Como usar o IBM Block Storage for Bluemix com o IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Introdução ao IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [Demo do IBM Block Storage for Bluemix](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## Referência da API
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

