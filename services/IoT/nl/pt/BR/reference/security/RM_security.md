---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gerenciamento de risco e segurança
{: #RM_security}
Última atualização: 15 de novembro de 2016
{: .last-updated}

O complemento Gerenciamento de Risco e Segurança permite que as organizações aprimorem a segurança do IBM Watson IoT Platform criando, reforçando e relatando a segurança de conexão de dispositivo. Com este complemento, os certificados e a autenticação Transport Layer Security (TLS) são usados, na parte superior dos IDs de usuário e tokens que são usados pelo Watson IoT Platform para determinar como e onde os dispositivos se conectam à plataforma. Durante a comunicação entre dispositivos e o servidor, quaisquer dispositivos que não tenham certificados válidos com acesso ao servidor, como configurado no complemento Gerenciamento de Risco e Segurança, têm o acesso negado, mesmo que usem IDs de usuário e senhas válidos.

**Nota:** Para se inscrever e ativar o programa Beta de Gerenciamento de Risco e Segurança do IBM Watson IoT Platform, acesse https://developer.ibm.com/iotplatform/2016/11/02/experience-the-latest-iot-security-capabilities-sign-up-to-our-november-beta-today/.

## Política de segurança de conexão

A política de Segurança de Conexão reforça como os dispositivos se conectam à plataforma. É possível configurar as políticas de conexão padrão para todos os tipos de dispositivo, bem como as configurações customizadas para tipos específicos de dispositivo. A política pode ser configurada para permitir conexões não criptografadas, para reforçar conexões Transport Layer Security (TLS) e para permitir que os dispositivos autentiquem com certificados do lado do cliente. Quando certificados do lado do cliente estão sendo usados, a política de segurança fornece uma opção adicional de usar apenas o certificado para autenticação de cliente ou usar uma combinação de um certificado de cliente e ID de cliente e par de token de autenticação.   

A segurança de conexão também pode ser configurada para clientes usarem seu próprio certificado do lado do servidor em vez do certificado padrão que é fornecido. Isso pode ser útil, por exemplo, se os dispositivos dos usuários estiverem autenticando o servidor durante o handshake TLS. Nesta liberação inicial do Gerenciamento de Risco e Segurança, o nome de domínio do servidor Watson IoT Platform não pode ser mudado e deve ser usado no estado em que se encontra no certificado do servidor.

## Certificados de cliente

Para configurar os certificados de cliente e o acesso do servidor para dispositivos, o operador do sistema importa os certificados de autoridade de certificação (CA) associados e os certificados do servidor do sistema de mensagens para o Watson IoT Platform. O analista de segurança, então, configura as políticas de segurança de conexão para que as conexões padrão entre os dispositivos e a plataforma usem os níveis de segurança Apenas Certificados ou Certificados com Tokens de Autenticação. O analista pode incluir diferentes políticas para diferentes tipos de dispositivos.

## Políticas de lista de desbloqueio e lista de bloqueio

As políticas de lista de desbloqueio e lista de bloqueio fornecem a capacidade de controlar os locais dos quais os dispositivos têm permissão para se conectar à conta da organização. Uma lista de bloqueio identifica todos os endereços IP, CIDRs ou países que devem ter o acesso negado ao servidor, enquanto uma lista de desbloqueio dá acesso explícito aos endereços IP específicos.

## Painel Gerenciamento de Risco e Segurança

Finalmente, o operador do sistema e o analista de segurança podem usar o painel Gerenciamento de Risco e Segurança para visualizar o status geral de segurança. Cartões no painel podem fornecer a eles uma visão geral abrangente da conformidade e também o status de conexão dos dispositivos.
