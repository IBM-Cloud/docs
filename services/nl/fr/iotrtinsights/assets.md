---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}

# Gestion des actifs{: #manage-assets}

L'une des forces d'{{site.data.keyword.iotrtinsights_full}} est qu'il permet de mapper vos périphériques à vos actifs gérés et de créer des règles qui s'appliquent à tous les périphériques qui sont mappés à un actif.
{: shortdesc}

Par exemple, le seul et unique actif que vous souhaitez surveiller peut comprendre plusieurs périphériques et un grand nombre de capteurs. 

>**Astuce :** Vous pouvez répéter la procédure de mappage lorsque vos actifs sont mis à jour ou modifiés. Le paramètre `action` défini dans les fichiers de contexte et de mappage vous permet d'ajouter et de retirer des actifs et des périphériques.

Pour mapper vos périphériques à vos actifs :
1. Créez une liste d'actifs et sauvegardez-la dans un fichier CSV.
Ce fichier contient les données d'actif de votre logiciel de gestion des actifs.
Exemple de format de fichier :
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  Où :  
  - ASSETNUM - (**Obligatoire**) : Numéro d'ID d'actif dans votre système. (12)
  - ASSETTYPE - Type d'actif. (15)
  - AS_DESCRIPTION - Brève description de l'actif. (100)
  - AS_DESCRIPTION_LD - Description complète de l'actif. (32,000)
  - INSTALLDATE - (Date au format aaaa-MM-jj). Date d'installation de l'actif. 
  - AS_ITEMNUM - Numéro d'élément connexe pour l'actif. (30)
  - AS_ITEMSETID - Numéro de jeu d'éléments pour l'actif. (8)
  - AS_LOCATION - Emplacement de l'actif. (12)
  - PRIORITY - (Entier) Priorité de l'actif. (12)
  - PURCHASEPRICE - (Virgule décimale) Prix d'achat de l'actif. (10.2)
  - REPLACECOST - (Virgule décimale) Coût lié au remplacement de l'actif. (10.2)
  - SERIALNUM - Numéro de série de l'actif. (64)
  - AS_SITEID - ID du site dans lequel l'actif est installé. (8)
  - AS_STATUS - Etat de l'actif. (20)
  - ACTION - Un symbole `+` signifie que l'actif est ajouté, et un symbole `-` signifie que l'actif est retiré.   
  >**Astuce :** Le chiffre indiqué entre parenthèses représente la longueur maximale de la chaîne. Sauf indication contraire, le paramètre doit contenir des caractères alphanumériques de casse mixte.

5. Créez une liste de mappage d'actifs et de périphériques et sauvegardez-la dans un fichier CSV.
Ce fichier permet de mapper les actifs importés dans la liste d'actifs sur vos périphériques {{site.data.keyword.iot_short}}.
  Exemple de format de fichier :
```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  Où :
    - sourceType - Comprend les données {{site.data.keyword.iot_short}} suivantes pour votre périphérique :
      - orgid - ID de votre organisation {{site.data.keyword.iot_short}}
      - iot-device-type - Type de votre périphérique {{site.data.keyword.iot_short}}  
    - sourceID - ID de votre périphérique {{site.data.keyword.iot_short}}  
    - targetType - Utilisez le mot `asset` pour créer un mappage d'actifs
    - targetID - Entrée ASSETNUM pour l'actif provenant du fichier de contexte que vous avez créé
    - action - Un symbole `+` signifie que l'actif est mappé, et un symbole `-` signifie que l'actif a été retiré du mappage. 
2. Connectez-vous à la console {{site.data.keyword.iotrtinsights_short}} en tant qu'utilisateur administrateur.
2. Accédez à **Périphériques > Gérer des groupes de périphériques** et cliquez sur **Importer un actif**.  
3. Recherchez le fichier d'actif que vous avez créé et sélectionnez-le.
4. Cliquez sur l'![icône Créer](images/create.png "icône Créer") pour créer la liste d'actifs. 
3. Recherchez le fichier de mappage d'actifs et de périphériques que vous avez créé et sélectionnez-le.
4. Cliquez sur l'![icône Créer](images/create.png "icône Créer") pour créer la liste d'actifs. 
5. Accédez à **Périphériques > Gérer des groupes de périphériques** et cliquez sur l'un de vos actifs pour afficher la liste des périphériques que vous avez mappés à cet actif. 
