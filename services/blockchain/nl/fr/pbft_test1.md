---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Test de consensus 1: Aucun noeud Byzantine
{: #pbft_test1}
Dernière mise à jour : 4 août 2016
{: .last-updated}

Le test de consensus 1 teste le protocole de consensus PBFT dans un scénario de réseau de blockchain où aucun des quatre noeuds n'est de type Byzantine : aucun de ces noeuds ne s'est déconnecté de façon arbitraire et simultanée.
{:shortdesc}

Après le lancement de votre plan Developer Network ou High Security Business Network, procédez comme suit pour tester PBFT sans noeuds Byzantine :

(**Remarque **:  Les fragments de code et les instructions utilisent différentes valeurs symboliques.  **VPO URL**, **"test_user1"**, **"test_user1_enrollSecret"** et **YOUR_CHAINCODE_ID** sont simplement des espaces réservés.  Pour connaître les valeurs littérales de vos **données d'identification de service** et **URL VP**, consultez l'onglet **APIs** sur votre console réseau.  La valeur de **YOUR_CHAINCODE_ID** figure sous l'onglet **Network** dès que vous avez déployé une portion de code blockchain sur le réseau.  En outre, les valeurs hachées dans vos contenus de réponse JSON seront différents de ceux figurant dans ces exemples.)

1.	Connectez-vous avec votre ID utilisateur et mot de passe réseau :   
    a. Exécutez POST sur ***VP0 URL***/registrar  
    b.	Exécutez le contenu {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}  
    c.	L'homologue retourne le contenu
2.	Vérifiez que le réseau est opérationnel :  
    a.	Interrogez la hauteur de chaîne de blocs pour chaque homologue, en indiquant l'URL de chaque homologue :  
    b.  Exécutez GET ***VP0 URL***/chain  
    c.  L'homologue retourne le contenu :
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	S'il s'agit de la première opération sur la chaîne de blocs, la hauteur de chaîne est 1, car le seul bloc sur la chaîne est le bloc d'origine. La hauteur de chaîne augmente au fur et à mesure de l'ajout de transactions dans le registre.
3.	Déployez le code blockchain :   
    a.	Exécutez POST sur ***VP0 URL***/chaincode  
    b.  Avec le contenu :  
       ```
       {
       "jsonrpc": "2.0",
       "method": "deploy",
       "params": {
       "type": 1,
       "chaincodeID":{
       "path":"github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02"
       },
       "ctorMsg": {
       "function":"init",
       "args": ["a", "1000", "b", "2000"]
       },
       "secureContext": "***test\_user1***"
       },
       "id": 1
       }
       ```
     c.  L'homologue retourne le contenu :  
       ```
       {
       "jsonrpc": "2.0",
       "result": {
       "status": "OK",
       "message":
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. La demande est transmise à l'ensemble des quatre homologues sur le réseau. Les homologues exécutent le protocole de consensus PBFT, et conviennent d'exécuter cette demande et de stocker le résultat sur leurs copies respectives du livre.  
    e.	Notez que toutes les transactions sont asynchrones. Le contenu retourné comporte un hachage de code blockchain, que vous utiliserez dans des appels de code blockchain ultérieurs.
4.  Après un court intervalle, vérifiez que la demande de déploiement est terminée :  
    a.  Interrogez la hauteur de chaîne de blocs pour chaque homologue, en indiquant l'URL de chaque homologue :  
    b.  Exécutez GET ***VP0 URL***/chain  
    c.  La commande retourne le contenu :
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  L'achèvement de l'opération de déploiement dépend de facteurs comme la vitesse de processeur et le temps d'attente des réseaux.
5.  A présent que vous avez déployé un code blockchain, vous pouvez appeler des opérations sur le code blockchain :   
    a.  A l'aide de chaincode_example02, déplacez l'unité 1 de a vers b :  
    b.  Exécutez POST sur ***VP0 URL***/chaincode avec le contenu :
      ```
      {
      "jsonrpc": "2.0",
      "method": "invoke",
      "params": {
      "type": 1,
      "chaincodeID":{
      "name":"YOUR_CHAINCODE_ID"
      },
      "ctorMsg": {
      "function":"invoke",
      "args": ["a", "b", "1"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 2
      }
      ```
    c.  L'homologue retourne le contenu :
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
      },
      "id": 2
      }
      ```  
    d.  La demande est de nouveau transmise à l'ensemble des quatre homologues. Les homologues exécutent le protocole de consensus PBFT, et conviennent d'exécuter cette demande et de stocker le résultat sur leurs copies respectives du livre.
6.  La demande précédente est asynchrone. Après un court intervalle, vérifiez que l'opération d'appel est terminée en demandant la valeur de la variable “a” sur le code blockchain :  
    a.  Exécutez POST sur ***VP0 URL***/chaincode avec le contenu :
      ```
      {
      "jsonrpc": "2.0",
      "method": "query",
      "params": {
      "type": 1,
      "chaincodeID":{
      "name":"YOUR_CHAINCODE_ID"
      },
      "ctorMsg": {
      "function":"query",
      "args": ["a"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 3
      }
      ```   
    b.  L'homologue retourne le contenu :
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "999"
      },
      "id": 3
      }
      ```
    c.  Comme prévu, la valeur de "a" est inférieure de 1 par rapport à la période où le code blockchain a été déployé à l'origine.  Souvenez-vous que la valeur d'origine affectée à "a" était 1 000 et que la valeur d'origine affectée à "b" était 2 000.  La demande d'appel que vous avez déclenchée à l'étape 5 produit une unité transférée de "a" à "b".
7.  Vous pouvez continuer à exécuter des opérations d'appel (invoke) et de requête (query). Le processus est le même que dans les étapes précédentes.

  (FIN du test de consensus 1)
