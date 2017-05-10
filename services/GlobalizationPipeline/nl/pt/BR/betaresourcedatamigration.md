---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Migrando dados de recurso da versão beta
{: #globalizationpipeline_betaresourcedatamigration}


A versão beta do {{site.data.keyword.GlobalizationPipeline_full}} será finalizada após um determinado período após a liberação da versão GA. Os dados do usuário nas instâncias beta não serão movidos para as instâncias de serviço GA. Para manter os dados após o GA, é possível exportar os dados de recurso para arquivos e depois importar para a nova instância. Observe que não é possível executar essa operação usando o painel de serviço. Além disso, a exportação de dados de recurso em um formato de arquivo de recursos não preservará outros metadados associados às entradas de recursos.

Para suportar migração de dados de beta para GA, foi incluído um recurso na ferramenta de linha de comandos Java do {{site.data.keyword.GlobalizationPipeline_short}}. A origem da ferramenta é hospedada em https://github.com/IBM-Bluemix/gp-java-tools e sua liberação binária também estará disponível no repositório github. A captura instantânea de desenvolvimento mais recente foi postada. [Faça o download.
](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

A ferramenta usa uma API REST aprimorada após a liberação beta para ***fazer upload das entradas de recursos***, portanto, a instância de serviço de destino deve ser a versão GA. 
* Origem: beta ou GA
* Destino: somente GA

Para copiar todos os dados de pacote configurável em uma instância de serviço de Globalização para outra instância, use o comando a seguir:

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url` e os outros valores de parâmetro estão localizados nas credenciais do serviço de origem/destino, por exemplo: 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
Além disso, toda a CLI do GP foi atualizada para suportar credenciais em formato json,
além das opções individuais `(-s / -i / -u / -p)`. É possível criar
um arquivo json com conteúdo, como este abaixo: 

creds.json 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"

} 
```
Em seguida, é possível especificar o arquivo por `-j
<json-file>`. No comando `copy/copy-all-bundles`, é possível substituir

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

com

`-j creds.json `
 
Como alternativa, é possível copiar o pacote configurável de um local para outro usando o comando: 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**Nota:** dois parâmetros adicionais, `-b <source-bundle-id>` e `-d <dest-bundle-id>`, podem ser usados além daquelas para copiar todos os pacotes configuráveis (copy-all-bundles). Esse comando pode ser usado para copiar um pacote configurável dentro da mesma instância. Nesse caso, é possível eliminar os parâmetros de credencial de serviço de destino `(--dest-*)`.


Os comandos acima extraem dados existentes de pacote configurável e de entrada de recurso e faz o upload deles para o novo local. Durante o processo, alguns campos controlados pelo servidor REST serão atualizados (como o campo updatedBy/updatedAt). Além disso, como esses comandos não copiam dados de ligação e configuração de serviço, você pode precisar configurar serviços de MT na instância de destino.


Por exemplo, a versão beta suporta a tradução árabe por meio do Watson Language Translator. Na versão GA, a tradução em árabe não é mais oferecida gratuitamente. Quando você portar dados beta na nova instância GA, o conteúdo em árabe já traduzido será preservado. Nenhuma mudança no idioma de origem acionará a tradução em árabe automaticamente, a menos que você configure a ligação do Watson para ativar a tradução em árabe. Esse também é o caso de quando a instância de origem é a versão GA. A ligação de serviços de MT externa é específica de uma instância GP; a ligação/configuração para outra instância não será portada automaticamente. 

