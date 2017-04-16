
{:new_window: target="_blank"}


# Anexando volumes do {{site.data.keyword.blockstorageshort}} a um servidor virtual
{: #attaching-block-storage-volume}

Última atualização: 13 de setembro de 2016
{: .last-updated}

Os volumes são anexados e removidos de servidores virtuais como dispositivos com um nome de dispositivo específico. Para
que um servidor virtual seja capaz de persistir dados em um volume,
deve-se anexar o volume ao servidor virtual.

Para anexar um volume, siga estas etapas:

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Selecione um volume na lista de volumes disponíveis.
4.	Clique em **Anexar**.
5.	No diálogo Anexar, selecione uma instância de um servidor virtual na lista suspensa.
6.	Opcionalmente, especifique o dispositivo a ser usado para anexar esse volume. 
    
    **Nota**: se você não especificar o dispositivo, o sistema selecionará automaticamente o primeiro dispositivo disponível no servidor virtual.

7.	Clique em **Anexar** para enviar as informações e feche o diálogo.

O volume está listado na tabela de volumes anexados com as
informações sobre a instância do servidor virtual.
O servidor virtual agora pode usar o dispositivo para persistir dados. 

O que Vem em Seguida?

Depois que o volume é criado e incluído em um servidor virtual, consulte [Preparando volumes](../BlockStorage/blockstorage_preparingvolume.html) para prepará-lo para uso.
