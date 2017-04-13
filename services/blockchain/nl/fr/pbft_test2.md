---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Test de consensus 2 : Un noeud Byzantine
{: #pbft_test2}

Dernière mise à jour : 4 août 2016
{: .last-updated}

Le test de consensus 2 teste le protocole PBFT dans un scénario de réseau où l'un des quatre noeuds est de type Byzantine : un noeud s'est déconnecté de façon arbitraire et simultanée.
{:shortdesc}

Le protocole PBFT garantit qu'un réseau de blockchain comportant N homologues continuera de fonctionner si au maximum (N-1)/3 homologues se déconnectent en mode Byzantine (de façon arbitraire et simultanée). Votre environnement de chaîne de blocs Bluemix comporte quatre homologues, de sorte que si l'un d'eux plante, le réseau continuer d'exécuter le consensus et d'ajouter des transactions dans le registre. L'application de la formule PBFT révèle que (4-1)/3 = 1 = nombre de noeuds Byzantine, de sorte que le traitement de transaction sur le réseau de blockchain se poursuit.

Procédez comme suit pour tester PBFT sur un réseau à quatre noeuds avec un noeud Byzantine :
1.	Connectez-vous avec votre ID utilisateur et mot de passe réseau :   
    a.  Exécutez POST sur ***VP0 URL***/registrar  
    b.  Exécutez le contenu : {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  L'homologue retourne le contenu
2.  Vérifiez que le réseau est opérationnel :  
    a.  Interrogez la hauteur de chaîne de blocs pour chaque homologue, en indiquant l'URL de chaque homologue :   
    b   Exécutez GET ***VP0 URL***/chain  
    c.  La commande retourne le contenu :
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message":
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d. La demande est transmise à l'ensemble des quatre homologues sur le réseau. Les homologues exécutent le protocole de consensus PBFT, et conviennent d'exécuter cette demande et de stocker le résultat sur leurs copies respectives du livre.  
    e.  Notez que toutes les transactions sont asynchrones. Le contenu retourné comporte un hachage de code blockchain, que vous utiliserez dans des appels de code blockchain ultérieurs.  
    f.  L'achèvement du déploiement dépend de facteurs comme la vitesse de processeur et le temps d'attente des réseaux.  
4.  A des fins de test, simulez le noeud Byzantine VP2 en l'arrêtant manuellement, à l'aide du bouton d'arrêt dans l'interface.  (**Remarque **: Entre 30 et 60 secondes peuvent s'écouler avant que votre interface n'indique que le noeud VP2 est "Arrêté".)
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
    d.  La demande est de nouveau transmise à l'ensemble des quatre homologues. Les homologues exécutent le protocole de consensus PBFT, et conviennent d'exécuter cette demande et de stocker le résultat sur leurs copies respectives du livre.
6.  Cette demande est aussi asynchrone. Après un court intervalle, vérifiez que l'opération d'appel est terminée en demandant la valeur de la variable “a” sur le code blockchain :  
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
7.  Comme prévu, la valeur de “a” est inférieure de 1 par rapport à la période où le code blockchain a été déployé à l'origine.
8.  Vous pouvez continuer à exécuter des opérations d'appel (invoke) et de requête (query) supplémentaires. Le processus est le même que dans les étapes précédentes.

(FIN du test de consensus 2)
