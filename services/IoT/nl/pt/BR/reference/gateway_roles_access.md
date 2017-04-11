---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Níveis de acesso para funções de gateway

As tabelas a seguir mostram o nível de acesso para cada uma das funções de gateway.

As tabelas mostram níveis de acesso para:
- [Operações de dispositivo](#gateway-device-ops)
- [Operações de log](#gateway-log-ops)
- [Operações de cache](#gateway-cache-ops)
<!-- [Historian Operations](#gateway-historian) -->
- [Operações de organização](#gateway-org-ops)
- [Operações de controle de acesso](#gateway-access-ops)
- [Operações de análise de dados](#gateway-analytics-ops)
- [Operações de terceiros](#gateway-third-party)  
<!-- - [Risk Management Operations](#gateway-risk-mgt) -->

## Funções de gateway
{: #gateway-roles}

### Operações de Dispositivo {: #gateway-device-ops}

Operações de Dispositivo || Funções de gateway|
:--------: | ---------------------|------------------------
           | **Gateway padrão** | **Gateway privilegiado**
Criar, atualizar ou excluir dispositivos|-|X
Visualizar dispositivos|P|X
Ativar dispositivo|-|X
Publicar um evento|P|X
Assinar um evento|-|-
Publicar um comando|-|-
Assinar um comando|P|X
Iniciar ação de gerenciamento de dispositivo|P|X
Visualizar ações de gerenciamento de dispositivo|P|X
Limpar ações de gerenciamento de dispositivo|-|-
Gerenciar pacotes configuráveis de ações de gerenciamento de dispositivo|-|X
Criar, atualizar ou excluir tipos de dispositivos|-|-
Visualizar tipos de dispositivos|P|X
Gerenciar logs de diagnóstico|-|-
Visualizar logs de diagnóstico|-|-

### Operações de log {: #gateway-log-ops}

Operações de log || Funções de gateway|
:--------: | ---------------------|------------------------
           | **Gateway padrão** | **Gateway privilegiado**
Visualizar logs do servidor|-|-

### Operações de cache {: #gateway-cache-ops}

Operações de cache || Funções de gateway|
:--------: | ---------------------|------------------------
           | **Gateway padrão** | **Gateway privilegiado**
Visualizar dados ativos (cache de eventos)|-|-
Gerenciar dados ativos (cache de eventos)|-|-


### Operações de organização {: #gateway-org-ops}

Operações de organização || Funções de gateway|
:--------: | ---------------------|------------------------
           | **Gateway padrão** | **Gateway privilegiado**
Configurar parâmetros de armazenamento|-|-				
Configurar provedor de autenticação|-|-				
Criar, visualizar, atualizar ou excluir configuração de e-mail|-|-				
Visualizar provedores de e-mail disponíveis|-|-			
Criar, visualizar, atualizar ou excluir modelos de correio|-|-		
Criar, atualizar ou excluir usuários|-|-			
Visualizar usuários|-|-
Criar, atualizar, excluir convites de usuários|-|-		
Visualizar convites de usuários|-|-		
Preencher convite|-|-		
Criar, atualizar ou excluir chaves API (interface de programação de aplicativos)|-|-		
Visualizar chaves API (interface de programação de aplicativos)|-|-		
Visualizar informações de uso da organização|-|-

### Operações de controle de acesso {: #gateway-access-ops}

Operações de controle de acesso || Funções de gateway|
:--------: | ---------------------|------------------------
           | **Gateway padrão** | **Gateway privilegiado**
Visualizar propriedades de usuários (incluindo direitos de acesso)|-|-
Visualizar propriedades próprias dos usuários (incluindo direitos de acesso)|-|-
Gerenciar usuários (incluindo direitos de acesso)|-|-		
Visualizar propriedades da chave API (incluindo direitos de acesso)|-|-		
Visualizar propriedades próprias da chave API (incluindo direitos de acesso)|-|-		
Criar, atualizar ou excluir chaves API (incluindo direitos de acesso)|-|-
Visualizar propriedades do dispositivo (incluindo direitos de acesso)|P|X
Visualizar propriedades próprias do dispositivo (incluindo direitos de acesso)|P|X		
Criar, atualizar, excluir dispositivo (incluindo direitos de acesso)|-|X
Visualizar funções|-|-
Criar, atualizar, excluir funções customizadas|-|-
Visualizar operações|-|-

### Operações de análise de dados {: #gateway-analytics-ops}

Operações de análise de dados || Funções de gateway|
:--------: | ---------------------|------------------------|
           | **Gateway padrão** | **Gateway privilegiado** |
Visualizar regras de análise de dados|-|-
Gerenciar regras de análise de dados|-|-
Visualizar ações de análise de dados|-|-
Gerenciar ações de análise de dados|-|-
Visualizar alertas de análise de dados|-|-
Visualizar esquemas de mensagens de análise de dados|-|-
Gerenciar esquemas de mensagens de análise de dados|-|-

### Operações de serviço de terceiro {: #gateway-third-party}

Operações de serviço de terceiro || Funções de gateway|
:--------: | ---------------------|------------------------
           | **Gateway padrão** | **Gateway privilegiado**
Processar notificações em lote de plataforma externa|-|-
Processar notificações em lote e enviá-las à plataforma externa|-|-		
Publicar um evento para um dispositivo|-|-
Assinar eventos a partir de um dispositivo|-|-		
Configurar uma URL (Localizador Uniforme de Recursos) de retorno de chamada da plataforma externa|-|-		
Configurar o nível de assinatura da plataforma externa|-|-		
Obter status de funcionamento do status do conector|-|-
Verificar se um sistema externo está ativado e validar credenciais|-|-
