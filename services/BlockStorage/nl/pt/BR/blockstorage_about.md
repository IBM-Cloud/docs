{:new_window: target="_blank"}


# Sobre {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Última atualização: 07 de setembro de 2016
{: .last-updated}

O serviço do IBM {{site.data.keyword.blockstorageshort}} lhe permite anexar armazenamento persistente em um servidor virtual. Para usar o armazenamento, você anexa os volumes de bloco em seus
servidores virtuais. Os dados nos volumes de armazenamento de bloco persistem além do ciclo de vida de seu servidor virtual. Isso significa que é possível remover os volumes de uma instância de servidor e
anexar novamente em outra instância de servidor, sem nenhuma mudança em seus dados. O {{site.data.keyword.blockstorageshort}} usa o OpenStack Cinder para gerenciar o ciclo de vida de volume. 

O armazenamento é acessado em um dispositivo de bloco para o qual é possível particionar, formatar e montar, como /dev/vdb. Os dados persistem até você exclui-los. 

## Volumes 
{: #using-volumes-concept}

Os volumes do {{site.data.keyword.blockstorageshort}} são criados por meio de uma instância de serviço do {{site.data.keyword.blockstorageshort}}. É possível anexar os volumes a um servidor virtual das maneiras a seguir:
  

* Especificar um dispositivo específico que você fornecer. 
* Especificar que o sistema selecione automaticamente um nome de dispositivo disponível. 

O servidor virtual executa suas operações de E/S diretamente com o dispositivo especificado, independentemente do serviço {{site.data.keyword.blockstorageshort}}.

## Captura Instantânea 
{: #using-snapshots-concept}

Também é possível criar capturas instantâneas de nível de bloco dos volumes. Uma captura instantânea captura dados no volume de armazenamento de bloco em um momento específico. É possível usar
capturas instantâneas para executar backups incrementais de seus dados. Dito isto, as capturas instantâneas existem no mesmo armazenamento que o volume original. Portanto, capturas instantâneas não
são uma estratégia de recuperação de desastre suficiente.

**Nota**: não será possível criar capturas instantâneas enquanto um volume estiver conectado a uma instância de servidor. 

Quando você criar um volume a partir de uma captura instantânea, um novo volume será criado que existirá no mesmo estado em que o volume original estava no momento em que você tomou uma captura
instantânea. 

Criar um volume a partir de uma captura instantânea tem o impacto a seguir:

* Volumes existentes não são removidos.
* Dados que são criados, modificados ou excluídos após a captura instantânea relevante ser tomada não são incluídos no novo
volume.

O que Vem em Seguida?

Criar um volume. Para obter mais informações, consulte [Criando volumes](../BlockStorage/blockstorage_creatingvolume.html).
