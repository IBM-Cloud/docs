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

# Níveis de acesso para funções de usuário

As tabelas a seguir mostram o nível de acesso para cada uma das funções de usuário padrão.

As tabelas mostram níveis de acesso para:
- [Operações de dispositivo](#user-device-ops)
- [Operações de log](#user-log-ops)
- [Operações de cache](#user-cache-ops)
<!-- [Historian Operations](#user-historian) -->
- [Operações de organização](#user-org-ops)
- [Operações de controle de acesso](#user-access-ops)
- [Operações de análise de dados](#user-analytics-ops)
- [Operações de terceiros](#user-third-party)  
<!-- - [Risk Management Operations](#user-risk-mgt) -->

## Permissões de Função de Usuário {: #user-roles}

### Operações de Dispositivo {: #user-device-ops}

Operações de Dispositivo ||| Papéis do usuário|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desenvolvedor** | **Analista** | **Leitor**
Criar, atualizar ou excluir dispositivos | P | P | P | - | -
Visualizar dispositivos | P | P | P | P | X
Ativar dispositivo | P | P | P | - | -
Publicar um evento | - | - | - | - | -
Assinar um evento | P | P | P | P | X
Publicar um comando | P | P | P | - | -
Assinar um comando | - | - | - | - | -
Iniciar ação de gerenciamento de dispositivo | P | P | P | - | -
Visualizar ações de gerenciamento de dispositivo | P | P | P | P | X
Limpar ações de gerenciamento de dispositivo | P | P | P | - | -
Gerenciar pacotes configuráveis de ações de gerenciamento de dispositivo | P | P | P | - | -
Criar, atualizar ou excluir tipos de dispositivos | P | P | P | - | -
Visualizar tipos de dispositivos | P | P | P | P | X
Gerenciar logs de diagnóstico | P | P | P | - | -
Visualizar logs de diagnóstico | P | P | P | - | -

### Operações de log {: #user-log-ops}

Operações de log ||| Papéis do usuário|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desenvolvedor** | **Analista** | **Leitor**
Visualizar logs do servidor | P | P | P | P | P

### Operações de cache {: #user-cache-ops}

Operações de cache ||| Papéis do usuário|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desenvolvedor** | **Analista** | **Leitor**
Visualizar dados ativos (cache de eventos) | P | P | P | P | X
Gerenciar dados ativos (cache de eventos) | P	| P | P |	P	| -

### Operações de organização {: #user-org-ops}

Operações de organização ||| Papéis do usuário|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desenvolvedor** | **Analista** | **Leitor**
Configurar parâmetros de armazenamento|	P| - |-|-|-				
Configurar provedor de autenticação|	P|-|-|-|-				
Criar, visualizar, atualizar, excluir configuração de e-mail	|P|-|-|-|-				
Visualizar provedores de e-mail IoTP disponíveis	|P|	P|-|-|-			
Criar, visualizar, atualizar, excluir modelos de correio	|P	|P	|-|-|-		
Criar, atualizar, excluir usuários	|P|	P|-|-|-			
Visualizar usuários	|P|	P|	P|	P|-
Criar, atualizar, excluir convites de usuários|	P	|P	| -|-|-		
Visualizar convites de usuários	|P	|P	|- |- |-		
Preencher convite	|P|	P|	P|	P|	X
Criar, atualizar, excluir chaves API (interface de programação de aplicativos)	|P	|P	| -|-|-		
Visualizar chaves API (interface de programação de aplicativos)	|P	|P	|- |- |-		
Visualizar informações de uso da organização	|P	|P	| -|-|-		

### Operações de controle de acesso {: #user-access-ops}

Operações de controle de acesso ||| Papéis do usuário|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desenvolvedor** | **Analista** | **Leitor**
Visualizar propriedades de usuários, incluindo direitos de acesso	|P|	P|	P|	P| -
Visualizar propriedades próprias dos usuários, incluindo direitos de acesso	|P|	P|	P|	P|	X
Gerenciar usuários, incluindo direitos de acesso	|P	|P	|-|-|-		
Visualizar propriedades de chave API (interface de programação de aplicativos), incluindo direitos de acesso|	P|	P|	P|	P|-
Visualizar propriedades próprias da chave API (interface de programação de aplicativos), incluindo direitos de acesso	|-|	-|	-| -| -		
Criar, atualizar, excluir chave API (interface de programação de aplicativos), incluindo direitos de acesso	|P	|P	|-|-|-		
Visualizar propriedades do dispositivo, incluindo direitos de acesso	|P|	P|	P|	P|	X
Visualizar propriedades próprias do dispositivo, incluindo direitos de acesso	|-	|- |- |- |-		
Criar, atualizar, excluir dispositivo, incluindo direitos de acesso	|P|	P|	P|	-| -
Visualizar funções	|P	|P	|P	|P	|X
Criar, atualizar, excluir funções customizadas	|P	|P |- |- |-
Visualizar operações*	|P	|P	|P	|P	|P

### Operações de análise de dados {: #user-analytics-ops}

Operações de análise de dados ||| Papéis do usuário|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desenvolvedor** | **Analista** | **Leitor**
Visualizar regras de análise de dados|	P|	P|	P|	P|	X
Gerenciar regras de análise de dados|	P|	P|	P|	P| -
Visualizar ações de análise de dados|	P|	P|	P|	P|	X
Gerenciar ações de análise de dados|	P|	P|	P|	P| -
Visualizar alertas de análise de dados|	P|	P|	P|	P|	X
Visualizar esquemas de mensagens de análise de dados|	P|	P|	P|	P|	X
Gerenciar esquemas de mensagens de análise de dados|	P|	P|	P|	P| -

### Operações de serviço de terceiro {: #user-third-party}

Operações de serviço de terceiro ||| Papéis do usuário|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desenvolvedor** | **Analista** | **Leitor**
Processar notificações em lote de plataforma externa	|P|	P	|P |-|-
Processar notificações em lote e enviá-las à plataforma externa	|P|	P	|P| -| -		
Publicar um evento para um dispositivo	|P|	P	|P|	- |-
Assinar eventos a partir de um dispositivo	|P	|P	|P |-| -		
Configurar uma URL (Localizador Uniforme de Recursos) de retorno de chamada da plataforma externa	|P	|P	|P|	-| -		
Configurar o nível de assinatura da plataforma externa|	P|	P|	P |- |-		
Obter status de funcionamento do status do conector	|P|	P	|P	|- |-
Verificar se um sistema externo está ativado e validar credenciais	|P	|P|	P	|- |-
