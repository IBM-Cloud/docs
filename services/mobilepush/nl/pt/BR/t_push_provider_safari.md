---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando credenciais para o navegador Safari
{: #configure-credential-for-safari}
Última atualização: 06 de dezembro de 2016
{: .last-updated}

Agora o serviço IBM {{site.data.keyword.mobilepushshort}} estende os recursos para enviar notificações para o navegador Safari. Observe que a versão suportada é Safari 10.0.

## Gerando um certificado
  {: #certificate-generation}

Assegure-se de ter uma conta do Apple Developer. É necessário
registrar um ID de push do website e gerar um certificado para
configurar o seu navegador Safari para receber notificações. As
etapas a seguir ajudarão na introdução.

1. No centro de Membro de desenvolvedor Apple, clique em
**Certificados, ID e perfis**. 
2. Clique em **Identificadores** e, sem
seguida, **IDs de push do website**.
3. Escolha criar uma nova entrada, selecionando o ícone de
mais.
  ![painel Push](images/safari_1.jpg)

4. No painel Registrar ID de push do website, forneça uma
descrição do ID de push do website e um ID do identificador
apropriados. É recomendado que esteja no formato de nome de domínio
reverso, começando com "web". Por exemplo:
web.com.example.dailyweatherreports.
5. Registre o ID de push do website. Agora, você tem seu ID de push do website. 
6. Selecione **Editar** para criar um certificado a ser usado pelo ID de push do
website.
7. Na janela Assistente de certificado, forneça seu ID do
e-mail e um nome comum. Deixe o endereço de e-mail da Autoridade
de certificação em branco.
8. Clique em **Salvar em disco** e
selecione **Continuar**.
9. Escolha para salvar o certificado em uma pasta
apropriada.
10. Escolha `.certSigningRequest` criado no disco, quando solicitado, no assistente
para gerar o certificado. Certifique-se de fazer download do certificado de push do website criado no
formato `.cer`.
11. Abra o certificado na ferramenta KeyChain Access. Clique com o botão direito e exporte
como um certificado p12. Observe a senha fornecida durante a geração do certificado p12.


## Configurando para notificações
  {: #configuration-notification}
 
Após gerar o certificado, é possível configurar o serviço para enviar notificações para o Safari. 

Conclua estas etapas:

1. No painel de serviço Notificações push, **clique em Configurar**. 
2. Selecione a guia Web. 
3. Na seção Push do Safari, atualize o formulário com as informações necessárias. 
	- **Nome do website**: este é o nome que você forneceu no centro de notificação.
	- **ID de push do website**: atualize com a sequência de domínio reversa para seu
ID de push do website. Por exemplo, web.com.example.www.
	- **URL do website**: forneça a URL do website que deve ser inscrita para
notificações push. Por exemplo, https://www.example.com.
	- **Domínios permitidos**: este é parâmetro opcional. Esta é a lista de websites
que solicitam permissão do usuário. Certifique-se de que as URLs sejam valores separados por vírgula. Observe
que o valor na URL do website será usado se isso não for fornecido. 
	- **Sequência de formatações de URL**: a URL a ser resolvida quando a notificação é clicada. Por exemplo, ["https://www.example.com"]. Assegure-se de que a URL use o esquema HTTPS ou HTTP.
	- **Certificado de push da web do Safari**: faça upload do
certificado .p12 e forneça a senha.
4. Clique em **Salvar**.	

![painel Push](images/push_configure_safari.jpg)	

Agora, você está configurado para enviar notificações push para o navegador Safari.

	
