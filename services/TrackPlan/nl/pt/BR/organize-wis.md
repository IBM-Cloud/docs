---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Organizando e filtrando itens de trabalho {: #tp-organize}  

*Última atualização: 29 de abril de 2016*
{: .last-updated}

O serviço do {{site.data.keyword.trackplan}} inclui várias opções para classificar e organizar os seus itens de trabalho.
{: shortdesc}

##Filtrando itens de trabalho {: #tp-filteringwis}

É possível filtrar itens de trabalho com base em palavras ou em valores para atributos específicos. 

A filtragem é suportada nestas visualizações:   
- Meu Trabalho
- Meus inscritos
- Trabalho recebido
- Trabalho Acumulado
- Planejamento de sprint
- Trabalho da Equipe
- Todos os Trabalhos

Se você digitar uma palavra, os resumos de item de trabalho que contiverem essa palavra serão mostrados. Também é possível filtrar itens de trabalho com base em
valores para atributos específicos. Para obter detalhes, consulte a tabela a seguir.

| Atributo |Exemplo | 
|-------|-------|
|*Tipo  | `*Defect` |
|#Tag  | `#conference`| 
|@:Owner  | `@:jasmith`|
|$Priority|`$High`|
|!Severity|`!Major`|       
   

É possível criar consultas que usam qualquer atributo de item de trabalho digitando o nome do atributo. Por exemplo, se você digitar `Created
by`, as opções de consulta e a sintaxe serão mostradas. É possível usar operadores, como "e," "ou" e "não" em seus critérios de filtro. Também é possível
incluir operações complexas que aninham múltiplos operadores usando parênteses. Para ver exemplos, clique no ícone **Ajuda**.
![ícone Ajuda de filtro](images/filter_helpicon.png)

Quando você clica no campo **Filtrar itens de trabalho por palavra-chave**, os operadores e filtros que você pode usar para criar consultas são mostrados.

![Filtrando com opções de conclusão automática](images/filterMenu2.png)

##Salvando visualizações customizadas {: #tp-customviews}
É possível criar visualizações customizadas aplicando filtros. Em seguida, é possível compartilhar as visualizações com a sua equipe.    

1. No campo **Filtrar itens de trabalho**, digite a forma curta de um tipo de atributo e um valor para esse atributo, por exemplo,
`$high`. Algumas opções de atributo são automaticamente listadas quando você digita a forma curta, por exemplo, *Type, $Priority e !Severity.
![Filtrar com tipos de atributo e atributos](images/filterAttributes.png)
2. Clique em **SALVAR**.
3. Nome da visualização. 
4. Se você desejar que a visualização customizada inclua o sprint que você está visualizando, marque a caixa de seleção para incluir o sprint. No exemplo a
seguir, o sprint de Lista não processada será incluído na visualização "Lista não processada de alta prioridade".
![Salvar o diálogo de visualização customizada com o sprint incluído](images/filterIncludeSprints.png)
5. Clique em **SALVAR**. 
6. Se você desejar compartilhar as suas visualizações salvas com a sua equipe, na seção Visualizações customizadas, clique no ícone compartilhar ao lado da
nova visualização. Em seguida, clique em **OK**.
![Seta de visualização customizada de compartilhamento](images/filterShare.png)

Visualizações customizadas retornam resultados apenas para o sprint e o status atuais que você está visualizando. Se você desejar que a visualização retorne
resultados para mais sprints ou status, clique na visualização e mude-a conforme necessário.

##Visualizando e organizando os seus itens de trabalho {: #tp-organizingwis}

- Para visualizar itens de trabalho de sua propriedade, veja a visualização Meu trabalho. 
- Se você usar itens de trabalho específicos frequentemente, será possível marcá-los como seus favoritos clicando em seus ícones de Estrela <img class="inline"  src="./images/star.gif" alt="ícone de Estrela">. Em seguida, será possível ver todos os seus itens de trabalho favoritos na visualização Meus
marcados com estrela. Quando você clica no ícone de Estrela para um item de trabalho, somente você pode ver que o marcou como um favorito.  
- Para visualizar todos os itens de trabalho nos quais você está inscrito, veja a visualização Meus inscritos.
- Para visualizar os seus itens de trabalho classificados por suas datas de modificação, veja a visualização Meu trabalho recente.
- Para visualizar a atividade do seu item de trabalho, veja a visualização Minhas atividades. A seção Meus eventos lista os itens de trabalho nos quais você
foi mencionado. A seção Minhas assinaturas lista todas as mudanças que ocorreram em itens de trabalho nos quais você está inscrito.

##Acionando Itens de Trabalho {: #tp-triaging}

Quando um item de trabalho é criado, mas não designado para um sprint, o item de trabalho é mostrado na visualização Trabalho recebido.
Assim que um item de trabalho é designado a um sprint, ele é removido da visualização Trabalho recebido.

Na visualização Trabalho recebido, é possível fazer a triagem de itens de trabalho de várias maneiras: 
- Para rejeitar o item de trabalho, clique no ícone **Colocar este item na lixeira**
<img class="inline"  src="./images/trash.gif" alt="ícone Colocar este item na lixeira">. O item de trabalho será resolvido e o seu status será mudado para Inválido.
- Para aceitar o item de trabalho e designá-lo para a Lista não processada, clique no ícone **Triagem para lista não processada**
<img  class="inline" src="./images/triage.gif" alt="ícone Triagem para lista não processada">. Em seguida, será possível avaliar o item de trabalho com relação a outros itens de trabalho na visualização
Planejamento de sprint e designar o item de trabalho para um sprint.
- Para designar o item de trabalho para um sprint, abra o item de trabalho e selecione um
valor na lista **Planejado para**.

![Fazendo triagem de itens de trabalho na visualização Trabalho recebido](images/incoming_work_attributes.png)  

Para obter mais informações sobre como gerenciar itens de trabalho,
[veja
Gerenciando um projeto com o Planejador Rápido](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.1/com.ibm.team.concert.tutorial.doc/topics/tut_quick_planner_lesson.html).
