
{:new_window: target="_blank"}


# Anexando volumes do {{site.data.keyword.blockstorageshort}} a um servidor virtual
{: #attaching-block-storage-volume}

Última atualização: 29 de julho de 2016
{: .last-updated}

Os volumes são anexados e removidos de servidores virtuais como dispositivos com um nome de dispositivo específico. Para
que um servidor virtual seja capaz de persistir dados em um volume,
deve-se anexar o volume ao servidor virtual.

Para anexar um volume, siga estas etapas:

1.	Selecione um volume na lista de volumes disponíveis.
2.	Clique em **Anexar**.
3.	No diálogo Anexar, selecione uma instância de um servidor virtual na lista suspensa.
4.	Opcionalmente, especifique o dispositivo a ser usado para anexar esse volume. Se você não especificar o dispositivo, o sistema selecionará automaticamente o primeiro dispositivo disponível no servidor virtual.
5.	Clique em **Anexar** para enviar as informações e feche o diálogo.

O volume está listado na tabela de volumes anexados com as
informações sobre a instância do servidor virtual.
O servidor virtual agora pode usar o dispositivo para persistir dados. 

O que Vem em Seguida?

Depois que o volume é criado e incluído em um servidor virtual, consulte [Preparando volumes](../BlockStorage/blockstorage_preparingvolume.html) para prepará-lo para uso.
