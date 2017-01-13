---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configurando certificados
{: #set_up_certificates.md}
Última atualização: 15 de novembro de 2016
{: .last-updated}

Ao usar o complemento Gerenciamento de Risco e Segurança, os certificados são usados para autenticação de dispositivo ou para substituir o certificado do servidor IBM Watson IoT Platform padrão para o sistema de mensagens MQTT. Todos os dispositivos que não têm certificados assinados válidos têm acesso negado e não podem se comunicar com o servidor.

Para configurar certificados e acesso ao servidor para dispositivos, o operador do sistema registra os certificados de autoridade de certificação (CA) associados e, como opção, registra os certificados do servidor de mensagens no Watson IoT Platform.

## Requisitos do certificado

O certificado que você registra deve ter o ID do dispositivo inserido como Nome Comum (CN) ou SubjectAltName no certificado. Para o campo *CN*, o formato é CN=d:devtype:devid. Para o campo SubjectAltName, o formato é: SubjectAltName=d:devtype:devid, em que devtype é o Tipo de Dispositivo do dispositivo e devid é o ID do Cliente do dispositivo.

O uso de uma lista de revogação de certificado (CRL), para indicar quais dispositivos não têm mais permissão para conectar, não é suportado na liberação Beta.

Se você incluir um certificado de CA ou substituir o certificado do servidor de sistema de mensagens, todos os dispositivos deverão se conectar usando um cliente MQTT que suporte a Indicação de Nome do Servidor (SNI). Com a arquitetura de ocupação variada, a SNI informa ao servidor MQTT quais certificados devem ser usados para a conexão de cada organização/locatário.

##Registrando certificados de Autoridade de Certificação (CA) para autenticação de dispositivo

1. Efetue login no Watson IoT Platform e navegue para **Configurações Gerais**.
2. Na seção **Gerenciamento de Risco**, em **Certificados de CA**, clique em **Incluir Certificado**.
3. Navegue para selecionar um arquivo de certificado para fazer upload ou arrastar e soltar um arquivo na janela **Incluir Certificado**. O arquivo pode ter apenas um certificado dentro dele e as datas do certificado devem ser válidas. Os arquivos que possuem as extensões .pem, .cer, .cert ou .crt são aceitos. É possível visualizar as informações de certificado dentro do arquivo selecionado.
4. Insira uma descrição do arquivo de certificado.
5. Confirme se o arquivo correto está selecionado e clique em **Salvar**. O certificado selecionado está listado na
tabela e está ativo por padrão.

## Registrando certificados do servidor de sistema de mensagens

Certificados do servidor padrão são fornecidos com a plataforma. É possível usar um dos certificados padrão ou fazer upload de um de sua organização. Se você ainda não tiver um certificado para usar, poderá criar uma solicitação para um novo certificado. Depois de receber o novo certificado, deve-se assiná-lo e, em seguida, fazer upload dele de volta para a plataforma.

Para usar um dos certificados padrão ou outro certificado que já tenha sido transferido por upload, selecione o certificado que deseja usar na lista suspensa **Certificado do servidor de sistema de mensagens padrão** na tabela em **Certificados do Servidor de Sistema de Mensagens**.

### <a name="upload"> </a> Fazendo upload de um certificado de sua organização

1. Na seção **Gerenciamento de Risco** de **Configurações Gerais**, em **Certificados do Servidor de Sistema de Mensagens**, clique em **Incluir Certificado**.
2. Navegue para selecionar um arquivo de certificado para fazer upload ou arrastar e soltar um arquivo na janela **Incluir Certificado**. 
3. Navegue para selecionar o arquivo de chave privado para fazer upload ou arrastar e soltar um arquivo na janela **Incluir Certificado**.  
4. Insira a passphrase da chave privada, se a chave privada tiver sido criptografada com uma passphrase.
5. Confirme se o arquivo correto está selecionado e clique em **Salvar**.
6. Selecione o certificado recém-transferido por upload da lista suspensa **Certificado do servidor de sistema de mensagens padrão**. O certificado selecionado é listado na tabela como o certificado ativo.


### Solicitando um novo certificado

 Se desejar usar um novo certificado de servidor de sistema de mensagens, você poderá gerar uma solicitação de assinatura de certificado (CSR) para solicitar um novo certificado.

 1. Na seção **Gerenciamento de Risco** de **Configurações Gerais**, em **Certificados de Servidor de Sistema de Mensagens**, clique em **Gerar CSR**.
 2. Insira os detalhes para fazer uma solicitação de assinatura de certificado (CSR) para seu servidor e clique em **Gerar**. A CSR é exibida na tabela.
 3. Faça download da solicitação e envie-a para uma autoridade de certificação para assinatura.
 4. Depois de obter um certificado, você pode fazer upload dele seguindo as etapas em Fazendo upload de um certificado de sua organização. Depois que o certificado for transferido por upload, a CSR na tabela será substituída pelo certificado transferido por upload.
