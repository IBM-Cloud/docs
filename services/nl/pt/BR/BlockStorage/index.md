{:new_window: target="_blank"} 

# Introdução ao {{site.data.keyword.blockstorageshort}} (BETA)

O {{site.data.keyword.blockstoragefull}} fornece acesso ao armazenamento de nível de bloco para cargas de trabalho e tempos de execução intensivos de transação na necessidade de armazenamento persistente.

É possível usar o IBM {{site.data.keyword.blockstorageshort}} para {{site.data.keyword.Bluemix_notm}} para criar volumes {{site.data.keyword.blockstorageshort}} que podem ser anexados às máquinas virtuais. Os dados nos volumes de armazenamento de bloco persistem além do ciclo de vida de suas máquinas virtuais. O IBM {{site.data.keyword.blockstorageshort}} usa o OpenStack Cinder para gerenciar o ciclo de vida de volume.

Os volumes {{site.data.keyword.blockstorageshort}} são criados por meio de uma instância de serviço do IBM {{site.data.keyword.blockstorageshort}}. É possível anexar os volumes a uma máquina virtual sob um dispositivo específico fornecido por você ou o sistema pode selecionar automaticamente um nome de dispositivo disponível. A máquina virtual executa suas operações de E/S diretamente com o dispositivo especificado independentemente do serviço {{site.data.keyword.blockstorageshort}}.

Também é possível criar capturas instantâneas de nível de bloco dos volumes. O serviço {{site.data.keyword.blockstorageshort}} não permite a criação de capturas instantâneas enquanto o volume estiver anexado, portanto, as capturas instantâneas resultantes serão consistentes por travamento. 

## Como criar uma instância de serviço {{site.data.keyword.blockstorageshort}}
Para criar uma instância do serviço {{site.data.keyword.blockstorageshort}} em seu espaço, siga estas etapas:
 
1.	Acesse a guia **Catálogo** do {{site.data.keyword.Bluemix_notm}} e insira **{{site.data.keyword.blockstorageshort}}** na caixa de procura ou acesse **Serviços** e selecione **Armazenamento**. Clique no serviço **{{site.data.keyword.blockstorageshort}}**. 
2.	Insira um espaço e o nome do serviço. Selecione o plano e clique em **Criar**.
 	
O serviço {{site.data.keyword.blockstorageshort}} é suportado somente em um contexto desvinculado. 

Uma instância de serviço {{site.data.keyword.blockstorageshort}} é criada em seu espaço. É possível abrir a UI do {{site.data.keyword.blockstorageshort}} para gerenciar volumes a qualquer momento clicando no ícone de instância de serviço.

## Interface com o usuário (UI) do {{site.data.keyword.blockstorageshort}}
A interface gráfica com o usuário do {{site.data.keyword.blockstorageshort}} fornece uma visão geral resumida de seus volumes de armazenamento, capturas instantâneas e consumo total de armazenamento para ambos os volumes e capturas instantâneas na parte superior da janela. 

O cabeçalho inclui a data e hora da última atualização da UI. É possível usar o ícone de atualização (um ícone de seta circular) para atualizar a UI manualmente, se necessário. 

Use a barra de procura para localizar volumes com base na sequência inserida. As tabelas são filtradas conforme você digita para mostrar somente os volumes que correspondem à sequência de procura inserida.

Abaixo da visão geral estão duas guias para volumes e capturas instantâneas. A guia de volume está selecionada por padrão. As tabelas nessa guia listam informações detalhadas sobre volumes disponíveis e anexados. Cada linha em uma tabela mostra as propriedades mais importantes de um volume. Propriedades adicionais ficam visíveis ao expandir uma linha. Os volumes anexados também mostram a instância da máquina virtual e o dispositivo ao qual o volume está anexado. 

A guia de captura instantânea mostra uma tabela de capturas instantâneas com propriedades e comportamento semelhantes. 

Use o ícone Criar acima das tabelas para criar um novo volume ou para manipular os existentes. Se estiver criando um volume a partir de uma captura instanânea, também é possível usar a lista suspensa Ações.


## Ações de volume

### Criar um volume

1.	Clique em **Criar** para iniciar o diálogo **Criar volume**.
2.	Forneça o tamanho do volume desejado. Números decimais não são aceitos. O tamanho é limitado pela cota que foi designada para sua organização.
3.	Forneça um nome. O nome é somente para propósitos de exibição.
4.	Opcionalmente, forneça uma descrição mais detalhada do volume. 
5.	Clique em **Criar** para enviar as informações e feche o diálogo. 

A criação de um volume pode consumir algum tempo. 

### Excluir um volume

1.	Selecione o volume que você deseja excluir.
2.	Clique em **Excluir (Delete)**.
3.	Confirme a exclusão desse volume.

Não é possível excluir um volume que esteja anexado a uma máquina virtual. Deve-se separar o volume primeiro.

### Estender um volume
É possível aumentar o tamanho do volume por meio da ação **Estender**. Não é possível reduzir o tamanho de um volume.

1.	Selecione o volume a ser estendido.
2.	Clique em **Estender**.
3.	Selecione o novo tamanho do volume. Forneça o novo tamanho total do volume.
4.	Clique em **Estender** para enviar as informações e feche o diálogo. 

Para ser estendido, um volume deve estar no estado **Disponível**. 

### Anexar e separar um volume para uma máquina virtual
Os volumes são anexados e separados de máquinas virtuais como dispositivos com um nome de dispositivo específico. Para que uma máquina virtual seja capaz de persistir dados em um volume, deve-se anexar o volume à máquina virtual.

Para anexar um volume, siga estas etapas: 

1.	Selecione um volume na lista de volumes disponíveis.
2.	Clique em **Anexar**.
3.	No diálogo Anexar, selecione uma instância de uma máquina virtual na lista suspensa. 
4.	Opcionalmente, especifique o dispositivo a ser usado para anexar esse volume. Se você não especificar o dispositivo, o sistema selecionará automaticamente o primeiro dispositivo disponível na máquina virtual.
5.	Clique em **Anexar** para enviar as informações e feche o diálogo.

O volume está listado na tabela de volumes anexados com as informações sobre a instância da máquina virtual. 
A máquina virtual agora pode usar o dispositivo para persistir dados. 

Para separar um volume, siga estas etapas: 

1.	Selecione um volume na lista de volumes anexados. 
2.	Clique em **Separar**.
3.	Confirme a separação no diálogo. 

Após ser separado, o volume não fica mais disponível para operações de E/S na instância da máquina virtual. Na UI do serviço {{site.data.keyword.blockstorageshort}}, agora o volume está disponível para ser anexado a outras máquinas virtuais.

## Ações de snapshot

### Criar uma Captura Instantânea

1.	Selecione a guia **Volumes** para obter uma lista de volumes.
2.	Selecione o volume do qual você deseja criar uma captura instantânea na coluna de volumes não anexados. Certifique-se de que o volume selecionado não esteja anexado. O volume selecionado é destacado. 
3.	Clique em **Ações** e selecione **Criar captura instantânea** na lista suspensa.
4.	Forneça um nome à captura instantânea e clique em **Criar**.

**Nota:** Não é possível excluir um volume enquanto capturas instantâneas para o volume existirem. 

### Criar um volume a partir de uma captura instantânea

1.	Selecione a guia **Capturas instantâneas** para obter uma lista de capturas instantâneas.
2.	Selecione a captura instantânea a partir da qual você deseja criar um volume. A captura instantânea selecionada é destacada.
3.	Clique em **Ações** e selecione **Criar volume** na lista suspensa.
4.	Forneça ao novo volume um novo e, opcionalmente, um novo tamanho e clique em **Criar**. 

**Nota:** o novo tamanho do volume deve ser igual ou superior ao tamanho da captura instantânea. 

### Excluir uma captura instantânea

1.	Selecione a guia **Capturas instantâneas** para obter uma lista de capturas instantâneas.
2.	Selecione a captura instantânea que deseja excluir. A captura instantânea selecionada é destacada.
3.	Clique em **Ações** e selecione **Excluir**. 



># Links Relacionados {:class="linklist"}
>## Referência da API {:id="api"}
>* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
