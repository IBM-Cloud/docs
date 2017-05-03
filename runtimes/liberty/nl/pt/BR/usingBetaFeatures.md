---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Usando os recursos beta
{: #using_beta_features}

Os recursos beta do Liberty fornecem um acesso antecipado aos novos
modelos de programação e de funcionalidade que podem ser incluídos em uma liberação futura
do Liberty. A maioria dos recursos beta também podem ser usados em aplicativos implementados no Bluemix.

**Importante**: os recursos beta são somente para propósitos de teste e desenvolvimento e não podem ser usados em produção. Para obter os termos de
uso completos, consulte o [
contrato de licença beta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Recursos beta do Liberty disponíveis no Bluemix
<table>
<tr>
<th align="left">Recurso</th>
<th align="left">Recurso</th>
<th align="left">Recurso</th>
<th align="left">Recurso</th>
</tr>

<tr>
<td>bluemixLogCollector-1.1</td>
<td>httpWhiteboard-1.0</td>
<td>logstashCollector-1.1</td>
<td>osgiBundle-1.0</td>
</tr>
</table>

Para usar os recursos beta do Liberty no Bluemix, será necessário fazer o seguinte:

1. [Implemente um diretório do servidor ou um servidor em pacote](optionsForPushing.html) com um ou mais recursos beta ativados no arquivo server.xml como no exemplo a seguir:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>bluemixLogCollector-1.1</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Configure a variável de ambiente **IBM_LIBERTY_BETA** como **true**. Essa variável direciona o buildpack do Liberty para instalar
e ativar os recursos beta em seu aplicativo.  Por exemplo:
  * usando a ferramenta de linha de comandos cf:
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * ou usando o arquivo manifest.yml:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Configure a variável de ambiente **JBP_CONFIG_LIBERTY** como
**"version: +"**. Essa variável ativa o [tempo de execução mensal do Liberty](buildpackDefaults.html#liberty_versions) que suporta recursos beta. Por exemplo:
  * usando a ferramenta de linha de comandos cf:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * ou usando o arquivo manifest.yml:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Se você estiver ativando os recursos beta em um aplicativo existente, não se esqueça de remontar seu aplicativo após a configuração das variáveis de ambiente.

{: #codeblock}

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
