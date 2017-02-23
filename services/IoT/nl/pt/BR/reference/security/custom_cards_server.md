---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protegendo seu servidor de cartões customizados
{: #securing_custom_cards}

Servidores de cartões customizados são servidores da web padrão que hospedam o código javascript de cartões customizados. Para assegurar a integridade de seu ambiente {{site.data.keyword.iot_short_notm}}, é necessário proteger seu servidor de cartões customizados tomando medidas para proteger a origem do cartão, conforme discutidos neste tópico.
{:shortdesc}

**Importante:** cartões customizados são atualmente oferecidos como um recurso experimental e a extensão de cartões customizados é ativada por sessão do navegador. A configuração de conexão de cartões customizados e os pacotes de cartões não são compartilhados globalmente em sua organização {{site.data.keyword.iot_short_notm}}.

## Requisito de função do {{site.data.keyword.Bluemix_notm}}
{: #roles_requirements}

Deve-se ter direitos de administrador do {{site.data.keyword.iot_short_notm}} para criar uma conexão do servidor de cartões customizados.

## Considerações de segurança do servidor de cartões customizados
{: #server_requirements}

Os seguintes requisitos são configurados pelo {{site.data.keyword.iot_short_notm}}:
- O diretório que serve o conteúdo do cartão customizado no servidor não deve requerer credenciais para acessar.  
Nenhuma autenticação é fornecida para o servidor de cartões customizados ao conectar para acessar e carregar cartões customizados.
- O servidor deve usar o protocolo HTTP Secure (HTTPS).
- O servidor deve suportar conexões de compartilhamento de recurso de origem cruzada (CORS).  

Para proteger o código de cartões customizados e o próprio servidor de cartões, o servidor de cartões deve ser localizado e assegurado usando defesa em profundidade. Isso inclui proteção de firewall para restringir o acesso ao servidor de cartões customizados.

O processamento de cartão customizado é sempre entre o navegador de um usuário e servidor de cartões customizados. O backend do {{site.data.keyword.iot_short_notm}} nunca é envolvido no processamento ou ajuste das informações e do código de cartões customizados.

Não há restrições colocadas no código JavaScript para escolher implementar em seus cartões no servidor de cartões customizados. O código Javascript em cartões customizados tem acesso a todas as informações mantidas no navegador, assim como quaisquer outros cartões em execução no painel.  Certifique-se de que o servidor de cartões customizados correto está fornecendo o código para o navegador exibir e processar os cartões customizados.

Os cartões executam seu código na sessão do navegador do {{site.data.keyword.iot_short_notm}} exatamente como escrito. Além disso, a conexão do servidor de cartões customizados é criada sem credenciais fornecidas ao servidor de cartões customizados. O navegador de um usuário pode conectar-se a qualquer servidor de cartões customizados configurado.

É importante configurar somente servidores de cartões customizados conhecidos e assegurados para fornecer cartões customizados aos painéis de seus usuários.   
