---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Armazenando objetos grandes {: #large-files}

Os uploads são limitados a um tamanho máximo de 5 GB para um único upload. No entanto, é possível segmentar objetos maiores em partes menores e usar um arquivo manifest para concatenar os segmentos. Quando um objeto é concatenado não há tamanho máximo.
{: shortdesc}

Os objetos grandes podem ser dinâmicos ou estáticos. Com objetos grandes estáticos (SLO), os segmentos não precisam estar no mesmo contêiner; cada segmento pode ser armazenado em qualquer contêiner e receber qualquer nome. Com os objetos grandes dinâmicos, o Cliente Swift cria um contêiner e segmentos numerados que são transferidos por upload em paralelo ao contêiner.


## Objetos grandes dinâmicos: {: #dynamic}

É possível fazer upload de objetos grandes dinâmicos de duas maneiras:
  * Ter o cliente Swift manipulando tudo automaticamente
  * Usar a API Swift para fazer isso você mesmo

#### Usando o Cliente Swift para lidar com objetos grandes dinâmicos

O cliente Swift usa o parâmetro `-segment-size` para dividir seu
objeto em partes menores. O cliente cria um novo contêiner com o nome do contêiner no
qual você deseja para fazer upload dos arquivos e inclui um sufixo com o número do
segmento (`<container_name>_segments`). Os segmentos são
transferidos por upload em paralelo. Após o upload de todos os segmentos, eles são
transferidos por upload como um objeto concatenado para um arquivo manifest com o nome do
arquivo original.

1. Depois de ter efetuado login no {{site.data.keyword.Bluemix_notm}} e
estar pronto para o upload, execute o comando a seguir para segmentar seu arquivo.
    ```
    swift upload <container_name> <file_name> --segment-size <size_in_bytes>
    ```
    {: pre}

#### Usando a API Swift para manipular Objetos grandes dinâmicos

É possível segmentar os objetos para que eles tenham 5 GB ou menos e, em seguida, fazer upload deles por meio da API do Swift.

**Observação**: ao fazer upload, todos os segmentos devem ser transferidos por upload antes do arquivo manifest. Se o objeto for transferido por download antes de todos os segmentos serem transferidos por upload, o objeto transferido por download será concatenado inconsistentemente.

É possível fazer upload de arquivos
grandes concluindo as etapas a seguir.

1. Classifique os segmentos por nome na ordem em que eles precisarão ser concatenados para formar o objeto original.
2. Faça upload de seus segmentos em um contêiner que seja separado do contêiner
que contém o arquivo manifest. A limitação para uploads começa após o décimo segmento ser transferido por upload e aumenta consideravelmente o tempo de upload.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000002
    ```
    {: pre}

3. Faça upload de um arquivo manifest vazio com o cabeçalho
`X-Object-Manifest` configurado com o valor correspondente
`<container>/prefix>`.

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <container_name>/<object_name>/" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}

    **Nota**: o arquivo manifest deve ficar vazio. Se não, o conteúdo do arquivo é considerado como um dos segmentos e cai na ordem de concatenação que é ditada pelos nomes classificados.
4. Faça download do objeto. Como resultado, você recebe o objeto inteiro. É
possível incluir ou remover segmentos sem precisar atualizar o arquivo manifest. Segmentos com o prefixo correto permanecem como parte do objeto. Excluir o manifest não exclui os segmentos.

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


## Objetos grandes estáticos {: #static}

Os objetos grandes estáticos usam segmentos e um arquivo manifest, mas você tem mais controle. Com SLO, os segmentos não precisam estar no mesmo contêiner; cada segmento pode ser armazenado em qualquer contêiner e receber qualquer nome. No entanto, os segmentos devem ter pelo menos 1 MB. Não é necessário definir um cabeçalho para o arquivo manifest, embora o cabeçalho “X-Static-Large-Object” seja automaticamente incluído e configurado como true após um manifest correto ser transferido por upload.
{: shortdesc}

O arquivo manifest é um documento JSON que fornece detalhes dos segmentos e deve ser transferido por upload depois que todos os segmentos foram transferidos por upload. Os dados que são fornecidos para cada segmento no manifest é comparado com os metadados de segmentos reais. Se algo não corresponder, o manifest não será transferido por upload.

<table>
<caption> Tabela 1. Atributos JSON o arquivo manifest </caption>
  <tr>
    <th> Atributo </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> <i>path</i> </td>
    <td> O local e o nome do segmento. Especificado como container_name/object_name. </td>
  </tr>
  <tr>
    <td> <i> etag </i> </td>
    <td> Fornecido pela solicitação PUT quando o objeto é transferido por upload. É possível também localizá-lo executando um HEAD para o objeto. </td>
  </tr>
  <tr>
    <td> <i> size_bytes </i> </td>
    <td> O tamanho do objeto, em bytes. </td>
  </tr>
</table>



#### Para fazer upload de arquivos grandes

1. Execute o comando a seguir para fazer upload dos segmentos. A limitação para uploads começa após o décimo segmento ser transferido por upload e aumenta consideravelmente o tempo de upload.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    ```
    {: pre}

2. Construa o manifest:

    ```
    [
        {
            "path": "<container_one>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "size_bytes": 801882690
        },
        {
            "path": "container_two/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "size_bytes": 1048576
        },
        {
            "path": "<container_one>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "size_bytes": 138257
        }
    ]
    ```
    {: pre}

3. Faça upload do arquivo manifest incluindo a consulta `multipart-manifest=put` no nome do manifest.

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}

4. Faça download do objeto.

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}


#### Trabalhando com objetos grandes estáticos

É possível gerenciar seus arquivos usando os comandos a seguir.

**Observação**: para incluir ou remover segmentos no objeto, faça upload de um novo arquivo manifest com uma nova lista de segmentos. O
nome do manifest pode permanecer o mesmo.

* Para fazer download do conteúdo do arquivo manifest, deve-se incluir a
consulta `multipart-manifest=get` em seu comando. O conteúdo que você recebe não é idêntico ao conteúdo que você transferiu por upload.

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=get
    ```
    {: pre}

* Para excluir o manifest, execute o comando a seguir:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}

* Para excluir o manifest e todos os segmentos, inclua a consulta `multipart-manifest=delete` após o nome do manifest:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=delete
    ```
    {: pre}
