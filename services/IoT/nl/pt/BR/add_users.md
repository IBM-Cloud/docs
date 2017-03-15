---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciando o acesso de usuário

No painel de acesso, é possível controlar e gerenciar o acesso à sua organização do {{site.data.keyword.iot_full}}. É possível incluir usuários incluindo, convidando, registrando ou importando os mesmos. Também é possível fornecer diferentes níveis de acesso a seus usuários designando funções.
{:shortdesc}

- [Incluindo novos usuários](#adding-new-users)
- [Editando usuários](#editing-users)
- [Bloqueando o acesso de usuário](#blocking-users)
- [Removendo usuários](#removing-users)

## Incluindo novos usuários
{: #adding-new-users}

Na guia **Acesso** do painel, é possível incluir membros individuais usando as funções Incluir, Convidar ou Registrar. Também é possível incluir, convidar ou registrar vários membros simultaneamente usando a função Importar.

Por padrão, contas dos membros não expiram. Ao incluir usuários à sua organização do {{site.data.keyword.iot_short_notm}}, é possível configurar opcionalmente uma data de validade para suas contas.

### Incluindo membros em sua organização do {{site.data.keyword.iot_short_notm}}

Para incluir um membro em sua organização, você precisará do IBMid do membro. Para incluir um membro, você não precisa de confirmação do membro.

Para incluir um único membro em sua organização do {{site.data.keyword.iot_short_notm}}:
1. No painel do {{site.data.keyword.iot_short_notm}}, vá para **Acessar**.
2. Clique em **Incluir membro** e selecione **Incluir**.
3. Insira o IBMid do membro.
4. Selecione uma função para o membro.
5. Opcional: configure uma data de validade para o membro.
6. Clique em **Incluir membro**.

Para incluir vários membros simultaneamente, deve-se fazer upload de um arquivo `.csv` que contém o IBMid, a função e a data de expiração opcional de cada membro.
1. No painel do {{site.data.keyword.iot_short_notm}}, vá para **Acessar**.
2. Clique em **Incluir membro** e selecione **Importar**.
3. Clique em **Inclusão em massa**.
4. Selecione uma função padrão e assegure que os números das colunas em seu `arquivo .csv` correspondam aos números das colunas nas configurações de CSV.
5. Assegure que o separador de colunas em seu arquivo `.csv` corresponda ao separador de colunas nas configurações de CSV.
6. Clique em **Procurar seus arquivos** ou arraste o arquivo `.csv` para a janela **Fazer upload do CSV**.

### Convidando membros para sua organização do {{site.data.keyword.iot_short_notm}}

Quando você convida um usuário para se tornar um membro de sua organização do {{site.data.keyword.iot_short_notm}}, o usuário recebe um e-mail que contém um link de convite. Os links de convite expiram 48 horas após serem enviados. Se um link de convite não for usado no prazo de 48 horas, o usuário deverá ser convidado novamente para receber um novo link de convite.

Para convidar um membro para sua organização do {{site.data.keyword.iot_short_notm}}:
1. No painel do {{site.data.keyword.iot_short_notm}}, vá para **Acessar**.
2. Clique em **Incluir membro** e selecione **Convidar**.
3. Inserir o endereço de e-mail do membro.
4. Selecione uma função para este membro.
5. Opcional: configure uma data de validade para o membro.
6. Clique em **Convidar membro**.

Para convidar vários membros simultaneamente, deve-se fazer upload de um arquivo `.csv` que contém o endereço de e-mail, a função e a data de validade opcional de cada membro.
1. No painel do {{site.data.keyword.iot_short_notm}}, vá para **Acessar**.
2. Clique em **Incluir membro** e selecione **Importar**.
3. Clique em **Convite em massa**.
4. Selecione uma função padrão e assegure que os números das colunas em seu arquivo `.csv` correspondam aos números das colunas nas configurações de CSV.
5. Assegure que o separador de colunas em seu arquivo `.csv` corresponda ao separador de colunas nas configurações de CSV.
6. Clique em **Procurar seus arquivos** ou arraste o arquivo `.csv` para a janela **Fazer upload do CSV**.

### Registrando um membro com sua organização do {{site.data.keyword.iot_short_notm}}

Se sua organização não estiver usando o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, será possível incluir membros individuais em sua organização registrando-os, o que não requer um IBMid.

Para registrar um membro em sua organização do {{site.data.keyword.iot_short_notm}}:
1. No painel do {{site.data.keyword.iot_short_notm}}, vá para **Acessar**.
2. Clique em **Incluir membro** e selecione **Convidar**.
3. Inserir o endereço de e-mail do membro.
4. Selecione uma função para este membro.
5. Insira o assunto, o nome da região e do emissor.
   **Importante:** assegure que os campos `Assunto`, `Nome da região` e `Emissor` obedeçam as recomendações e normas do OpenID Connect. Para obter mais informações, consulte o website do [OpenID Connect ![Ícone de link externo](../../icons/launch-glyph.svg)](http://openid.net/connect/){: new_window}.
6. Opcional: configure uma data de validade para o membro.
7. Clique em **Registrar membro**.

Para registrar vários membros simultaneamente, deve-se fazer upload de um arquivo CSV (`.csv`) que contém o endereço de e-mail, a função, o assunto, o nome da região, o emissor e a data de validade opcional de cada membro.
1. No painel do {{site.data.keyword.iot_short_notm}}, vá para **Acessar**.
2. Clique em **Incluir membro** e selecione **Importar**.
3. Clique em **Registro em massa**.
4. Selecione uma função padrão e assegure que os números das colunas em seu arquivo CSV correspondam aos números das colunas nas configurações de CSV.
5. Assegure que o separador de colunas em seu arquivo CSV corresponda ao separador de colunas nas configurações de CSV.
6. Clique em **Procurar seus arquivos** ou arraste o arquivo CSV para a janela **Fazer upload do CSV**.

### Construindo seu arquivo CSV

Ao construir um arquivo CSV para importar membros para sua organização, assegure que sejam incluídas as informações necessárias para o método que você está usando. Use vírgulas ou pontos e vírgulas para separar colunas. Ao fazer upload do arquivo CSV, em **Configurações de CSV**, assegure que o separador de colunas correto seja selecionado.

## Editando usuários
{: #editing-users}

Os usuários podem ser editados para mudar sua função, incluir, remover ou mudar uma data de expiração de acesso ou incluir ou remover o acesso à organização.

1. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Membros** na barra de navegação à esquerda.
2. Clique no ícone **Editar** ![Editar](/docs/images/edit_32.svg) próximo ao usuário que você deseja editar.
3. Faça as mudanças desejadas no usuário.
4. Clique em **Salvar**.

## Bloqueando o acesso de usuário
{: #blocking-users}

Os usuários podem ser bloqueados contra o acesso à organização do {{site.data.keyword.iot_short_notm}}, enquanto ainda mantêm a associação à organização.

1. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Membros** na barra de navegação à esquerda.
2. Clique na alternância próxima ao usuário que você deseja bloquear contra o acesso à organização do {{site.data.keyword.iot_short_notm}}.


## Removendo usuários
{: #removing-users}

Os usuários podem ser removidos completamente da organização do {{site.data.keyword.iot_short_notm}}. A remoção dos usuários não pode ser desfeita e os usuários devem ser [incluídos na plataforma](#adding-new-users) para restaurar o acesso.

1. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Membros** na barra de navegação à esquerda.
2. Clique no ícone **Excluir** ![Excluir](/docs/images/trash_32.svg) próximo ao usuário a ser removido.
3. Clique em **Excluir** no diálogo de confirmação.
