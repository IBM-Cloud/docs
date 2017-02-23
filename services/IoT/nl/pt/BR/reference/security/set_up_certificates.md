---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configurando Certificados
{: #set_up_certificates}

Os certificados são usados para autenticação de dispositivo ou para substituir o certificado de servidor padrão do {{site.data.keyword.iot_full}} para o sistema de mensagens MQTT. Todos os dispositivos que não têm certificados assinados válidos têm acesso negado e não podem se comunicar com o servidor.

Para configurar certificados e acesso ao servidor para dispositivos, o operador do sistema registra os certificados de autoridade de certificação (CA) associados e, como opção, registra os certificados do servidor de mensagens na plataforma {{site.data.keyword.iot_short_notm}}.

## Requisitos do certificado
{: #cert_reqs}

### Certificados de autoridade de certificação
Os certificados de autoridade de certificação permitem que a organização reconheça os certificados de cliente em dispositivos como confiáveis para que os dispositivos possam se conectar ao servidor. Um certificado de autoridade de certificação pode usar uma lista de revogação de certificado (CRL). A CRL deve estar acessível no momento em que a CA é incluída na plataforma ou o certificado de autoridade de certificação será rejeitado.

Se você incluir um certificado de autoridade de certificação ou substituir o certificado do servidor de sistema de mensagens, todos os dispositivos deverão se conectar usando um cliente MQTT que suporte a Server Name Indication (SNI) para que o servidor possa usar as CAs apropriadas para autenticar o dispositivo.

Se você incluir um certificado de autoridade de certificação, mas não tiver o complemento Gerenciamento de Risco e Segurança ativado, todos os dispositivos se conectarão ao TLS com a política de conexão Autenticação por Token e Certificado de Cliente. Se o complemento Gerenciamento de Risco e Segurança estiver ativado, será possível configurar diferentes políticas de conexão. Para obter informações sobre como configurar políticas de segurança de conexão, veja [Configurando políticas de segurança](set_up_policies.html).

### Certificados de cliente ou de dispositivo
Os certificados individuais de cliente ou de dispositivo permanecem nos dispositivos e não são transferidos por upload para a plataforma. O certificado de assinatura de CA usado para assinar todos os certificados de dispositivo é o único certificado transferido por upload para a plataforma. Caso você esteja usando certificados de servidor autoassinados, deverá ser feito upload da Raiz e da CA intermediária (ca.pem) usada para assinar o certificado de cliente (cert.pem).

O certificado de dispositivo individual que você assina com o certificado de autoridade de certificação deve ter o ID do dispositivo inserido como Nome Comum (CN) ou SubjectAltName no certificado. Para o campo *CN*, o formato é 'CN=d:devtype:devid'. Para o campo SubjectAltName, o formato é 'SubjectAltName=email:d:devtype:devid', em que 'devtype' é o Tipo de dispositivo do dispositivo e 'devid' é o identificador de cliente do dispositivo.

## Registrando certificados de Autoridade de Certificação (CA) para autenticação de dispositivo
{: #reg_ca_cert}

1. Efetue login no {{site.data.keyword.iot_short_notm}} e navegue para **Configurações gerais**.
2. Na seção **Segurança**, em **Certificados de autoridade de certificação**, clique em **Incluir certificado**.
3. Navegue para selecionar um arquivo de certificado para fazer upload ou arrastar e soltar um arquivo na janela **Incluir Certificado**. O arquivo pode ter apenas um certificado dentro dele e as datas do certificado devem ser válidas. Somente certificados no formato .pem ou .der são aceitos. É possível visualizar as informações de certificado dentro do arquivo selecionado.
4. Insira uma descrição para o arquivo de certificado.
5. Confirme se o arquivo correto está selecionado e clique em **Salvar**. O certificado selecionado está listado na tabela e está ativo por padrão.

## Registrando certificados do servidor de sistema de mensagens
{: #reg_msg_cert}

Um certificado de servidor padrão é fornecido com a plataforma. É possível usar o certificado padrão ou fazer upload de um de sua organização. Se você ainda não tiver um certificado para usar, poderá criar uma solicitação para um novo certificado. Depois de receber o novo certificado, deve-se assiná-lo e, em seguida, fazer upload dele de volta para a plataforma.

Para usar o certificado padrão ou outro certificado que já tenha sido transferido por upload, selecione o certificado que deseja usar na lista suspensa **Certificado do servidor de sistema de mensagens padrão** na tabela em **Certificados do servidor de sistema de mensagens**.

**Nota:** as páginas do painel da plataforma podem fazer conexões internas com o servidor de sistema de mensagens para recuperar informações do dispositivo. Ao configurar certificados de servidor autoassinados para uma organização, os usuários do painel devem incluir o certificado do servidor como um certificado confiável em seus navegadores para evitar problemas de conexão porque os navegadores, por padrão, não reconhecerão o servidor de sistema de mensagens como um servidor confiável.

### Fazendo upload de um certificado de sua organização
{: #upload_cert}
1. Na seção **Segurança** de **Configurações gerais**, em **Certificados do servidor de sistema de mensagens**, clique em **Incluir certificado**.
2. Navegue para selecionar um arquivo de certificado para fazer upload ou arrastar e soltar um arquivo na janela **Incluir Certificado**.
3. Navegue para selecionar o arquivo de chave privado para fazer upload ou arrastar e soltar um arquivo na janela **Incluir Certificado**.  
4. Insira a passphrase da chave privada, se a chave privada tiver sido criptografada com uma passphrase.
5. Confirme se o arquivo correto está selecionado e clique em **Salvar**.
6. Selecione o certificado recém-transferido por upload da lista suspensa **Certificado do servidor de sistema de mensagens padrão**. O certificado selecionado é listado na tabela como o certificado ativo.

### Solicitando um novo certificado
{: #request_cert}

Se você desejar usar um novo certificado de servidor de sistema de mensagens, será possível gerar uma Certificate Signing Request (CSR) para solicitar um novo certificado.

 1. Na seção **Segurança** de **Configurações gerais**, em **Certificados do servidor de sistema de mensagens**, clique em **Gerar CSR**.
 2. Insira os detalhes para solicitar uma CSR para seu servidor e clique em **Gerar**. A CSR é exibida na tabela.
 3. Faça download da solicitação e envie-a para uma autoridade de certificação para assinatura.
 4. Depois de obter um certificado, é possível fazer upload dele seguindo as etapas em [Fazendo upload de um certificado de sua organização](#upload_cert). Depois que o certificado for transferido por upload, a CSR na tabela será substituída pelo certificado transferido por upload.
