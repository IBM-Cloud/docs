---

copyright:
  years: 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciando o acesso de usuário
Última atualização: 16 de setembro de 2016
{: .last-updated}

No painel de acesso, é possível controlar e gerenciar o acesso à sua organização do {{site.data.keyword.iot_full}}. É possível incluir usuários incluindo, convidando, registrando ou importando os mesmos. Também é possível fornecer diferentes níveis de acesso a seus usuários designando funções.
{:shortdesc}

## Acesso ao usuário

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
   **Importante:** assegure que os campos `Assunto`, `Nome da região` e `Emissor` obedeçam as recomendações e normas do OpenID Connect. Para obter mais informações, consulte o website do [OpenID Connect](http://openid.net/connect/).
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
