{:new_window: target="_blank"} 


# Usando a captura instantânea do {{site.data.keyword.blockstorageshort}} {: #using-block-storage-snapshot} 
Última atualização: 07 de setembro de 2016
{: .last-updated}

Para usar capturas instantâneas, siga estas etapas:

## Criando uma captura instantânea {: #creating-snapshot} 

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Clique na guia Gerenciar.
4.	Na página Gerenciar, clique na guia **Volumes** para obter uma lista de volumes.
5.	Selecione o volume do qual você deseja criar uma captura instantânea na coluna de volumes não anexados. Certifique-se de que o volume selecionado não esteja anexado. O volume selecionado é destacado. 
6.	A partir do menu suspenso Ações, clique em **Criar captura instantânea**.
7.	Forneça um nome à captura instantânea e clique em **Criar**.

**Nota:** 

* Não será possível excluir um volume enquanto existirem capturas instantâneas para o volume. 
* O tamanho da captura instantânea é automaticamente configurado para ser o mesmo que aquele do volume original.

## Criando um volume a partir de uma captura instantânea {: #creating-volume-from-snapshot}

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Clique na guia Gerenciar.
4.	Na página Gerenciar, clique na guia **Capturas instantâneas** para obter uma lista de capturas instantâneas.
5.	Selecione a captura instantânea a partir da qual você deseja criar um volume. A captura instantânea selecionada é destacada.
6.	A partir do menu suspenso Ações, clique em **Criar volume**.
7.	Forneça ao novo volume um novo e, opcionalmente, um novo tamanho e clique em **Criar**. 

**Nota:** o novo tamanho do volume deve ser igual ou superior ao tamanho da captura instantânea. 

## Excluindo uma captura instantânea {: #deleting-snapshot}

1.  Na UI do Bluemix, selecione **Console > Armazenamento**.
2.  Selecione a instância de Armazenamento de bloco que você provisionou anteriormente.
3.	Clique na guia Gerenciar.
4.	Na página Gerenciar, clique na guia **Capturas instantâneas** para obter uma lista de capturas instantâneas.
5.	Selecione a captura instantânea que deseja excluir. A captura instantânea selecionada é destacada.
6.	A partir do menu suspenso Ações, clique em **Excluir**. 



