---

copyright:
  years: 2017
lastupdated: "2017-5-8"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Trabalhando com Git no Eclipse Orion Web IDE
{: #git_web_ide}

Quando você usa o Eclipse Orion {{site.data.keyword.webide}}, não precisa
do terminal do Git: é possível executar vários comandos comuns do Git no Web IDE.

Não importa onde você codifique, é possível usar essa referência rápida para executar tarefas comuns.

## Criar uma ramificação local
{: #create_branch}

### Eclipse Orion Web IDE
1. Clique na lista **Referência**.

1. Clique em **Nova ramificação**.

2. Digite o nome da ramificação e, em seguida, clique em **Enviar**.

### Terminal do Git
1. Digite `git branch <branchname>` e pressione Enter.

## Trabalhar em uma ramificação local
{: #start_working_on_branch}

### Eclipse Orion Web IDE
1. Clique na lista **Referência** e expanda **local**.

2. Ao lado da ramificação a ser modificada, clique no ícone de check-out
<img  class="inline" src="./images/checkout.png" alt="Ícone de check-out">.

1. Certifique-se de que a ramificação selecionada seja mostrada na lista
**Referência**.

### Terminal do Git
1. Para visualizar suas ramificações locais, digite `git branch -l` e pressione Enter.

2. Digite `git checkout <branchname>` e pressione Enter.


## Atualize uma ramificação local para incluir as mudanças da ramificação
remota
{: #update_branch}

### Eclipse Orion Web IDE
1. Clique em **Sync**.

1. Se você encontrar conflitos, [resolva-os](#resolve_a_rebase_conflict).

### Terminal do Git
1. Digite `git pull` e pressione Enter.

## Excluir uma ramificação local
{: #delete_branch}

### Eclipse Orion Web IDE
1. Certifique-se de que a ramificação a ser excluída não seja retirada. Se essa
ramificação for retirada, [efetue check-out de outra
ramificação](#start_working_on_branch).

1. Clique na lista **Referência** e expanda
**local**.

2. Ao lado da ramificação local a ser removida, clique em
**Excluir**
<img class="inline"  src="./images/delete.png" alt="ícone Excluir">.

### Terminal do Git
1. Digite `git branch -d <branchname>` e pressione Enter.

##Forçar push de mudanças de local para uma ramificação remota
{: #force_push}

Substitua o conteúdo de uma ramificação remota referenciada pelo conteúdo de sua ramificação local ativa.

**Importante:** Quando você forçar o push de uma ramificação
local para uma remota, poderá perder as confirmações na ramificação remota.

### Eclipse Orion Web IDE

1. Na seção Mudanças no diretório ativo, na seção Saída, clique na seta ao
lado de **Enviar por push**.
2. Clique em **Forçar o envio da ramificação por push**.
3. Confirme o aviso.

### Terminal do Git

1. Digite `git push <origin> <remote branch> -f` e
pressione Enter.

## Descarte mudanças desmontadas da ramificação local ativa
{: #discard_changes}

### Eclipse Orion Web IDE
1. Na seção Mudanças no diretório ativo, marque a caixa de seleção de cada arquivo modificado que tenha mudanças que você deseja descartar.
2. Clique no ícone de check-out <img class="inline"  src="./images/discard.png" alt="Efetuar check-out dos arquivos selecionados, descartando todas as mudanças">.

### Terminal do Git
1. Digite `git checkout -- path/to/file/filename` para descartar as mudanças em um arquivo.

## Confirmar arquivos e enviar por push para a ramificação remota
{: #commit}

### Eclipse Orion Web IDE
1. Na seção Mudanças no diretório ativo, marque a caixa de seleção de cada arquivo a ser confirmado.

3. No campo **Inserir a mensagem de confirmação**, digite uma mensagem que descreva suas mudanças.

  **Dica**: Forneça uma mensagem de confirmação detalhada. Sua mensagem deve fornecer detalhes suficientes para que alguém entenda por que a mudança foi necessária sem mais informações. É possível incluir um link para um item no rastreador de problemas da sua equipe para ajudar. A primeira linha da mensagem de confirmação deve conter menos de 50 caracteres. Inclua uma linha em branco antes de incluir outro texto.

4. Clique em **Confirmar**.

5. Clique em **Enviar por push**.

### Terminal do Git
1. Digite `git status` e pressione Enter.

2. Revise as mudanças a serem confirmadas. Se todos os seus arquivos estiverem listados para serem confirmados, continue. Para confirmar arquivos não estagiados, estagie-os primeiro.

3. Digite `git commit` e pressione Enter.

4. Insira o resumo da confirmação, inclua uma linha em branco e inclua a descrição
da confirmação.

  **Dica**: O resumo da confirmação deve ter menos de 50
caracteres. A descrição da confirmação deve fornecer detalhes suficientes para que alguém
entenda por que a mudança foi necessária sem mais informações. É possível incluir um link
para um item no rastreador de problemas da sua equipe para ajudar. 

5. Salve a mensagem de confirmação.

  **Nota:** Para salvar sua mensagem de confirmação e fechar o
Vim, que pode ser seu editor de texto padrão, pressione Esc, digite
`:wq` e pressione Enter.

4. Digite `git push` e pressione Enter.

## Visualizar o histórico de confirmação
{: #view_commit_history}

### Eclipse Orion Web IDE
1. Na seção Ramificação ativa, expanda **Histórico** para ver o
histórico de confirmação dessa ramificação.

  O histórico de confirmação também pode ser visualizado como um gráfico visual conectado.

1. Clique no ícone **alternância de representação gráfica**
<img  class="inline" src="./images/graphicalhistoryicon.png" alt="ícone Histórico gráfico">.

  Quando alternado, o histórico de confirmação e quaisquer mudanças de entrada ou de
saída para a ramificação ativa serão desenhados como um gráfico conectado. A
representação visual mostra todas as confirmações e as ramificações que foram feitas.

  <img class="screen-shot" src="./images/visualhistoryexample.png" alt="Histórico de confirmação visual">

### Terminal do Git
1. Digite `git log` e pressione Enter.

2. Navegue pelas confirmações do responsável.
 * Para visualizar mais entradas, pressione Page Down.
 * Para visualizar entradas anteriores, pressione Page Up.

3. Para parar de visualizar entradas, pressione Q.

## Comparar mudanças que uma confirmação introduziu
{: #compare_changes}

### Eclipse Orion Web IDE
1. Visualize seu histórico de confirmação e localize a confirmação. Para obter
mais informações, consulte [ Visualizar o histórico de confirmação](#view_commit_history).

2. Visualize os detalhes da confirmação clicando nela.

3. Próximo a um arquivo, clique em **>** e revise as mudanças do arquivo.

  **Nota:** Se uma confirmação introduziu uma mudança em uma
linha, a linha original será sombreada de rosa e a nova linha será sombreada de verde. Da mesma forma, as linhas que foram incluídas por uma confirmação são verde sombreado e as linhas que foram removidas são rosa sombreado.

### Terminal do Git
1. Digite `git log -p` e pressione Enter.

  **Nota:** Para visualizar somente um determinado número de
confirmações, digite `git log -p -<number_of_commits_to_view>`.

2. Navegue pelas confirmações.
 * Para visualizar mais entradas, pressione Page Down.
 * Para visualizar entradas anteriores, pressione Page Up.

3. Revise as mudanças.

  **Nota:** Se uma confirmação introduziu uma mudança em uma
linha, a linha original será em texto vermelho e iniciará com um sinal de menos (-). A nova linha será em texto verde e iniciará com um sinal de mais (+).  Da mesma forma, as linhas que foram incluídas por uma confirmação são em texto verde e iniciam com um +. As linhas que foram removidas por uma confirmação são em texto vermelho e iniciam com um -.

1. Para parar de visualizar entradas, pressione Q.

## Modificar a última confirmação
{: #modify_last_commit}

  **Nota:** Ao modificar a última confirmação depois
que enviá-la por push para um repositório remoto, você grava novamente o histórico de
confirmação. Isso pode causar falhas de confirmação e outros problemas para os outros
contribuidores em seu projeto. Certifique-se de que você saiba o que está fazendo
antes de modificar uma confirmação enviada por push para um repositório remoto.

### Eclipse Orion Web IDE
1. Selecione as caixas de seleção para os itens a serem incluídos na confirmação.

1. Marque a caixa de seleção **Corrigir confirmação anterior**.

2. Se necessário, insira uma nova mensagem de confirmação.

3. Clique em **Confirmar**.

### Terminal do Git
1. Verifique seu status. Conforme necessário, estagie ou não estagie os arquivos.

2. Digite `git commit --amend` e pressione Enter.

3. Em seu editor de texto, aceite ou modifique a mensagem de confirmação.

  **Nota:** Para salvar sua mensagem de confirmação e fechar o
Vim, que pode ser seu editor de texto padrão, pressione Esc, digite
`:wq` e pressione Enter.

## Identificar uma confirmação
{: #tag_commit}

### Eclipse Orion Web IDE
1. Visualize seu histórico de confirmação e localize a confirmação. Para obter
mais informações, consulte [ Visualizar o histórico de
confirmação](#view_commit_history).

2. Visualize os detalhes da confirmação clicando nela.

2. Na área de janela de confirmação, clique em **Criar uma tag para a confirmação**
<img class="inline"  src="./images/tag.png" alt="Criar uma tag para a confirmação">.

3. No campo de nome, digite o texto da tag. Clique em
**Enviar**.

### Terminal do Git
1. Visualize o histórico de confirmação e obtenha o ID da confirmação a ser
identificada. Para obter mais informações, consulte [
Visualizar o histórico de confirmação](#view_commit_history).

2. Digite `git tag -a <tag_text> <commit_id>` e
pressione Enter.

## Alterar o nome e o endereço de email do responsável
{: #change_the_committer_name_and_email_address}

### Eclipse Orion Web IDE
1. Clique no ícone de configuração <img class="inline" src="./images/configurations.png" alt="ícone Configuração">.

3. Mude o endereço de e-mail e o nome do usuário atualizando os valores user.email
e user.name. Clique em **Enviar** para salvar cada mudança.

### Terminal do Git
Para atualizar seu nome e endereço de e-mail de um repositório único:

1. Digite `git config user.email "<your@email.com>"` e
pressione Enter.

2. Digite `git config user.name "<Your Name>"` e pressione Enter.

Para atualizar seu nome e endereço de e-mail para todos os repositórios:

1. Digite `git config --global user.email
"<your@email.com>"` e pressione Enter.

2. Digite `git config --global user.name "<Your Name>"` e
pressione Enter.

##Reverter uma confirmação
{: #revert}

Reverta as mudanças que uma confirmação introduziu em sua ramificação ativa.

### Eclipse Orion Web IDE

1. Sob Histórico, selecione uma confirmação.

2. No lado direito da página, acima da resumo da confirmação, clique no ícone Reverter <img class="inline" src="./images/revert.png" alt="ícone Reverter">.

### Terminal do Git

1. Digite `git revert <commit ID>` e pressione Enter.

## Mesclar alterações
{: #merge_changes}

Quando precisar entregar mudanças de uma ramificação de origem para uma ramificação de destino, você deverá primeiro mesclar. Geralmente, a ramificação de origem é aquela na qual você fez mudanças; e a ramificação de destino é sua ramificação principal.

### Eclipse Orion Web IDE
1. Decida quais ramificações serão mescladas.

2. Efetue check-out da ramificação de destino. Para obter mais informações, consulte [Trabalhar em uma ramificação local](#start_working_on_branch).

 <img class="screen-shot" src="./images/destinationbranch.png" alt="Efetuar check-out da ramificação de destino">

1. Clique na lista **Referência**, expanda **local** e clique no nome da ramificação de origem. As mudanças da ramificação de origem são mostradas na seção Recebido.

  <img class="screen-shot" src="./images/sourcebranch.png" alt="As mudanças da ramificação de origem são mostradas na seção Recebido">

1. Na seção Recebido, clique no ícone **Mesclar** <img  class="inline" src="./images/mergeicon.png" alt="ícone Mesclar na seção Recebido">

1. Na lista **Referência**, clique no ícone de check-out ao lado da ramificação na qual você acabou de mesclar as mudanças.

1. Se você quiser entregar as mudanças, clique em **Enviar por push**. Caso contrário, neste momento, é possível criar uma implementação de teste para certificar-se de que tudo está funcionando conforme esperado.

### Terminal do Git
1. Decida quais ramificações serão mescladas.

2. Efetue check-out da ramificação de destino. Para obter mais informações,
consulte [Trabalhar em uma ramificação local](#start_working_on_branch).

3. Digite `git merge <source_name>` e pressione Enter.


## Resolver um conflito de mesclagem
{: #resolve_a_merge_conflict}

### Eclipse Orion Web IDE
1. Na área de janela Arquivos alterados, revise a lista de arquivos que contêm conflitos.

2. No Web IDE, abra cada arquivo que contém conflitos.

3. Resolva cada mudança em conflito.

  **Nota:** Exclua todo o texto que você não deseja manter. Cada conflito está neste formato:

		<<<<<<< HEAD
		Texto na ramificação retirada.
		=======
		Texto na ramificação mesclada.
		>>>>>>> commit_ID_from_merged_branch
4. Para arquivo em conflito, selecione a caixa de seleção. Digite a mensagem
de confirmação da mesclagem e clique em **Confirmar**.

### Terminal do Git
1. Para os arquivos que contêm conflitos, revise a mensagem do Git para os nomes.

2. Em um editor de texto, abra um arquivo que contenha conflitos.

3. Resolva cada mudança em conflito e, em seguida, salve o arquivo.

  **Nota:** Exclua todo o texto que você não deseja manter. Cada conflito está neste formato:

		<<<<<<< HEAD
		Texto na ramificação retirada.
		=======
		Texto na ramificação mesclada.
		>>>>>>> merged_branch
4. Estagie cada arquivo modificado e, em seguida, confirme a mesclagem.

## Rebasear ramificações
{: #rebase_branches}

### Eclipse Orion Web IDE
1. Decida quais ramificações serão rebaseadas. Você rebaseará o conteúdo da ramificação de origem na ramificação de destino.

2. Efetue check-out da ramificação de destino. Para obter mais informações,
consulte [Trabalhar em uma ramificação local](#start_working_on_branch).

1. Clique na lista **Referência**.

1. Clique no nome da ramificação de origem.

1. Na seção Recebido, clique no ícone Rebasear <img  class="inline" src="./images/rebase.png" alt="ícone Rebasear">.

5. Se você encontrar conflitos,
[resolva-os](#resolve_a_rebase_conflict).

6. Repita a etapa anterior quantas vezes forem necessárias para concluir a operação de rebaseamento.

1. Clique na lista **Referência**, expanda
**origem** e clique no nome da ramificação de origem.

1. Clique em **Enviar por push**.

### Terminal do Git
1. Efetue check-out da ramificação a ser atualizada, digitando `git checkout
<destination_branchname>` e pressionando Enter.

2. Digite `git rebase <source_branchname>` e pressione Enter.

3. Se você encontrar conflitos,
[resolva-os](#resolve_a_rebase_conflict).

5. Repita a etapa anterior quantas vezes forem necessárias para concluir a operação de rebaseamento.

  **Nota:** Para parar a operação de rebaseamento, digite
`git rebase --abort` e pressione Enter.

## Resolva um conflito de rebaseamento
{: #resolve_a_rebase_conflict}

### Eclipse Orion Web IDE
1. Na seção Mudanças no diretório ativo, revise a lista de arquivos em conflito.

2. No Web IDE, abra cada arquivo que contém conflitos.

3. Resolva cada mudança em conflito.

  **Nota:** Exclua todo o texto que você não deseja reter. Cada conflito está neste formato:

		<<<<<<< HEAD
		Texto na ramificação retirada.
		=======
		Texto na ramificação mesclada.
		>>>>>>> commit_ID_from_merged_branch
4. Na área de janela de rebaseamento, marque a caixa de seleção de cada arquivo corrigido e clique em **Continuar**.

### Terminal do Git
1. Para os arquivos que contêm conflitos, revise a mensagem do Git para os nomes.

2. Em um editor de texto, abra um arquivo que contenha conflitos.

3. Resolva cada mudança em conflito e, em seguida, salve o arquivo.

  **Nota:** Exclua todo o texto que você não deseja reter. Cada conflito está neste formato:

		<<<<<<< HEAD
		Texto na ramificação retirada.
		=======
		Texto na ramificação mesclada.
		>>>>>>> merged_branch
4. Estagie cada arquivo modificado.

5. Continue a operação de rebaseamento digitando `git rebase --continue` e pressionando Enter.
