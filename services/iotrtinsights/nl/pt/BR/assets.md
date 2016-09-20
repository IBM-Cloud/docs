---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Gerenciando recursos {: #manage-assets}

Um dos poderes do {{site.data.keyword.iotrtinsights_full}} é mapear os dispositivos para os ativos gerenciados e criar regras que se aplicam a todos os dispositivos mapeados para um ativo.
{: shortdesc}

Por exemplo, um único ativo em que você está interessado em monitorar pode incluir vários dispositivos e um grande número de sensores. 

>**Dica:** também é possível repetir o procedimento de mapeamento quando os ativos forem atualizados ou modificados. O parâmetro `action` nos arquivos de contexto e mapeamento permite incluir e remover ativos e dispositivos.

Para mapear os dispositivos para os ativos: 
1. Crie uma lista de ativos e salve como um arquivo CSV.
Esse arquivo inclui dados de ativo a partir do software de gerenciamento de ativos.
Formato de arquivo de amostra:  
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  Em que:  
  - ASSETNUM - **Necessário:** o número do ID do ativo no sistema. (12)
  - ASSETTYPE - O tipo de ativo. (15)
  - AS_DESCRIPTION - Uma breve descrição do ativo. (100)
  - AS_DESCRIPTION_LD - Uma descrição completa do ativo. (32.000)
  - INSTALLDATE - (Data no formato aaaa-MM-dd) A data em que o ativo foi instalado.
  - AS_ITEMNUM - Um número de item relacionado para o ativo. (30)
  - AS_ITEMSETID - O número do conjunto de itens para o ativo. (8)
  - AS_LOCATION - O local do ativo. (12)
  - PRIORITY - (Número inteiro) A prioridade do ativo. (12)
  - PURCHASEPRICE - (Decimal) O preço de compra do ativo. (10,2)
  - REPLACECOST - (Decimal) O custo para substituir o ativo. (10,2)
  - SERIALNUM - O número de série do ativo. (64)
  - AS_SITEID - O ID do site em que o ativo está instalado. (8)
  - AS_STATUS - O status do ativo. (20)
  - ACTION - Um símbolo `+` significa que o ativo foi incluído e um símbolo `-` significa que o ativo foi removido.  
  >**Dica:** o número entre parênteses indica o comprimento máximo da sequência. A menos que indicado, o formato de parâmetro é caracteres alfanuméricos, composto por letras maiúsculas e minúsculas.

5. Crie uma lista de mapeamento de ativos e dispositivos e salve como um arquivo CSV.
  Esse arquivo é usado para mapear os ativos importados na lista de ativos para os dispositivos do {{site.data.keyword.iot_short}}.
  Formato de arquivo de amostra:  
  ```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  Em que:
    - sourceType - Consiste nos dados do {{site.data.keyword.iot_short}} a seguir para seu dispositivo:
      - orgid - O ID da organização do {{site.data.keyword.iot_short}}
      - iot-device-type - O tipo de dispositivo do {{site.data.keyword.iot_short}}  
    - sourceID - O ID do dispositivo do {{site.data.keyword.iot_short}}  
    - targetType - Use a palavra `asset` para criar um mapeamento de ativos.
    - targetID - A entrada ASSETNUM para o ativo a partir do arquivo de contexto criado
    - action - Um símbolo `+` significa que o ativo está mapeado e um símbolo `-` significa que o ativo foi removido do mapeamento.
2. Efetue login no console do {{site.data.keyword.iotrtinsights_short}} como um usuário administrador.
2. Acesse **Dispositivos > Gerenciar grupos de dispositivos** e clique em **Importar ativo**.  
3. Procure e selecione o arquivo de ativos que você criou.
4. Clique em ![ícone Criar](images/create.png "ícone Criar") para criar a lista de ativos.
3. Procure e selecione o arquivo de mapeamento de ativos e dispositivos que você criou.
4. Clique em ![ícone Criar](images/create.png "ícone Criar") para criar a lista de ativos.
5. Acesse **Dispositivos > Gerenciar grupos de dispositivos** e clique em um dos ativos para ver uma lista dos dispositivos que você mapeou para o ativo. 
