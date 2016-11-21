---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Trabalhando com arquivos grandes {: #large-files}
*Última atualização: 19 de outubro de 2016*
{: .last-updated}

O upload de objetos é limitado a um tamanho máximo de 5 GB em um único upload. No
entanto, ainda será possível fazer upload de objetos maiores que 5 GB se segmentá-los em
objetos menores. Após o upload dos objetos segmentados, um arquivo manifest também será
necessário para concatenar os segmentos no objeto original. Há duas maneiras de fazer isso: Objetos Grandes Dinâmicos (DLO) e Objetos Grandes Estáticos (SLO).
{: shortdesc}

### Objetos grandes dinâmicos: {: #dynamic}

Há duas maneiras de manipular DLO:
  * Ter o cliente Swift manipulando tudo automaticamente
  * Usar a API Swift para fazer isso você mesmo

#### Usando o cliente Swift para manipular objetos grandes dinâmicos

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

Você mesmo pode segmentar os objetos para que eles tenham 5 GB ou menos e, em
seguida, fazer upload deles por meio da API Swift. Ao fazer upload, é importante que seja
feito primeiro o upload de todos os segmentos antes de fazer o do manifest. Se o objeto
for transferido por download antes de todos os segmentos terem concluído o upload, o
objeto transferido por download será inconsistente. É possível fazer upload de arquivos
grandes concluindo as etapas a seguir.

1. Classifique os segmentos por nome na ordem em que eles deverão ser concatenados para formar o objeto original.
2. Faça upload de seus segmentos em um contêiner que seja separado do contêiner
que contém o arquivo manifest. O regulador para uploads inicia após o décimo segmento ter
sido transferido por upload e aumenta o tempo de upload consideravelmente. Por esse
motivo, é recomendado que o tamanho do segmento não seja menor que o tamanho do arquivo
dividido por 10.

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
    
    **Nota**: o arquivo manifest deve ficar vazio. Se não estiver, o
conteúdo do arquivo será considerado como um dos segmentos e cairá na ordem de concatenação que é
ditada pelos nomes classificados.
4. Faça download do objeto. Você receberá o objeto inteiro como resultado. É
possível incluir ou remover segmentos sem precisar atualizar o arquivo manifest. Os
segmentos com o prefixo correto continuarão parte do objeto. A exclusão do manifest não
excluirá os segmentos.

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


### Objetos grandes estáticos {: #static}

Objetos grandes estáticos usam segmentos e um arquivo manifest, mas permitem mais
controle. Com SLO, os segmentos não precisam estar no mesmo contêiner; cada segmento
pode ser armazenado em qualquer contêiner e receber qualquer nome. No entanto, os
segmentos devem ter pelo menos 1 MB. Você não é obrigado a configurar um cabeçalho para o arquivo manifest, embora o cabeçalho “X-Static-Large-Object” seja automaticamente incluído e configurado como true após um manifest correto ter sido transferido por upload.
{: shortdesc}

O arquivo manifest é um documento JSON que fornece detalhes dos segmentos e
deve ser transferido por upload depois que todos os segmentos foram transferidos por
upload. Os dados fornecidos para cada segmento no manifest são comparados com os
metadados dos segmentos reais. Se algo não corresponder, o manifest não será transferido
por upload.

<table>
  <tr>
    <th> Atributo </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> path </td>
    <td> O local e o nome do segmento. Especificado como container_name/object_name. </td>
  </tr>
  <tr>
    <td> etag </td>
    <td> Fornecido pela solicitação PUT quando o objeto é transferido por upload. É possível também localizá-lo executando um HEAD para o objeto.</td>
  </tr>
  <tr>
    <td> size_bytes </td>
    <td> O tamanho do objeto, em bytes. </td>
  </tr>
</table>

*Tabela 1: Atributos JSON no arquivo manifest na ordem de concatenação*

É possível fazer upload de arquivos grandes concluindo as etapas a seguir:

1. Execute o comando a seguir para fazer upload dos segmentos. O regulador para
uploads inicia após o décimo segmento ter sido transferido por upload e aumenta o tempo
de upload consideravelmente. Por esse motivo, é recomendado que o tamanho do segmento não
seja menor que o tamanho do arquivo dividido por 10.

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
    
3. Faça upload do manifest. Para fazer isso, deve-se incluir a consulta
`multipart-manifest=put` no nome do manifest executando o comando a
seguir:

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}
    
4. Faça download do objeto. 

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}
    
Aqui estão alguns comandos que podem ser necessários ao trabalhar com Objetos grandes estáticos.

* Para fazer download do conteúdo do arquivo manifest, deve-se incluir a
consulta `multipart-manifest=get` em seu comando. O conteúdo que você
recebe não será idêntico ao conteúdo transferido por upload.

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

**Nota**: para incluir segmentos no objeto ou removê-los dele,
você precisa fazer upload de um novo arquivo manifest com uma nova lista de segmentos. O
nome do manifest pode permanecer o mesmo.
