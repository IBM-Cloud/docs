---

copyright:
  years: 2016
lastupdated: "2016-08-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Test de consensus 3 : Deux noeuds Byzantine
{: #pbft_test2}


Le test de consensus 3 teste le protocole de consensus PBFT dans un scénario de réseau où deux des quatre noeuds sont de type Byzantine : deux noeuds se sont déconnectés de façon arbitraire et simultanée.
{:shortdesc}

Le protocole PBFT garantit qu'un réseau de blockchain comportant N homologues continuera de fonctionner si au maximum (N-1)/3 homologues se déconnectent en mode Byzantine (de façon arbitraire et simultanée). Votre réseau de blockchain Bluemix comporte quatre homologues, de sorte que si deux homologues plantent, le réseau n'exécutera AUCUNE transaction et n'ajoutera pas de blocs dans le registre. L'application de la formule PBFT révèle que (4-1)/3 = 1 < le nombre de noeuds Byzantine (2), de sorte que le traitement de transaction s'arrête.

Procédez comme suit pour tester PBFT sur un réseau à quatre noeuds avec deux noeuds Byzantine :
1.  Connectez-vous avec votre ID utilisateur et mot de passe réseau :   
    a.  Exécutez POST sur ***VP0 URL***/registrar  
    b.  Exécutez le contenu {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}  
    c.  L'homologue retourne le contenu
2.  Vérifiez que le réseau est opérationnel :  
    a.  Interrogez la hauteur de chaîne de blocs pour chaque homologue, en indiquant l'URL de chaque homologue :   
    b.  Exécutez GET ***VP0 URL***/chain  
    c.  La commande retourne le contenu :
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  S'il s'agit de la première opération sur la chaîne de blocs, la hauteur de chaîne est 1, car le seul bloc sur la chaîne est le bloc d'origine. La hauteur de chaîne augmente au fur et à mesure de l'ajout de transactions dans le registre.
3.  Déployez le code blockchain :   
    a.  Exécutez POST sur ***VP0 URL***/chaincode  
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
      "message": "YOUR_CHAINCODE_ID"
      },
      "id": 1
      }
      ```
    d.  La demande est transmise à l'ensemble des quatre homologues sur le réseau. Les homologues exécutent le protocole de consensus PBFT, et conviennent d'exécuter cette demande et d'ajouter le résultat à leurs copies respectives du registre.  
    e.  Notez que toutes les transactions sont asynchrones. Le contenu retourné contient un ID transaction uniquement, que vous pouvez utiliser ultérieurement pour l'interrogation du résultat.
4.  A des fins de test, simulez des noeuds VP2 et VP3 qui se déconnectent, en mode Byzantine (de façon arbitraire et simultanée), en les arrêtant manuellement avec le bouton d'arrêt de l'interface.  (**Remarque **: Entre 30 et 60 secondes peuvent s'écouler avant que votre interface n'indique que les noeuds VP2 et VP3 sont "Arrêtés".)
5.  Exécutez une opération d'appel sur le code blockchain :  
    a.  Dans cet exemple, chaincode_example02 déplace 1 unité de a vers b :  
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
    d.  Etant donné que le réseau échoue au test PBFT f=(N-1)/3, l'opération d'appel est acceptée en entrée mais elle n'est pas exécutée, et rien n'est ajouté dans le registre partagé.
6.  Vérifiez que l'opération d'appel n'est pas exécutée, en interrogeant la valeur de la variable "a" :  
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
      "message": "1000"
      },
      "id": 3
      }
      ```
    c.  Notez que la valeur de “a” demeure inchangée.

  (FIN du test de consensus 3)
