---

copyright:
 years: 2015, 2016

---

# Resolução de problemas
{: #errors}
Última atualização: 08 de novembro de 2016
{: .last-updated}

Use esta seção como um guia para solucionar problemas comuns do {{site.data.keyword.mobilepushshort}}.


### Ocorreu um erro do servidor interno. Contate o administrador. (Código de erro interno: PUSHD102E)

####Explicação

**Explicação**: este erro poderá ocorrer se
você tiver criado uma instância push antes de novembro de 2015.  

####RESPOSTA DO USUÁRIO

**Ação**:  para resolver esse problema, exclua a instância de push e crie uma nova.

**Observação**: ao excluir a instância
push, as suas tags não serão preservadas.


### UnauthorizedRegistration

####Explicação

**Explicação**: o Chrome Web Push não
funciona com as Chaves do Firebase Cloud Messaging (FCM). Caso você não possa receber notificações push da web no Chrome após mudar para o FCM do GCM, é porque o website foi configurado anteriormente para
funcionar com o projeto GCM e o novo projeto foi criado no FCM. Os tokens gerados que identificam o navegador são armazenadas em cache pelo navegador Chrome.

**Ação**: é possível resolver este problema
ao remover os cookies e reconfigurar as permissões do navegador. Isso
solicitaria permissões para ativar Notificações push. 

