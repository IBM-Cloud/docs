---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

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

#{{site.data.keyword.geospatialshort_Geospatial}} resolução de problemas 
{: #ts_geospatial}


Obtenha as respostas para várias questões comuns sobre o uso do {{site.data.keyword.geospatialshort_Geospatial}} no {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Quando paro o meu app, o serviço continua monitorando regiões
{: #stop-monitoring}


Parar o app não para automaticamente o {{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}


Você parou o aplicativo que usa o {{site.data.keyword.geospatialshort_Geospatial}}, mas vê no painel de administração de serviço que o serviço ainda está monitorando as regiões especificadas em seu app.
{: tsSymptoms}


Se você parar seu aplicativo, a instância de serviço do {{site.data.keyword.geospatialshort_Geospatial}} continuará a ser executada. O serviço continua a monitorar regiões até que você pare o serviço, independentemente se o app está ou não em execução. 
{: tsCauses}


Pare o {{site.data.keyword.geospatialshort_Geospatial}} no painel de
administração de serviços. Ou você pode modificar seu app para parar o serviço usando a API REST e, em seguida, enviar por
push suas alterações novamente para o {{site.data.keyword.Bluemix_short}}.
{: tsResolve}

##O serviço está monitorando regiões que não especifiquei em meu app
{: #unspecified-region}



Se você tiver mais de um aplicativo ligado à mesma instância de serviço, outro
aplicativo poderá ter incluído essas regiões.
{:shortdesc}



Quando você visualiza a instância do {{site.data.keyword.geospatialshort_Geospatial}} no painel de administração de serviços, vê que ela está monitorando mais regiões do
que as especificadas em um de seus apps.
{: tsSymptoms}

Uma única instância do {{site.data.keyword.geospatialshort_Geospatial}} monitora as regiões de todos os apps que estão ligados a ela. Isso significa que quando você visualiza o painel de
administração de serviços, verá informações das regiões especificadas por todos os seus apps.
{: tsCauses}

Para parar o {{site.data.keyword.geospatialshort_Geospatial}}
de monitorar determinadas regiões:

1. Parar o serviço.
2. Modifique seu app ou apps para remover essas regiões.
3. Envie por push seu app ou apps novamente para o {{site.data.keyword.Bluemix_short}}.
{: tsResolve}


##Resolução de problemas do painel de administração de serviços
{: #dashboard}

À medida que você resolve problemas do seu aplicativo, você desejará acessar o painel
de administração de serviços para verificar o status
de sua instância de serviço. Se ele não estiver processando dados, talvez você possa
corrigir o problema parando e reiniciando o serviço.
{:shortdesc}

O status de sua instância de serviço do {{site.data.keyword.geospatialshort_Geospatial}} é separado do status de seu aplicativo e vários aplicativos podem estar ligados à mesma instância de serviço. 

O painel de
administração de serviços fornece informações sobre o status do {{site.data.keyword.geospatialshort_Geospatial}}, e não sobre os aplicativos que estão ligados
a ele. Os status separados de sua instância de serviço e seu aplicativo ou aplicativos significam que se você parar seu
aplicativo, sua instância de serviço do {{site.data.keyword.geospatialshort_Geospatial}} continuará a ser executada. O
serviço continua a monitorar as regiões escolhidas até que você as remova, independentemente de o seu aplicativo estar ou não
em execução.
