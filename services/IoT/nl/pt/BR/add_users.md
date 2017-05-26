---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciando o acesso de usuário
{: #managing-user-access}

No painel de membros, é possível controlar e gerenciar o acesso à sua organização do {{site.data.keyword.iot_full}}. É possível incluir usuários incluindo, convidando<!--, registering--> ou importando-os. Também é possível fornecer diferentes níveis de acesso a seus usuários, designando funções.
{:shortdesc}

## Adicionando usuários
{: #adding-new-users}

Na guia **Membros** do painel, é possível incluir membros individuais usando as funções <!--Add, Invite, or Register--> Incluir ou Convidar. Também é possível <!--add, invite, or register-->incluir ou convidar múltiplos membros simultaneamente usando a função Importar.

Por padrão, contas dos membros não expiram. Ao incluir usuários à sua organização do {{site.data.keyword.iot_short_notm}}, é possível configurar opcionalmente uma data de validade para suas contas.

### Incluindo membros em sua organização do {{site.data.keyword.iot_short_notm}}

Para incluir um membro em sua organização, você precisará do IBMid do membro. Para incluir um membro, você não precisa de confirmação do membro.

Para incluir um único membro em sua organização do {{site.data.keyword.iot_short_notm}}:
1. No painel do {{site.data.keyword.iot_short_notm}}, acesse **Membros**.
2. Clique em **Incluir membros** e selecione a guia **Incluir**.
3. Insira o IBMid do membro.
4. Selecione uma função para o membro.
5. Opcional: configure uma data de validade para o membro.
6. Clique em **Incluir**.

Para incluir vários membros simultaneamente, deve-se fazer upload de um arquivo `.csv` que contém o IBMid, a função e a data de expiração opcional de cada membro. Para obter informações, veja [Construindo seu arquivo CSV](#constructing-your-csv).
1. No painel do {{site.data.keyword.iot_short_notm}}, acesse **Membros**.
2. Clique em **Incluir membros** e selecione a guia **Importar**.
3. Procure seus arquivos ou arraste o arquivo `.csv` para a janela **Fazer upload do CSV**.
4. Selecione uma função padrão para usar se uma função especificada no arquivo CSV não for reconhecida.
5. Mapeie os números de coluna no arquivo CSV para as entradas de IBMid, de função e de data de validade (opcional) correspondentes.
6. Selecione o separador de colunas de vírgula ou ponto-e-vírgula apropriado para corresponder ao separador usado no arquivo `.csv`.
7. Clique em **Importar** para importar os IBMids e criar os membros.


### Convidando membros para sua organização do {{site.data.keyword.iot_short_notm}}

Quando você convida um usuário para se tornar um membro de sua organização do {{site.data.keyword.iot_short_notm}}, o usuário recebe um e-mail que contém um link de convite. Os links de convite expiram 48 horas após serem enviados. Se um link de convite não for usado no prazo de 48 horas, o usuário deverá ser convidado novamente para receber um novo link de convite.

**Importante:** o recurso de convite requer um serviço de e-mail configurado. Para obter mais informações, veja a seção E-mail do tópico [Integrações de serviço externo](reference/extensions/index.html#email).

Para convidar um membro para sua organização do {{site.data.keyword.iot_short_notm}}:
1. No painel do {{site.data.keyword.iot_short_notm}}, acesse **Membros**.
2. Selecione a guia **Convites**.
2. Clique em **Convidar membros** e selecione a guia **Convidar**.
3. Inserir o endereço de e-mail do membro.
4. Selecione uma função para este membro.
5. Opcional: configure uma data de validade para o membro.
6. Clique em **Convidar membro**.

Para convidar vários membros simultaneamente, deve-se fazer upload de um arquivo `.csv` que contém o endereço de e-mail, a função e a data de validade opcional de cada membro. Para obter informações, veja [Construindo seu arquivo CSV](#constructing-your-csv).
1. No painel do {{site.data.keyword.iot_short_notm}}, acesse **Membros**.
2. Selecione a guia **Convites**.
2. Clique em **Convidar membros** e selecione a guia **Importar**.
3. Procure seus arquivos ou arraste o arquivo `.csv` para a janela **Fazer upload do CSV**.
4. Selecione uma função padrão para usar se uma função especificada no arquivo CSV não for reconhecida.
5. Mapeie os números de coluna no arquivo CSV para as entradas de endereço de e-mail, de função e de data de validade (opcional) correspondentes.
6. Selecione o separador de colunas de vírgula ou ponto-e-vírgula apropriado para corresponder ao separador usado no arquivo `.csv`.
7. Clique em **Importar** para enviar os convites.

<!-- ### Registering a member with your {{site.data.keyword.iot_short_notm}} organization

If your organization is using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, you can add individual members to your organization by registering them, which does not require an IBMid.

To register a member with your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Enter the subject, realm name, and issuer.
   **Important:** Ensure that the `Subject`, `Realm Name`, and `Issuer` fields comply with the OpenID Connect recommendations and standards. For more information, see the [OpenID Connect ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://openid.net/connect/){: new_window} website.
6. Optional: Set an expiry date for the member.
7. Click **Register Member**.

To register multiple members simultaneously, you must upload a CSV (`.csv`) file that contains the email address, role, subject, realm name, issuer, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Register**.
4. Select a default role and ensure that the column numbers on your CSV file match the column numbers in the CSV settings.
5. Ensure the column separator in your CSV file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the CSV file into the **Upload CSV** window. -->

### Construindo seu arquivo CSV
{: #constructing-your-csv}

Ao construir um arquivo CSV para importar membros para sua organização, assegure que sejam incluídas as informações necessárias para o método que você está usando. Use vírgulas ou pontos e vírgulas para separar colunas.  
**Importante:** ao fazer upload do arquivo CSV, em **Configurações de CSV**, assegure-se de selecionar o separador de colunas correto.

Arquivo de CSV de amostra com delimitação por vírgula:  
```
user1@sample.com,PD_DEVELOPER_USER,1489505652152
user2@sample.com,PD_OPERATOR_USER,1489505652152
user3@sample.com,PD_ADMIN_USER,1489505652152
```

Em que as entradas de coluna a seguir são usadas:  
- Coluna 1: o endereço de e-mail do usuário.  
Se você estiver incluindo membros, certifique-se de usar o endereço de e-mail correspondente a um IBMid válido. Se estiver convidando membros, será possível usar qualquer endereço de e-mail válido.
- Coluna 2: a função a ser designada ao usuário.  
Insira uma das funções a seguir:
 - PD_ADMIN_USER
 - PD_OPERATOR_USER
 - PD_DEVELOPER_USER
 - PD_ANALYST_USER
 - PD_READER_USER  
 Para obter mais informações sobre as funções de usuário, veja [Funções de usuário, aplicativo e gateway](roles_index.html#user_roles).
- Coluna 3: o registro de data e hora do Unix (em milissegundos desde 1 de janeiro de 1970 às 00h UTC) que corresponde à data de validade do usuário.

## Editando usuários
{: #editing-users}

Os usuários podem ser editados para mudar sua função, incluir, remover ou mudar uma data de expiração de acesso ou incluir ou remover o acesso à organização.

1. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Membros** na barra de navegação à esquerda.
2. Clique no ícone **Editar** próximo ao usuário que você deseja editar.
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
2. Clique no ícone **Excluir** próximo ao usuário a ser removido.
3. Clique em **Excluir** no diálogo de confirmação.
