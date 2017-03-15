---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-22"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gerenciamento de risco e segurança
{: #RM_security}

O complemento Gerenciamento de risco e segurança permite que as organizações aprimorem a segurança do {{site.data.keyword.iot_full}} criando, aplicando e relatando a segurança de conexão de dispositivo. Com esse complemento, os certificados e a autenticação transport layer security (TLS) são usados sobre os IDs de usuário e os tokens usados pelo {{site.data.keyword.iot_short_notm}} para determinar como e onde os dispositivos se conectam à plataforma. Durante a comunicação entre dispositivos e o servidor, quaisquer dispositivos que não tenham certificados válidos com acesso ao servidor, como configurado no complemento Gerenciamento de Risco e Segurança, têm o acesso negado, mesmo que usem IDs de usuário e senhas válidos.

## Política de segurança de conexão
{: #connect_policy}

A política Segurança da conexão impõe como os dispositivos se conectam à plataforma e como eles são usados com os planos de segurança Grátis e Avançado. É possível configurar as políticas de conexão padrão para todos os tipos de dispositivo, bem como as configurações customizadas para tipos específicos de dispositivo. A política pode ser configurada para permitir conexões não criptografadas, para reforçar conexões Transport Layer Security (TLS) e para permitir que os dispositivos autentiquem com certificados do lado do cliente.

Se você usar um plano de segurança padrão, as políticas de conexão não estarão disponíveis. Para obter informações sobre como configurar políticas de segurança de conexão, veja [Configurando políticas de segurança](set_up_policies.html).

A segurança de conexão também pode ser configurada para clientes usarem seu próprio certificado do lado do servidor em vez do certificado padrão que é fornecido. Isso poderá ser útil, por exemplo, no caso de os dispositivos dos usuários serem autenticados no servidor durante o handshake TLS. Nesta liberação inicial do Gerenciamento de risco e segurança, o nome de domínio do servidor {{site.data.keyword.iot_short_notm}} não pode ser mudado e deve ser usado no estado em que se encontra no certificado do servidor.



## Certificados de cliente
{: #certificates}

Para configurar os certificados de cliente e o acesso ao servidor para dispositivos, o operador do sistema importa os certificados de autoridade de certificação (CA) associados e os certificados do servidor do sistema de mensagens para o {{site.data.keyword.iot_short_notm}}. O analista de segurança, então, configura as políticas de segurança de conexão para que as conexões padrão entre os dispositivos e a plataforma usem os níveis de segurança Apenas Certificados ou Certificados com Tokens de Autenticação. O analista pode incluir diferentes políticas para diferentes tipos de dispositivos.

Para obter informações sobre como configurar certificados, veja [Configurando certificados](set_up_certificates.html).

## Políticas de lista de bloqueio e lista de desbloqueio
{: #wl_bl}

As políticas de lista de bloqueio e lista de desbloqueio fornecem a capacidade de controlar os locais dos quais os dispositivos têm permissão para se conectar à conta da organização. Uma lista de bloqueio identifica todos os endereços IP, CIDRs ou países que devem ter o acesso negado ao servidor, enquanto uma lista de desbloqueio dá acesso explícito aos endereços IP específicos.

Para obter informações sobre como configurar políticas de lista de bloqueio e lista de desbloqueio, veja [Configurando listas de bloqueio e listas de desbloqueio](set_up_policies.html#config_black_white).

## Painel Gerenciamento de Risco e Segurança
{: #dashboard}

Finalmente, o operador do sistema e o analista de segurança podem usar o painel Gerenciamento de Risco e Segurança para visualizar o status geral de segurança. Cartões no painel podem fornecer a eles uma visão geral abrangente da conformidade e também o status de conexão dos dispositivos.
