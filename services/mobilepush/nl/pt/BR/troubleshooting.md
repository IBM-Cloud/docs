---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Resolução de problemas
{: #errors}
Última atualização: 11 de janeiro de 2017
{: .last-updated}

Use esta seção como um guia para solucionar problemas comuns do {{site.data.keyword.mobilepushshort}}.


### Ocorreu um erro do servidor interno. Contate o administrador. (Código de erro interno: PUSHD102E)

**Explicação**: este erro poderá ocorrer se
você tiver criado uma instância push antes de novembro de 2015.  

**Resposta do usuário**: para resolver esse problema, exclua a instância de push e
crie uma nova. Observe que, ao excluir a instância de push, suas tags não serão preservadas.


### UnauthorizedRegistration

**Explicação**: o Chrome Web Push não
funciona com as Chaves do Firebase Cloud Messaging (FCM). Caso você não possa receber notificações push da web no Chrome após mudar para o FCM do GCM, é porque o website foi configurado anteriormente para
funcionar com o projeto GCM e o novo projeto foi criado no FCM. Os tokens gerados que identificam o navegador são armazenadas em cache pelo navegador Chrome.

**Resposta do usuário**: é possível resolver este problema ao remover os cookies e
reconfigurar as permissões do navegador. Isso
solicitaria permissões para ativar Notificações push. 


### Os trabalhadores de serviço não são suportados neste navegador

**Explicação**: o SDK que foi incluído como uma parte de `BMSPushSDK.js` usando o trabalhador de serviço não está disponível. 

**Resposta do usuário**: é recomendável alternar para um navegador que suporte o trabalhador de serviço. As versões suportadas dos navegadores são o Firefox versão 49 ou mais recente e o Chrome versão 53 (64 bits) ou mais recente.


### SecurityError: a operação é insegura

**Explicação**: você poder ver o erro ao ativar o console da web no Firefox. O suporte de push da web no serviço de Notificação push requer que o website seja acessado com o protocolo `https`, em vez de `http`.

**Resposta do usuário**: recomenda-se tentar a conexão ao website usando `https` no navegador.

