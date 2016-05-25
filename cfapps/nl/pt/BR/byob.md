---

 

copyright:

  years: 2015，2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando buildpacks da comunidade
*Última atualização: 15 de março de 2016*

Se não for possível localizar um iniciador no Catálogo do {{site.data.keyword.Bluemix}} que forneça o tempo de execução desejado, será possível trazer um buildpack externo para o {{site.data.keyword.Bluemix_notm}}. É possível especificar um buildpack customizado e compatível com Cloud Foundry ao implementar o app usando o comando cf push.
{:shortdesc}

São fornecidos buildpacks externos pela comunidade do Cloud Foundry para
utilização como seus próprios buildpacks. Antes de
implementar o app no {{site.data.keyword.Bluemix_notm}},
certifique-se de instalar a interface de linha de comandos cf.

**Nota:** buildpacks externos não são fornecidos pela IBM, portanto, talvez seja necessário entrar em contato com a comunidade do Cloud Foundry para obter suporte.

## Buildpacks integrados da comunidade

No {{site.data.keyword.Bluemix_notm}},
é possível usar os buildpacks integrados que são fornecidos pela comunidade do
Cloud Foundry. Para ver buildpacks integrados da comunidade, execute o comando cf buildpacks:

```
cf buildpacks
Getting buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
Para obter o mesmo tempo de execução ou estrutura, os buildpacks criados pela IBM têm precedência sobre os da comunidade. Para usar o buildpack da comunidade para sobrescrever o buildpack criado pela IBM, deve-se especificar o buildpack usando a opção -b com o comando cf push.
<p>Por exemplo, é possível usar o buildpack da comunidade para apps Java™ da web:</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>Também é possível usar o buildpack da comunidade para o app Node.js:</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>Para um tempo de execução ou uma estrutura não suportados por buildpacks criados pela IBM, mas suportados pelos buildpacks integrados da comunidade, não é necessário usar a opção -b com o comando cf push.</p><p>Por exemplo, para apps Ruby, não há buildpacks criados pela IBM. É possível
usar o buildpack integrado da comunidade inserindo o comando a seguir:</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## Buildpacks externos

É possível usar buildpacks externos ou customizados no {{site.data.keyword.Bluemix_notm}}. Deve-se especificar a URL do buildpack com a opção -b e especificar a pilha com a opção ```-s``` no comando **cf push**. Por exemplo, para usar um buildpack de comunidade externo para arquivos estáticos, execute o comando a seguir

```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

Um outro
exemplo é que se você não desejar usar o buildpack integrado da comunidade para aplicativos Ruby,
é possível usar um buildpack externo inserindo o seguinte
comando:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

Também é
possível usar um buildpack customizado para seu aplicativo. Por exemplo, para usar um buildback PHP de software livre fornecido pela comunidade Cloud Foundry, ao implementar o app PHP no Bluemix, insira o comando a seguir para especificar a URL do repositório Git do buildpack:

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## Especificando a versão do buildpack Java

<ul>
<li>
Use o comando <strong>cf set-env</strong>. Por exemplo, insira o comando a seguir para configurar a versão Java para 1.7.0:
<pre class="pre"><code>cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { version: 1.7.0_+ }}&#39;</code></pre>
<p>Em seguida,
remonte seu aplicativo para efetivar a mudança:</p>
<pre class="pre"><code>cf restage app_name</code></pre>
</li>
<li>
Use o arquivo <code>manifest.yml</code>. É possível incluir a variável de ambiente
e o valor que deseja especificar diretamente
no arquivo. Para obter informações detalhadas, consulte <a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">Variáveis de ambiente</a>.</li></ul>
  

