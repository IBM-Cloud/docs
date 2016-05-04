---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Customizando o JRE
{: #customizing_jre}

*Última atualização: 23 de março de 2016*

Os aplicativos são executados em um Java Runtime
Environment (JRE) fornecido e configurado pelo buildpack Liberty. O buildpack Liberty também
possibilita configurar a versão ou tipo de JRE,
customizar as opções da JVM ou sobrepor as funções do JRE.

## IBM JRE

Por padrão, os aplicativos são configurados
para executar com uma versão leve do IBM JRE. Esse
JRE leve é dividido para fornecer função principal essencial com um disco
e área de cobertura da memória muito reduzidos. Para obter informações adicionais sobre o conteúdo do JRE leve, veja [Liberty for Java Runtime](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/docs/bluemix/libertyforjava_jre.doc.html).

O
IBM JRE versão 8 é usado, por padrão. Use a variável de ambiente JBP_CONFIG_IBMJDK para especificar uma versão alternativa do IBM JRE. Por exemplo, para usar o mais recente
IBM JRE 7.1, configure a variável de ambiente a seguir:
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: #codeblock}

A
propriedade da versão pode ser configurada para um intervalo de versão. Existem dois intervalos
de versão suportados: 1.7.+ e 1.8.+. Para obter os melhores resultados, use Java 8.

## OpenJDK
{: #openjdk}

Opcionalmente, os aplicativos podem ser
configurados para execução com o OpenJDK como o JRE. Para ativar um aplicativo para execução com o OpenJDK, configure a variável de ambiente da JVM (Java virtual machine) como "openjdk". Por
exemplo, usando a ferramenta de linha de comandos cf, execute o comando:
```
    $ cf set-env myapp JVM 'openjdk'
```
{: #codeblock}

Se ativado, o OpenJDK versão 8 é usado, por padrão. Use a variável de ambiente JBP_CONFIG_OPENJDK para especificar uma versão alternativa do OpenJDK. Por exemplo, para usar o mais recente OpenJDK 7,
configure a variável de ambiente a seguir:
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: #codeblock}

A propriedade da versão pode ser configurada para um intervalo de versão como 1.7.+ ou qualquer versão específica listada na [lista de versões do OpenJDK disponíveis](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml). Para obter os melhores resultados, use Java 8.

## Configurando as opções do JRE
{: #configuring_jre}

### Configuração padrão da JVM
{: #jvm_default_config}

O buildpack Liberty configura as opções da JVM
padrão considerando:

* Um limite de memória de um aplicativo.  As configurações de heap da JVM aplicadas
são calculadas com base em:
  * o limite de memória de um aplicativo, conforme explicado em [Limites de memória e o buildpack do Liberty](memoryLimits.html#memory_limits)
  * o tipo de JRE, uma vez que as opções relacionadas ao heap para a JVM variam de acordo
com as opções suportadas do JRE.

* Os [Recursos do Liberty suportados no Bluemix](libertyFeatures.html#libertyfeatures).
  * As transações do banco de dados global two-phase commit não são suportadas no Bluemix e, portanto, são desativadas configurando -Dcom.ibm.tx.jta.disable2PC=true.

* O ambiente do Bluemix.

    As opções da JVM são configuradas para fornecer otimização em um ambiente do Bluemix e para ajudar os diagnósticos de condições de erro relacionado à memória.
  * a recuperação rápida de falha de um aplicativo é configurada desativando
as opções de dumps da JVM e eliminando os processos quando a memória de um
aplicativo está esgotada.
  * ajuste de virtualização (somente IBM JRE).
  * roteamento de informações nos recursos de memória disponível do aplicativo
no momento da falha para o Loggregator.
  * se um aplicativo estiver configurado para ativar os dumps de memória da JVM, o encerramento de processos Java será desativado e os dumps de memória da JVM serão roteados para um diretório "dumps" de aplicativo comum. Esses dumps podem ser visualizados a partir do painel do Bluemix ou da CLI do CF.

A seguir está uma configuração da JVM padrão de exemplo que é gerada pelo buildpack para um aplicativo que é implementado com um limite de memória de 512 M:
```
    -Xtune:virtualized
    -Xmx384M
    -Xdump:none
    -Xdump:heap:defaults:file=../../../../../dumps/heapdump.%Y%m%d.%H%M%S.%pid.%seq.phd
    -Xdump:java:defaults:file=../../../../../dumps/javacore.%Y%m%d.%H%M%S.%pid.%seq.txt
    -Xdump:snap:defaults:file=../../../../../dumps/Snap.%Y%m%d.%H%M%S.%pid.%seq.trc
    -Xdump:tool:events=systhrow,filter=java/lang/OutOfMemoryError,request=serial+exclusive,exec=../../../../.buildpack-diagnostics/killjava.sh
    -Dcom.ibm.tx.jta.disable2PC=true
```
{: #codeblock}

### Customizando a configuração da JVM
{: #customizing_jvm}

Os aplicativos podem customizar as opções
da JVM com as especificações que são definidas pelo JRE configurado
para o aplicativo. Referencie as diretrizes sobre como especificar uma
opção e seu uso diretamente da documentação do JRE, uma vez
que as opções variam de acordo com o JRE.

<table>
<tr>
<th align="left">JRE</th>
<th align="left">Formato de opções da linha de comandos</th>
<th align="left">Referência</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>inclui opções de tempo de execução (prefixadas por -X), quaisquer propriedades de sistema do Java (prefixadas com -D) e não recomenda -XX para o uso casual (essas opções estão sujeitas à mudança)
</td>
<td>[Opções da linha de comandos da Versão 8](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html), [Opções da linha de comandos da Versão 7](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)
</td>
</tr>

<tr>
<td> OpenJDK </td>
<td>é baseado no tempo de execução do HotSpot que possui a notação de
-X para não padrão, -XX para opções do desenvolvedor e sinalizações Booleanas
para ativar ou desativar a opção </td>
<td>[Visão tempo de execução de execução do HotSpot](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html) </td>
</tr>
</table>

Um aplicativo que requer opções customizadas da JVM pode configurar a opção como um valor para uma das variáveis de ambiente IBM_JAVA_OPTIONS, JAVA_OPTS ou JVM_ARGS no Bluemix. Consulte a seção Variáveis de ambiente sobre como configurar a variável de ambiente de um aplicativo. Um servidor em pacote ou um diretório do servidor também pode incluir um arquivo jvm.options que contém as opções da linha de comandos em vez de configurar uma variável de ambiente.

Quando as opções da JVM são aplicadas ao JRE, as opções padrão
do buildpack Liberty são aplicadas primeiro, seguidas pelas opções
customizadas. As opções customizadas são anexadas em uma ordem específica,
que é listada na tabela. A sequência das opções Java aplicadas define quais opções têm precedência. As opções que são aplicadas por último têm precedência sobre as opções
que foram aplicadas anteriormente.

Nota: algumas opções podem não entrar em vigor a menos que a opção seja acionada por um agente.

<table>
<tr>
<th align="left">Ordem aplicada</th>
<th align="left">Configuração de opções da JVM do aplicativo</th>
<th align="left">Descrição</th>
<th align="left">Tipo de aplicativo suportado</th>
<th align="left">Para atualizar a opção JVM de um aplicativo implementado</th>
<th align="left">Aplicável ao JRE do OpenJDK</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>uma variável de ambiente que é suportada pelo IBM JRE</td>
<td>Todos</td>
<td>Reiniciar ou estagiar novamente o aplicativo</td>
<td>Não</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>uma variável de ambiente por meio da estrutura de Opções Java do buildpack do Liberty</td>
<td>Todos</td>
<td>Remontar o app</td>
<td>Sim</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>um arquivo de configuração da JVM que é suportado pelo servidor em pacote ou
diretório do servidor do tempo de execução do Liberty</td>
<td>Pacote do servidor</td>
<td>Remontar o app</td>
<td>Sim</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>uma variável de ambiente que é suportada pelo tempo de execução do
Liberty</td>
<td>Todos</td>
<td>Reiniciar ou remontar o app</td>
<td>Sim</td>
</tr>
</table>

### Determinando as opções da JVM aplicadas de um aplicativo em execução
{: #determining_applied_jvm_options}

Exceto para opções definidas pelo aplicativo que são especificadas com a variável de ambiente JVM_ARGS, as opções resultantes são persistidas no ambiente de tempo de execução como opções da linha de comandos (aplicativos Java independentes) ou em um arquivo	jvm.options (aplicativos Java não independentes). As opções da JVM aplicadas para o aplicativo podem ser visualizadas a partir do Painel do Bluemix ou da	CLI do CF.

As opções da JVM para aplicativo Java independente
são persistidas como opções da linha de comandos. Elas podem ser visualizadas a partir do arquivo staging_info.yml.
```
    $ cf files myapp staging_info.yml
```
{: #codeblock}

As opções da JVM para WAR, EAR, diretório do servidor e implementação do servidor em pacote são persistidas em um arquivo jvm.options.

Para visualizar o arquivo jvm.options para WAR, EAR e diretório do servidor, execute o comando:
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: #codeblock}

Para visualizar o arquivo jvm.options para um servidor em pacote, substitua <serverName> pelo nome do servidor e execute o comando:
```
    $ cf files myapp app/wlp/usr/servers/<serverName>jvm.options
```
{: #codeblock]

#### Exemplo de uso
{: #example_usage}

Implementando um aplicativo com opções customizadas da JVM para ativar a criação de log de coleta de lixo detalhada da JVM do IBM JRE:
* As opções da JVM inclusas no arquivo	manifest.yml de um aplicativo:
```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: #codeblock}

* Para visualizar a criação de log de coleta de lixo detalhada da JVM gerada:
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: #codeblock}    

* Atualizando a opção JVM do IBM JRE de um aplicativo implementado para acionar um heap, snap e javacore em uma condição OutOfMemory:

Configure a variável de ambiente do aplicativo com a opção JVM
e reinicie o aplicativo:
```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: #codeblock}

* Para visualizar os dumps da JVM gerados quando a condição sem memória
é acionada:
```
    $ cf files myapp dumps

    Obtendo arquivos para o app myapp na organização myemail@email.com / space dev como myemail@email.com...
    OK

    Snap.20141106.100252.81.0003.trc           307.3K
    heapdump.20141106.100252.81.0001.phd       3.9M
    javacore.20141106.100252.81.0002.txt     870.5K
```
{: #codeblock}

### Sobrepondo o JRE
{: #overlaying_jre}

Existem alguns casos
em que os arquivos precisam ser empacotados com o JRE para expor suas funções. O desenvolvedor
de aplicativos pode fornecer arquivos JRE para customização.

Os
arquivos a serem sobrepostos podem ser colocados em pacote com o WAR, EAR ou JAR
do aplicativo em uma pasta de recursos na raiz do archive. Para um servidor (arquivo compactado ou diretório do servidor), os arquivos podem ser colocados em pacote em uma pasta de recursos no diretório do servidor, com o arquivo server.xml.

* Arquivo WAR
  * WEB-INF
  * recursos
    * outros arquivos
    * .java-overlay


* Arquivo EAR
  * META-INF
  * recursos
    * outros arquivos
    * .java-overlay


* Arquivo JAR
  * META-INF
  * recursos
    * outros arquivos
    * .java-overlay


* server_name DIR
  * apps
  * dropins
  * server.xml
  * recursos
    * outros arquivos
    * .java-overlay

O diretório .java-overlay contém arquivos específicos na mesma hierarquia de arquivo que o Java JRE que está sendo sobreposto iniciando com .java/jre.

Por exemplo, se você desejar usar a criptografia AES de 256 bits, será necessário sobrepor estes arquivos de políticas Java:
```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Faça o download dos arquivos de políticas sem restrições apropriados e inclua-os em seu aplicativo como:
```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Ao enviar seu aplicativo por push, esses jars sobrepõem os jars de política padrão no tempo de execução do Java. Esse processo ativa a criptografia AES de 256 bits.

# rellinks
## geral
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
