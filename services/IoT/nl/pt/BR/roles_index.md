---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Funções de usuário, de aplicativo e de gateway

Funções são conjuntos de permissões que podem ser usados para conceder ou restringir acesso a operações específicas. É possível usar funções para gerenciar permissões para grupos de usuários, aplicativos e gateways.
{:shortdesc}

## Funções do usuário
{: #user_roles}

É possível designar funções de usuário ao incluir, convidar ou registrar um usuário em seu {{site.data.keyword.iot_full}}. Também é possível designar ou mudar funções de usuário a qualquer momento usando o painel do {{site.data.keyword.iot_short_notm}}. Para obter mais informações sobre como designar uma função a um usuário, consulte [Gerenciando funções de usuário](managing_user_roles.html).

As funções de usuário padrão a seguir estão disponíveis:

Atribuição de usuário | Descrição
------------- | -------------
Administrador | Uma função 'super usuário' que concede acesso a todas as APIs (interfaces de programação de aplicativos) relacionados ao usuário. Os administradores não podem acessar operações que são restritas a dispositivos e aplicativos.
Operador | Destinada a usuários da organização de front-end. Concede acesso à maioria das operações da organização, controle de acesso de controle de acesso, operações de análise de dados, operações de terceiros e operações de gerenciamento de risco.
Developer | Concede acesso sem restrição a operações de dispositivo, operações de log, operações de cache, operações de historiador, operações de análise de dados e operações de serviços de terceiros. A função fornece acesso limitado às operações de organização, de controle de acesso e de gerenciamento de risco.
Analista | Concede acesso a operações de análise de dados, incluindo criar, atualizar e excluir regras, ações e esquemas.
Leitor | A função do usuário padrão. Concede acesso limitado a operações que estão disponíveis a todos os usuários.

Para obter mais informações sobre as funções de usuário, consulte [Funções de usuário](reference/roles_access.html).

## Funções de Aplicativo
{: #application_roles}
É possível designar funções de aplicativo para conceder ou negar o acesso de seus aplicativos a operações específicas. Todas as funções de aplicativo negam acesso às operações a seguir:

- Todas as operações de gerenciamento de risco
- Configure os parâmetros de armazenamento
- Configurar provedores de autenticação
- Criar, atualizar ou excluir configuração de e-mail

As funções de aplicativo padrão a seguir estão disponíveis:

Função do Aplicativo | Descrição
------------- | -------------
Padrão | A função de aplicativo padrão. Concede acesso à maioria das operações de aplicativo, mas a nenhuma operação de usuário ou função.   
Operations | Concede acesso à gama mais ampla de operações, mas nega acesso às operações de assinatura ou publicação.
Backend confiável | Destinada a aplicativos que não requerem interação do operador do sistema. Nega acesso às operações de gerenciamento de dispositivo, de organização, de função ou extensão.
Processador de Dados | Destinada a aplicativos que executam análise de dados e processamento de dados. Os aplicativos processadores de dados recebem acesso limitado a operações de organização e operações de usuário, mas têm acesso total às operações de análise de dados, incluindo a criação e gerenciamento de regras, ações e esquemas.
Visualização | Destinada a aplicativos responsáveis por gerar as visualizações de dados. Os aplicativos de visualização têm acesso às operações de dados ativos e armazenados e às operações do painel.
Dispositivo | Destinada a aplicativos que assumem o papel de dispositivos; ou seja, eles fornecem uma fonte de dados que são enviados ao {{site.data.keyword.iot_short_notm}} como se fosse um dispositivo. Aplicativos de dispositivo recebem apenas acesso limitado às operações.

Para obter mais informações sobre o acesso de funções de aplicativo às operações, consulte [Funções de aplicativo](reference/app_roles_access.html).

## Funções de gateway
{: #gateway_roles}
Gateways têm um número limitado de funções que controlam a definição do gateway e a capacidade de registrar dispositivos no {{site.data.keyword.iot_short_notm}}.

As funções de gateway padrão a seguir estão disponíveis:

Função de gateway | Descrição
------------- | -------------
Padrão | A função de gateway padrão. Concede acesso restrito às operações.
Privilegiado | Destinada a gateways confiáveis e permite que gateways privilegiados incluam dispositivos no {{site.data.keyword.iot_short_notm}}. Concede acesso às operações relevantes para incluir, atualizar e gerenciar dispositivos e propriedades do dispositivo, mas não tem acesso a outras operações.  

Para obter mais informações sobre o acesso de funções de gateway às operações, consulte [Funções de gateway](reference/gateway_roles_access.html).
