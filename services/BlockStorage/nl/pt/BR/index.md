{:new_window: target="_blank"} 

# Introdução ao {{site.data.keyword.blockstorageshort}} (Beta)

*Última atualização: 15 julho de 2016*
{: .last-updated}

O {{site.data.keyword.blockstoragefull}} fornece acesso ao armazenamento de nível de bloco para cargas de trabalho e tempos de execução intensivos de transação na necessidade de armazenamento persistente.

É possível usar o IBM
{{site.data.keyword.blockstorageshort}} for
{{site.data.keyword.Bluemix_notm}} para criar volumes do
{{site.data.keyword.blockstorageshort}}, que podem ser
anexados aos servidores virtuais. Os dados nos volumes de
armazenamento de bloco persistem além do ciclo de vida de seus
servidores virtuais. O IBM {{site.data.keyword.blockstorageshort}} usa o OpenStack Cinder para gerenciar o ciclo de vida de volume.

Os volumes {{site.data.keyword.blockstorageshort}} são criados por meio de uma instância de serviço do IBM {{site.data.keyword.blockstorageshort}}. 
É possível anexar os volumes a uma máquina virtual sob um dispositivo específico fornecido por você ou o sistema pode selecionar automaticamente um nome de dispositivo disponível. 
O servidor virtual executa suas operações de E/S diretamente com o
dispositivo especificado, independentemente do serviço
{{site.data.keyword.blockstorageshort}}.

Também é possível criar capturas instantâneas de nível de bloco dos volumes. O serviço {{site.data.keyword.blockstorageshort}} não permite a criação de capturas instantâneas enquanto o volume estiver anexado, portanto, as capturas instantâneas resultantes serão consistentes por travamento. 


## Como criar uma instância de serviço {{site.data.keyword.blockstorageshort}}
Para criar uma instância do serviço {{site.data.keyword.blockstorageshort}} em seu espaço, siga estas etapas:
 
1.	Acesse a guia **Catálogo** do {{site.data.keyword.Bluemix_notm}} e insira **{{site.data.keyword.blockstorageshort}}** na caixa de procura ou acesse **Serviços** e selecione **Armazenamento**. Clique no serviço **{{site.data.keyword.blockstorageshort}}**. 
2.	Insira um espaço e o nome do serviço. Selecione o plano e clique em **Criar**.
 	
O serviço {{site.data.keyword.blockstorageshort}} é suportado somente em um contexto desvinculado. 

Uma instância de serviço {{site.data.keyword.blockstorageshort}} é criada em seu espaço. É possível abrir a UI do {{site.data.keyword.blockstorageshort}} para gerenciar volumes a qualquer momento clicando no ícone de instância de serviço.



## Usando a interface com o usuário (UI) do {{site.data.keyword.blockstorageshort}}{: #using-block-storage-ui}
A interface gráfica com o usuário do {{site.data.keyword.blockstorageshort}} fornece uma visão geral resumida de seus volumes de armazenamento, capturas instantâneas e consumo total de armazenamento para ambos os volumes e capturas instantâneas na parte superior da janela. 

O cabeçalho inclui a data e hora da última atualização da UI. É possível usar o ícone de atualização (um ícone de seta circular) para atualizar a UI manualmente, se necessário. 

Use a barra de procura para localizar volumes com base na sequência inserida. As tabelas são filtradas conforme você digita para mostrar somente os volumes que correspondem à sequência de procura inserida.

Abaixo da visão geral estão duas guias para volumes e capturas instantâneas. A guia de volume está selecionada por padrão. As tabelas nessa guia listam informações detalhadas sobre volumes disponíveis e anexados. Cada linha em uma tabela mostra as propriedades mais importantes de um volume. Propriedades adicionais ficam visíveis ao expandir uma linha. 
Os volumes anexados também mostram a instância do servidor virtual e o dispositivo ao qual o volume está anexado. 

A guia de captura instantânea mostra uma tabela de capturas instantâneas com propriedades e comportamento semelhantes. 

Use o ícone Criar acima das tabelas para criar um novo volume ou para manipular os existentes. Se estiver criando um volume a partir de uma captura instantânea, também
será possível usar a lista suspensa Ações.




## Anexando um volume a um servidor virtual {: #attaching-detaching-volume}
Os volumes são anexados e removidos de servidores virtuais como
dispositivos com um nome de dispositivo específico. Para que um
servidor virtual seja capaz de persistir dados em um volume, deve-se
anexar o volume ao servidor virtual.

Para anexar um volume, siga estas etapas: 

1.	Selecione um volume na lista de volumes disponíveis.
2.	Clique em **Anexar**.
3.	No diálogo Anexar, selecione uma instância de um servidor
virtual na lista suspensa. 
4.	Opcionalmente, especifique o dispositivo a ser usado para anexar esse volume. 
Se você não especificar o dispositivo, o sistema selecionará
automaticamente o primeiro dispositivo disponível no servidor virtual.
5.	Clique em **Anexar** para enviar as informações e feche o diálogo.

O volume está listado na tabela de volumes anexados com as
informações sobre a instância do servidor virtual.
O servidor virtual agora pode usar o dispositivo para persistir dados. 


# Links Relacionados
{: #rellinks}

## Referência da API
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

