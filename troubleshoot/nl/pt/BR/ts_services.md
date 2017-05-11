---

copyright:
  years: 2015, 2016
  
lastupdated: "2016-08-12"

---



{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# Resolução de problemas para serviços
{: #services}


Os problemas de serviços do {{site.data.keyword.Bluemix}} podem incluir um erro de tempo limite de gateway que ocorre quando você exclui uma instância de serviço. É possível recuperar desses problemas seguindo algumas etapas fáceis.
{:shortdesc}

## Ocorre um erro de broker de serviço ao excluir uma instância de serviço
{: #ts_service_broker}

Você poderá receber uma mensagem de erro quando tentar excluir
uma instância de serviço que já foi excluída do controlador de nuvem.
{:shortdesc}

Ao tentar excluir uma instância de serviço, você vê a mensagem de erro do broker de serviço a seguir:
{: tsSymptoms}
`Tempo limite do gateway`

Esse problema ocorrerá se
    a instância de serviço já tiver sido excluída do
controlador de nuvem.
{: tsCauses}

Crie uma instância de serviço com o mesmo nome de serviço, em seguida, ligue-a a seus aplicativos. Depois, é possível excluir a instância de serviço e os aplicativos que usam o serviço.   
{: tsResolve}
