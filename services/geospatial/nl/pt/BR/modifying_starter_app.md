---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Modificando o aplicativo iniciador para {{site.data.keyword.Bluemix_short}}
{: #modifying_starter_app}

É possível modificar o aplicativo iniciador e, em seguida, reimplementá-lo no {{site.data.keyword.Bluemix_short}} para ver os resultados.
{:shortdesc}


Uma modificação simples é aumentar ou remover o limite de eventos no aplicativo iniciador para que
        ele não seja mais executado.

1. Abra app.js em um editor de texto ou ambiente de desenvolvimento.
2. Mude a variável eventTarget ou exclua esta linha para remover o limite de evento inteiramente.
	 <pre><code>var eventTarget = 100;</code></pre>
3. Se você desejar remover o limite de evento, também precisará excluir a instrução IF a seguir:
	 <pre><code>  
	if (eventCount >= eventTarget) {
		    status_step[3] = "Completed";
		    console.log("\nTarget event count has been reached.  Geospatial Analytics service will be stopped.\n");
		    callback(null, null);
		    } 
	</code></pre> 
4. Reimplemente seu aplicativo modificado para {{site.data.keyword.Bluemix_short}} com o comando cf push.
	 <pre><code>  
	cf push myapp
	</code></pre>
5. Insira a URL do aplicativo ou "roteie-a" em seu navegador ou ative-a a partir do painel do
              {{site.data.keyword.Bluemix_short}}.
