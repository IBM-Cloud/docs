---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Como Gerenciar Usuários {: #manage-users}

Projetado para colaboração da equipe, o {{site.data.keyword.iotrtinsights_short}} permite que os administradores incluam mais usuários para acessar o console do {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Descrições de funções:
- Operador
Os operadores efetuam login diretamente no console do {{site.data.keyword.iotrtinsights_short}} para monitorar o fluxo de dados em tempo real de seus dispositivos e grupos de dispositivos. Os operadores também podem ativar e desativar as regras e modificar painéis editáveis.   
- Administrador
Além das tarefas que um operador pode executar, os administradores podem incluir usuários, gerenciar layouts do teclado, incluir origens de dados e gerenciar tipos de dispositivo.  
- Proprietário
A função de proprietário é designada ao ID IBM que implementou a instância do serviço {{site.data.keyword.iotrtinsights_short}} no Bluemix. Um proprietário tem os mesmos privilégios que um administrador, mas não pode ser excluído.

Para incluir um novo usuário:
1. Inclua o usuário no {{site.data.keyword.iot_short}}.  
>**Importante:** se você estiver incluindo um usuário com a função de administrador, também deve-se incluir esse usuário no {{site.data.keyword.iot_short}}.   

  1. Efetue login no painel do serviço {{site.data.keyword.iot_short}} que é uma origem de dados para o serviço {{site.data.keyword.iotrtinsights_short}}.   
  2. Navegue para **Acesso > Membros** e clique em **Incluir membros**. 
  3. Insira o ID IBM para o usuário que você deseja incluir e clique em **Incluir membros**. 
2. Inclua o usuário no {{site.data.keyword.iotrtinsights_short}}.
  1. Efetue login no console do {{site.data.keyword.iotrtinsights_short}} como um usuário com a função de administrador ou a função de proprietário. 
  2. Acesse **Configurar > Gerenciar usuários**.
  3. Clique em **Incluir novo usuário**.
  4. Insira o endereço de e-mail do usuário que você deseja convidar, selecione uma função para o usuário e clique em ![ícone Criar](images/create.png "ícone Criar"). Um e-mail que contém o link do console da web é enviado ao usuário. Se o endereço de e-mail já estiver associado a um ID IBM, o usuário poderá efetuar login e acessar o console diretamente. Caso contrário, será solicitado ao usuário para criar um ID IBM grátis antes de acessar o console.   
>**Selecionando a instância do Real-Time Insights:** os usuários que têm acesso a várias instâncias do Real-Time Insights como operadores ou administradores podem alternar rapidamente entre essas instâncias. No console do Real-Time Insights, eles podem clicar em seu nome de usuário e selecionar a instância que desejam acessar.   
