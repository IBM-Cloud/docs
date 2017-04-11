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

# Níveis de acesso para funções de aplicativo

As tabelas a seguir mostram o nível de acesso para cada uma das funções de aplicativo.

As tabelas mostram níveis de acesso para:
- [Operações de dispositivo](#app-device-ops)
- [Operações de log](#app-log-ops)
- [Operações de cache](#app-cache-ops)
<!-- [Historian Operations](#app-historian) -->
- [Operações de organização](#app-org-ops)
- [Operações de controle de acesso](#app-access-ops)
- [Operações de análise de dados](#app-analytics-ops)
- [Operações de terceiros](#app-third-party)  
<!-- - [Risk Management Operations](#app-risk-mgt) -->

## Application Roles
{: #app-roles}

### Operações de Dispositivo {: #app-device-ops}

Operações de Dispositivo ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicativo padrão** | **Aplicativo de operações** | **Aplicativo confiável de backend** | **Aplicativo de processador de dados** | **Aplicativo de visualização** | **Aplicativo de dispositivo**
Criar, atualizar ou excluir dispositivos|P|P|P|-|-|-
Visualizar dispositivos|P|P|P|P|P|-
Ativar dispositivo|P|P|P|-|-|-
Publicar um evento|P|-|P|-|-|X
Assinar um evento|P|P|P|P|P|X
Publicar um comando|P|P|P|P|-|-
Assinar um comando|P|-|P|-|-|X
Iniciar ação de gerenciamento de dispositivo|P|P|-|-|-|-
Visualizar ações de gerenciamento de dispositivo|P|P|-|-|-|X
Limpar ações de gerenciamento de dispositivo|P|P|-|-|-|-
Gerenciar pacotes configuráveis de ações de gerenciamento de dispositivo|P|P|-|-|-|-
Criar, atualizar ou excluir tipos de dispositivos|P|P|P|-|-|-
Visualizar tipos de dispositivos|P|P|P|P|-|-
Gerenciar logs de diagnóstico|P|P|-|-|-|X
Visualizar logs de diagnóstico|P|P|P|-|-|-

### Operações de log {: #app-log-ops}

Operações de log ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicativo padrão** | **Aplicativo de operações** | **Aplicativo confiável de backend** | **Aplicativo de processador de dados** | **Aplicativo de visualização** | **Aplicativo de dispositivo**
Visualizar logs do servidor|P|P|P|-|-|-

### Operações de cache {: #app-cache-ops}

Operações de cache ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicativo padrão** | **Aplicativo de operações** | **Aplicativo confiável de backend** | **Aplicativo de processador de dados** | **Aplicativo de visualização** | **Aplicativo de dispositivo**
Visualizar dados ativos (cache de eventos)|P|P|P|P|P|X
Gerenciar dados ativos (cache de eventos)|P|P|P|P|P|P

### Operações de organização {: #app-org-ops}

Operações de organização ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicativo padrão** | **Aplicativo de operações** | **Aplicativo confiável de backend** | **Aplicativo de processador de dados** | **Aplicativo de visualização** | **Aplicativo de dispositivo**
Configurar parâmetros de armazenamento|-|-|-|-|-|-				
Configurar provedor de autenticação|-|-|-|-|-|-				
Criar, visualizar, atualizar ou excluir configuração de e-mail|-|-|-|-|-|-				
Visualizar provedores de e-mail disponíveis|P|P|-|-|-|-			
Criar, visualizar, atualizar ou excluir modelos de correio|P|P|-|-|-|-		
Criar, atualizar ou excluir usuários|-|P|-|-|-|-			
Visualizar usuários|P|P|-|-|-|-
Criar, atualizar ou excluir convites de usuários|-|P|-|-|-|-		
Visualizar convites de usuários|P|P|-|-|-|-		
Preencher convite|P|P|-|-|-|-		
Criar, atualizar ou excluir chaves API (interface de programação de aplicativos)|-|P|-|-|-|-		
Visualizar chaves API (interface de programação de aplicativos)|P|P|-|-|-|-		
Visualizar informações de uso da organização|P|P|-|-|-|-

### Operações de controle de acesso {: #app-access-ops}

Operações de controle de acesso ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicativo padrão** | **Aplicativo de operações** | **Aplicativo confiável de backend** | **Aplicativo de processador de dados** | **Aplicativo de visualização** | **Aplicativo de dispositivo**
Visualizar propriedades de usuários, incluindo direitos de acesso|P|P|-|-|-|-
Visualizar propriedades próprias dos usuários, incluindo direitos de acesso|-|-|-|-|-|-
Gerenciar usuários, incluindo direitos de acesso|-|P|-|-|-|-		
Visualizar propriedades de chave API (interface de programação de aplicativos), incluindo direitos de acesso|P|P|-|-|-|-
Visualizar propriedades próprias da chave API (interface de programação de aplicativos), incluindo direitos de acesso|P|P|P|P|P|X		
Criar, atualizar, excluir chaves API (interface de programação de aplicativos), incluindo direitos de acesso|-|P|-|-|-|-		
Visualizar propriedades do dispositivo, incluindo direitos de acesso|P|P|P|P|P|-
Visualizar propriedades próprias do dispositivo, incluindo direitos de acesso|-|-|-|-|-|-		
Criar, atualizar, excluir dispositivo, incluindo direitos de acesso|P|P|P|-|-|-
Visualizar funções|P|P|-|-|-|-
Criar, atualizar, excluir funções customizadas|-|P|-|-|-|-
Visualizar operações*|P|P|-|-|-|-

### Operações de análise de dados {: #app-analytics-ops}

Operações de análise de dados ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicativo padrão** | **Aplicativo de operações** | **Aplicativo confiável de backend** | **Aplicativo de processador de dados** | **Aplicativo de visualização** | **Aplicativo de dispositivo**
Visualizar regras de análise de dados|P|P|-|P|P|-
Gerenciar regras de análise de dados|P|P|-|P|-|-
Visualizar ações de análise de dados|P|P|-|P|P|-
Gerenciar ações de análise de dados|P|P|-|P|P|-
Visualizar alertas de análise de dados|P|P|-|P|P|X
Visualizar esquemas de mensagens de análise de dados|P|P|-|P|P|-
Gerenciar esquemas de mensagens de análise de dados|P|P|-|P|-|-

### Operações de serviço de terceiro {: #app-third-party}

Operações de serviço de terceiro ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicativo padrão** | **Aplicativo de operações** | **Aplicativo confiável de backend** | **Aplicativo de processador de dados** | **Aplicativo de visualização** | **Aplicativo de dispositivo**
Processar notificações em lote de plataforma externa|P|P|-|-|-|-
Processar notificações em lote e enviá-las à plataforma externa|P|P|-|-|-|-		
Publicar um evento para um dispositivo|P|P|-|-|-|-
Assinar eventos a partir de um dispositivo|P|P|-|-|-|-		
Configurar uma URL (Localizador Uniforme de Recursos) de retorno de chamada da plataforma externa|P|P|-|-|P|-		
Configurar o nível de assinatura da plataforma externa|P|P|-|-|P|-		
Obter status de funcionamento do status do conector|P|P|P|-|P|-
Verificar se um sistema externo está ativado e validar credenciais|P|P|P|-|P|-
