{:new_window: target="_blank"} 

# Usando o volume do {{site.data.keyword.blockstorageshort}} 
{: #using-block-storage-volume} 
Última atualização: 07 de setembro de 2016
{: .last-updated}

Para usar volumes, siga estas etapas:

## Excluindo um volume {: #deleting-volume}

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Selecione o volume que você deseja excluir.
4.	A partir do menu suspenso Ações, clique em **Excluir**.
5.	Confirme a exclusão desse volume.

Não é possível excluir um volume anexado a um servidor virtual. Deve-se separar o volume primeiro. Excluir o volume o tornará inacessível para uso futuro e os dados nele serão perdidos. Além disso, não será possível excluir volumes que tenham capturas instantâneas associadas.

## Ampliando um volume {: #extending-volume}
É possível aumentar o volume em tamanho em até dez vezes do
tamanho original por meio da ação
**Ampliar**. Não é possível reduzir o tamanho de um volume.

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Selecione o volume a ser estendido.
4.	A partir do menu suspenso Ações, clique em **Ampliar**.
5.	Selecione o novo tamanho do volume. Forneça o novo tamanho total do volume.
6.	Clique em **Estender** para enviar as informações e feche o diálogo. 

Para ser estendido, um volume deve estar no estado **Disponível**. Após você ampliar o volume, deve-se notificar o sistema de arquivos (como ext4) em que o disco foi ampliado
redimensionando o sistema de arquivos para o novo tamanho. 

## Anexando e removendo um volume em um servidor
virtual {: #attaching-detaching-volume}
Os volumes são anexados e removidos de servidores virtuais como dispositivos com um nome de dispositivo específico. Para
que um servidor virtual seja capaz de persistir dados em um volume,
deve-se anexar o volume ao servidor virtual.

Para anexar um volume, siga estas etapas: 

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Selecione um volume na lista de volumes disponíveis.
4.	A partir do menu suspenso Ações, clique em **Anexar**.
5.	No diálogo Anexar, selecione uma instância de um servidor virtual na lista suspensa. 
6.	Opcionalmente, especifique o dispositivo a ser usado para anexar esse volume. Se você não especificar o dispositivo, o sistema selecionará automaticamente o primeiro dispositivo disponível no servidor virtual.
7.	Clique em **Anexar** para enviar as informações e feche o diálogo.

O volume está listado na tabela de volumes anexados com as
informações sobre a instância do servidor virtual. 
O servidor virtual agora pode usar o dispositivo para persistir dados. 

Quando você estiver pronto para remover um volume, deve-se preparar o servidor virtual para a remoção. Por exemplo, pare qualquer aplicativo que estiver usando o sistema de arquivos. Além disso,
desmonte o dispositivo a partir de dentro da instância de servidor virtual.

Para separar um volume, siga estas etapas: 

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Selecione um volume na lista de volumes anexados. 
4.	A partir do menu suspenso Ações, clique em **Remover**.
5.	Confirme a separação no diálogo. 

Após ser removido, o volume não ficará mais disponível para
operações de E/S na instância do servidor virtual. Na UI do serviço {{site.data.keyword.blockstorageshort}}, agora o volume está
disponível para ser anexado a outros servidores virtuais.
