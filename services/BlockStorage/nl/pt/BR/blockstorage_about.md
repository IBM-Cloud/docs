{:new_window: target="_blank"}


# Sobre {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Última atualização: 01 de agosto de 2016
{: .last-updated}

## Volumes 
{: #using-volumes-concept}

É possível usar o IBM {{site.data.keyword.blockstorageshort}} para criar volumes e anexá-los a servidores virtuais. Por padrão, o IBM {{site.data.keyword.virtualmachinesshort}} não possui armazenamento persistente e é revertido para a imagem padrão ao ser reiniciado. O {{site.data.keyword.blockstorageshort}} fornece armazenamento persistente para o servidor virtual. Os dados nos volumes de armazenamento de bloco persistem além do ciclo de vida de seu servidor virtual. O {{site.data.keyword.blockstorageshort}} usa o OpenStack Cinder para gerenciar o ciclo de vida de volume.

Os volumes do {{site.data.keyword.blockstorageshort}} são criados por meio de uma instância de serviço do {{site.data.keyword.blockstorageshort}}. É possível anexar os volumes a um servidor virtual das maneiras a seguir:
  

* Especificar um dispositivo específico que você fornecer. 
* Especificar que o sistema selecione automaticamente um nome de dispositivo disponível. 

O servidor virtual executa suas operações de E/S diretamente com o dispositivo especificado, independentemente do serviço {{site.data.keyword.blockstorageshort}}.

## Captura Instantânea 
{: #using-snapshots-concept}

Também é possível criar capturas instantâneas de nível de bloco dos volumes. Não é possível criar capturas instantâneas enquanto o volume é anexado, portanto, as capturas instantâneas resultantes terão um travamento consistente. 

O que Vem em Seguida?

Criar um volume. Para obter mais informações, consulte [Criando volumes](../BlockStorage/blockstorage_creatingvolume.html).
