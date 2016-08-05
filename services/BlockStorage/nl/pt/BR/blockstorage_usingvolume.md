{:new_window: target="_blank"} 

# Usando o volume do {{site.data.keyword.blockstorageshort}}{: #using-block-storage-volume} 

*Última atualização: 20 junho de 2016*
{: .last-updated}

## Criando um volume {: #creating-volume} 

1.	Clique em **Criar** para iniciar o diálogo **Criar volume**.
2.	Forneça o tamanho do volume desejado. Números decimais não são aceitos. O tamanho é limitado pela cota que foi designada para sua organização.
3.	Forneça um nome. O nome é somente para propósitos de exibição.
4.	Opcionalmente, forneça uma descrição mais detalhada do volume. 
5.	Clique em **Criar** para enviar as informações e feche o diálogo. 

A criação de um volume pode consumir algum tempo. 

## Excluindo um volume {: #deleting-volume}

1.	Selecione o volume que você deseja excluir.
2.	Clique em **Excluir (Delete)**.
3.	Confirme a exclusão desse volume.

Não é possível excluir um volume anexado a um servidor virtual. Deve-se separar o volume primeiro.

## Ampliando um volume {: #extending-volume}
É possível aumentar o volume em tamanho em até dez vezes do
tamanho original por meio da ação
**Ampliar**. Não é possível reduzir o tamanho de um volume.

1.	Selecione o volume a ser estendido.
2.	Clique em **Estender**.
3.	Selecione o novo tamanho do volume. Forneça o novo tamanho total do volume.
4.	Clique em **Estender** para enviar as informações e feche o diálogo. 

Para ser estendido, um volume deve estar no estado **Disponível**. 

## Anexando e removendo um volume em um servidor
virtual {: #attaching-detaching-volume}
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

Para separar um volume, siga estas etapas: 

1.	Selecione um volume na lista de volumes anexados. 
2.	Clique em **Separar**.
3.	Confirme a separação no diálogo. 

Após ser removido, o volume não ficará mais disponível para
operações de E/S na instância do servidor virtual. Na UI do serviço {{site.data.keyword.blockstorageshort}}, agora o volume está
disponível para ser anexado a outros servidores virtuais.
