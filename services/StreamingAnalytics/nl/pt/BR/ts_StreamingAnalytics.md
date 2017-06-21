---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.streaminganalyticsshort}} resolução de problemas
{: #ts_StreamingAnalytics}

É possível localizar as respostas a perguntas comuns sobre como usar o {{site.data.keyword.streaminganalyticsshort}} no {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Ao ativar o serviço, sou solicitado por credenciais para efetuar login no console
{: #log_in_console}

Ao ativar o {{site.data.keyword.streaminganalyticsshort}}, você é solicitado por credenciais para efetuar login no console de serviço.
{:shortdesc}

Você ativa um serviço do {{site.data.keyword.streaminganalyticsshort}} que criou anteriormente e, em vez de acessar diretamente o console de serviço, verá uma página de login na qual serão solicitadas as credenciais.
{: tsSymptoms}

A infraestrutura de serviço foi atualizada e o cache do navegador está impedindo o serviço de coletar a atualização.
{: tsCauses}

Limpe o cache do navegador para certificar-se de obter a versão mais recente do console de serviço.
{: tsResolve}

##Meu aplicativo está unhealthy
{: #app_unhealthy}

Não é possível executar seu aplicativo corretamente e o status de funcionamento é `unhealthy`.
{:shortdesc}

Você envia um aplicativo para a instância de serviço, o aplicativo é iniciado, mas falha imediatamente e o status de funcionamento é `unhealthy`.O erro a seguir aparece no arquivo de log: `/lib64/libc.so.6: version GLIBC_2.14 not found`.
{: tsSymptoms}

Você não compilou o aplicativo usando um sistema operacional RHEL 6.5 ou uma versão equivalente do CentOS.
{: tsCauses}

Deve-se recompilar seu aplicativo em um sistema operacional Red Hat Enterprise Linux (RHEL) 6.5 ou em uma versão equivalente do CentOS, usando processadores Intel. Envie seu aplicativo para a instância de serviço novamente.
{: tsResolve}
