---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#Criando um botão Implementar no {{site.data.keyword.Bluemix_notm}} {: #deploy-button} 

*Última atualização: 2 de março de 2016* 

O botão Implementar no {{site.data.keyword.Bluemix}} é uma maneira eficiente de compartilhar seu app público de origem Git para que outras pessoas possam experimentar com o código e implementá-lo no IBM {{site.data.keyword.Bluemix_notm}}. O botão requer configuração mínima e é possível inseri-lo em qualquer lugar que suporte marcação. Qualquer essoa que clicar no botão cria uma cópia clonada do código em um novo repositório Git de modo que seu app original permaneça não afetado. 
{: shortdesc} 

**Dica:** se a marca da empresa for importante, será possível [integrar um fluxo Implementar no iFrame do {{site.data.keyword.Bluemix_notm}}](../develop/deploy_button_embed.html) a seu conteúdo, em vez de inserir um botão. Quando as pessoas criam uma cópia clonada de seu app público de origem Git, elas permanecem em seu conteúdo em vez de serem redirecionadas ao website bluemix.net. 

Quando alguém clica em seu botão, ocorrem estas ações: 

1. Se a pessoa não tiver uma conta {{site.data.keyword.Bluemix}} ativa, uma conta para teste deve ser criada. 

2. A pessoa pode selecionar uma região, uma organização, um espaço e um nome de app. O nome do app sugerido é construído a partir do nome anterior do app, do nome do usuário da pessoa e do horário. 

3. A ramificação principal do repositório Git público original é clonada em um projeto {{site.data.keyword.jazzhub_title}} novo e privado com um novo repositório Git. 

4. Se o app requer um arquivo de construção, o arquivo de construção é detectado automaticamente e o app é construído. 

5. Se um pipeline for configurado para o processo de construção e implementação, um arquivo `pipeline.yml` será usado para implementar o app.

6. Se o app requer um contêiner, um `pipeline.yml` que define o serviço **IBM Containers** e um Dockerfile que define uma imagem serão usados para implementar o app em um contêiner do {{site.data.keyword.Bluemix_notm}}. 

7. O app é implementado na organização do {{site.data.keyword.Bluemix_notm}} da pessoa. 

##Exemplos do botão {: #button-examples} 

Veja um exemplo do botão de app para um repositório {{site.data.keyword.jazzhub_short}} público:

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/deploy_buttonx2.png" alt="Implementar no Bluemix" /></a>
</p> 

Veja um exemplo do botão de app para um repositório GitHub público: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/deploy_buttonx2.png" alt="Implementar no Bluemix" /></a>
</p> 

Veja um exemplo de botão para um app que é implementado em um contêiner do {{site.data.keyword.Bluemix_notm}}: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/deploy_buttonx2.png" alt="Implementar no Bluemix" /></a>
</p> 

##Criando um botão {: #create-button}

Para criar um botão Implementar no {{site.data.keyword.Bluemix_notm}}: 

<ol>
<li> Copie e modifique um dos modelos de fragmento a seguir e inclua um repositório Git público.
<p></p>
<p>
<strong>Dica</strong>: se você deseja especificar a entrada de construção para um projeto de Serviços DevOps, inclua um parâmetro de ramificação na URL do Git. Ao incluir um parâmetro de ramificação, o repositório Git público original, incluindo todas as suas ramificações, é clonado em um novo projeto privado de Serviços DevOps com um novo repositório Git. A ramificação Git especificada é configurada como a entrada para a tarefa de construção. Se você não especificar uma ramificação, a entrada para a tarefa de compilação será configurada como a ramificação principal por padrão.
</p>
<ul>
<li>HTML:
<p>
Ramificação principal padrão:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
Ramificação Git especificada:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>Redução de preço:
<p>
Ramificação principal padrão:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&#41;
</pre>
<p>Ramificação Git especificada:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&#41;
</pre>
</li>
</ul>
</li>
<li>Insira o fragmento nos blogs, artigos, wikis, arquivos leia-me ou em qualquer lugar em que deseja promover seu app. 
</li>
</ol>

##Considerações de fragmento para o botão {: #button-snippet}

Revise estas considerações quando estiver customizando o fragmento para o botão Implementar no Bluemix. 

* Ambos os modelos usam um caminho padrão para uma imagem de botão externo em formato PNG e em inglês. 

    * Se você preferir usar uma imagem SVG para o botão em vez de um PNG, existe uma versão SVG disponível. É possível alterar o caminho para a imagem de botão externa que é usada no fragmento para `https://bluemix.net/deploy/button.svg`.
	
	* Se preferir usar uma imagem maior para o botão, há uma imagem PNG disponível que tem o dobro do tamanho da original. É possível alterar o caminho da imagem de botão externa que é usada no fragmento para `https://bluemix.net/deploy/button_x2.png`. 
	
	* Se você preferir armazenar a imagem localmente, será possível fazer download da imagem e armazená-la no repositório Git. Ajuste o caminho para usar o local relativo da imagem. 
	
	* Se você deseja usar uma versão traduzida do botão, é possível referenciá-la remotamente ou fazer download dela a partir do [ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button). 
	
##Considerações de repositório para o botão {: #button-repo} 

Revise estas considerações para o repositório do projeto que você usará no botão Implementar no Bluemix. 

<ul>
<li>Um <code>manifest.yml</code> não precisa estar em seu repositório. No entanto, se seu app precisar que outros serviços sejam executados, deve fornecer um arquivo manifest que declare esses serviços.  

Com o arquivo manifest, é possível especificar: 
    <ul>
    <li>Um nome de app exclusivo.</li>  
    <li>Serviços declarados: Uma extensão manifest, que cria ou procura por serviços obrigatórios ou opcionais que devem ser configurados antes que o app seja implementado, como um serviço de cache de dados. É possível localizar uma lista de serviços, rótulos e planos elegíveis do {{site.data.keyword.Bluemix_notm}}, usando a <a href="https://github.com/cloudfoundry/cli/releases">Interface da linha de comandos CF</a> para executar o comando <code>cf marketplace</code> ou procurando no <a href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-*-dWdevcenter-*-devops-services-_-lp#/store">catálogo do {{site.data.keyword.Bluemix_notm}}</a>. 
    
    <strong>Nota:</strong> serviços declarados são uma extensão IBM do formato de manifest padrão do Cloud Foundry. Essa extensão pode ser revisada em uma liberação futura conforme o recurso evolui e melhora.
	
	<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank">Aprenda a criar um arquivo <code>manifest.yml</code>.</a>  
<pre class="codeblock">
	---
    #Modelo de manifest.yml

  declared-services:
    &lt;`arbitrary_service_instance_name`&gt;:  # [required]
      label: &lt;`actual_service_name`&gt; # [required] The actual service name from market place
      plan: Shared # [optional] If provided, used to fetch the declared service. Otherwise, defaults to 'Free' or 'free'.
  applications:
  - serviços
    - &lt;`arbitrary_service_instance_name`&gt;
    name: &lt;`appname`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #Exemplo de manifest.yml

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB: 
        label: cloudantNoSQLDB 
        plan: Shared 
  applications:
  - serviços
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> Se o repositório precisar ser construído antes da implementação do app, uma construção automatizada do código no repositório será acionada antes da implementação. As construções automatizadas ocorrem quando um arquivo do script de construção é detectado no diretório-raiz do repositório. 
	
	Construtores suportados: 
	    <ul>
		<li> <a href="http://ant.apache.org/manual/using.html" target="_blank">Ant:</a> /<code>build.xml</code>, que constrói a saída para a pasta <code>./output/</code> </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank">Gradle:</a> <code>/build.gradle</code>, que constrói a saída para a pasta <code>.</code> </i>
		<li> <a href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank">Grunt:</a> <code>/Gruntfile.js</code>, que constrói a saída para a pasta <code>.</code> </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank">Maven:</a> <code>/pom.xml</code>, que constrói a saída para a pasta <code>./target/</code></li>
	   </ul>
	</li>	
	<li>Para configurar o pipeline para o projeto em um diretório <code>.bluemix</code>, inclua um arquivo <code>pipeline.yml</code>. É possível criar um arquivo <code>pipeline.yml</code> manualmente ou gerar um a partir de um projeto existente do DevOps Services. Para criar um arquivo pipeline.yml a partir de um projeto do {{site.data.keyword.jazzhub_short}} e incluí-lo em seu repositório, conclua estas etapas. 
<ol>
<li>Abra seu projeto DevOps Services em um navegador e clique em <b>Construir e implementar</b>.</li>
<li>Configure seu pipeline com tarefas de construção e implementação.</li>
<li>Em seu navegador, inclua <code>/yaml</code> na URL de pipeline do projeto e pressione Enter. 
<br>Exemplo: <code>https://hub.jazz.net/pipeline/<owner>/<project_name>/yaml</code></li>
<li>Salve o arquivo <code>pipeline.yml</code> resultante.</li>
<li>No diretório-raiz de seu projeto, crie um diretório <code>.bluemix</code>.</li>
<li>Faça upload do arquivo <code>pipeline.yml</code> para o repositório <code>.bluemix</code>.</li>
</ol> </li>
	<li>Se você estiver implementando um app em um contêiner usando <stong>IBM Containers</strong>, deverá incluir o Dockerfile no diretório-raiz do repositório e, em um diretório <code>.bluemix</code>, incluir um arquivo <code>pipeline.yml</code>. 
	<ul>
	    <li> Para aprender mais sobre a criação de Dockerfiles, <a href="https://docs.docker.com/reference/builder/" target="_blank">consulte a documentação do Docker</a>. </li>
	    <li>É possível criar um arquivo <code>pipeline.yml</code> manualmente ou gerar um a partir de um projeto existente do DevOps Services. Para criar um <code>pipeline.yml</code> manualmente especificamente para contêineres, <a href="https://github.com/Puquios/" target="_blank">consulte os exemplos em GitHub</a>. </li>
        </ul>

 </li>
 </ul>
</ul>

Para obter ajuda com resolução de problemas, consulte [O botão Implementar no Bluemix não implementa um app](../troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}.	
