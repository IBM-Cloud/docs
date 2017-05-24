---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gerenciamento de risco e segurança
{: #RM_security}

É possível aprimorar a segurança para permitir criar, reforçar e relatar sobre a segurança de conexão de dispositivo. Com essa segurança avançada, os certificados e a autenticação transport layer security (TLS) são usados além dos IDs de usuário e dos tokens usados pelo {{site.data.keyword.iot_short_notm}} para determinar como e onde os dispositivos se conectarão à plataforma. Quando os certificados são ativados durante a comunicação entre dispositivos e o servidor, quaisquer dispositivos que não tenham certificados válidos, conforme configurado nas definições de segurança, terão o acesso negado, mesmo se usarem IDs de usuário e senhas válidos.

## Certificados de cliente
{: #certificates}

Para configurar os certificados de cliente e o acesso ao servidor para dispositivos, o operador do sistema importa os certificados de autoridade de certificação (CA) associados e os certificados do servidor do sistema de mensagens para o {{site.data.keyword.iot_short_notm}}. O analista de segurança, então, configura as políticas de segurança de conexão para que as conexões padrão entre os dispositivos e a plataforma usem os níveis de segurança Apenas Certificados ou Certificados com Tokens de Autenticação. O analista pode incluir diferentes políticas para diferentes tipos de dispositivos.

Para obter informações sobre como configurar certificados, veja [Configurando certificados](set_up_certificates.html).

## Planos da organização e políticas de segurança
As políticas de segurança aprimoradas permitem que as organizações determinem como desejam que os dispositivos se conectem e sejam autenticados para a plataforma, usando políticas de conexão e políticas de lista de bloqueio e lista de desbloqueio. As opções de política de segurança que estão disponíveis para uma organização dependem do tipo de plano da organização, como a seguir:

**Plano padrão:**
- Os operadores do sistema podem configurar políticas de conexão com as opções a seguir:
    - TLS opcional 
    - TLS com Autenticação do Token
    - TLS com Autenticação do Token e Autenticação por Certificado de Cliente

**Advanced Security Plan (ASP) ou Plano Lite:** 
- Os operadores do sistema podem configurar políticas de conexão com as opções a seguir:
    - TLS opcional 
    - TLS com Autenticação do Token
    - TLS com Autenticação por Certificado de Cliente
    - TLS com Autenticação do Token e Autenticação por Certificado de Cliente
    - TLS com Certificado de cliente ou Token
- Os operadores do sistema podem configurar listas de bloqueio ou listas de desbloqueio

## Políticas de conexão
{: #connect_policy}

As políticas de conexão reforçam como os dispositivos se conectam à plataforma. É possível configurar políticas de conexão padrão para todos os tipos de dispositivo e criar configurações customizadas para tipos específicos de dispositivo. A política pode ser configurada para permitir conexões não criptografadas, para reforçar conexões Transport Layer Security (TLS) e para permitir que os dispositivos autentiquem com certificados do lado do cliente.

Para obter informações sobre como configurar políticas de segurança de conexão, veja [Configurando políticas de segurança](set_up_policies.html).

A segurança de conexão também pode ser configurada para que os operadores do sistema possam usar seus próprios certificados de servidor de sistema de mensagens, em vez do certificado padrão fornecido. O uso de um certificado de servidor de sistema de mensagens customizado poderá ser útil, no caso de os dispositivos dos usuários serem autenticados no servidor durante o handshake TLS. Apenas os certificados de servidor de sistema de mensagens customizados que usarem o mesmo domínio que o servidor de sistema de mensagens IoTP original usar (<orgId>.messaging.internetofthings.ibmcloud.com) serão suportados.

## Políticas de lista de bloqueio e lista de desbloqueio
{: #wl_bl}

As políticas de lista de bloqueio e lista de desbloqueio fornecem a capacidade de controlar os locais dos quais os dispositivos têm permissão para se conectar à conta da organização. Uma lista de bloqueio identifica todos os endereços IP, CIDRs ou países que devem ter o acesso negado ao servidor, enquanto uma lista de desbloqueio dá acesso explícito aos endereços IP específicos.

Para obter informações sobre como configurar políticas de lista de bloqueio e lista de desbloqueio, veja [Configurando listas de bloqueio e listas de desbloqueio](set_up_policies.html#config_black_white).

## Painel Gerenciamento de Risco e Segurança
{: #dashboard}

Finalmente, o operador do sistema e o analista de segurança podem usar o painel Gerenciamento de Risco e Segurança para visualizar o status geral de segurança. Cartões no painel podem fornecer a eles uma visão geral abrangente da conformidade e também o status de conexão dos dispositivos.
