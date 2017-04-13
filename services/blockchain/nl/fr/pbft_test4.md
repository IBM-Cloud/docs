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


# Test de consensus 4 : Redémarrage d'un noeud Byzantine
{: #pbft_test1}


Le test de consensus 4 teste le protocole PBFT dans un scénario de réseau où l'un des quatre noeuds s'est reconnecté après avoir été un noeud de type Byzantine : une noeud est redémarré après s'être déconnecté de manière arbitraire et simultanée.

Un homologue Byzantine précédent qui a depuis rejoint un réseau de blockchain détectera que sa copie du registre aura un retard de synchronisation par rapport aux autres homologues. L'homologue en retard met automatiquement à jour son registre en copiant les blocs manquants d'un homologue par le registre actuel ; ce processus est appelé transfert d'état.
{:shortdesc}

Notez que ce scénario de test requiert un grand nombre d'opérations d'appel. Les homologues s'informent les uns les autres des états de leur registre actuel en envoyant des messages de *point de contrôle* internes ; l'homologue en retard détermine son retard en consultant ces messages.

Procédez comme suit pour tester PBFT après le redémarrage d'un noeud Byzantine :
1. Connectez-vous avec votre ID utilisateur et mot de passe réseau :   
   a. Exécutez POST sur ***VP0 URL***/registrar  
   b. Exécutez le contenu {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}  
   c.	L'homologue retourne le contenu
2. Vérifiez que le réseau est opérationnel :  
   a.	Interrogez la hauteur de chaîne de blocs pour chaque homologue, en indiquant l'URL de chaque homologue :  
   b. Exécutez **GET ***VP0 URL***/chain**  
   c. La commande retourne le contenu :  
```json
{
"currentBlockHash":
"RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d.	S'il s'agit de la première opération sur la chaîne de blocs, la hauteur de chaîne est 1, car le seul bloc sur la chaîne est le bloc d'origine. La hauteur de chaîne augmente au fur et à mesure de l'ajout de transactions dans le registre.
3. Déployez le code blockchain :   
   a.	Exécutez POST sur ***VP0 URL***/chaincode  
   b. Avec le contenu :  
```json
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
   c. L'homologue retourne le contenu :
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "YOUR_CHAINCODE_ID"
},
"id": 1
}
```
   d. La demande est transmise à l'ensemble des quatre homologues sur le réseau. Les homologues exécutent le protocole de consensus PBFT, et conviennent d'exécuter cette demande et de stocker le résultat sur leurs copies respectives du livre.  
   e. Toutes les transactions sont asynchrones. Le contenu retourné comporte un hachage de code blockchain, que vous utiliserez dans des appels de code blockchain ultérieurs. f. L'achèvement de l'opération de déploiement dépend de facteurs comme la vitesse de processeur et le temps d'attente des réseaux.  
4. A des fins de test, simulez un homologue VP2 qui se déconnecte en mode Byzantine (de façon arbitraire et simultanée), en arrêtant manuellement le noeud à l'aide du bouton d'arrêt de l'interface.
5. Exécutez une opération d'appel sur le code blockchain :  
   a. Dans cet exemple, chaincode_example02 déplace 1 unité de a vers b :  
   b. Exécutez POST sur ***VP0 URL***/chaincode with payload:
```json
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
  c. L'homologue retourne le contenu :
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
},
"id": 2
}
```
   d. La demande est de nouveau transmise à l'ensemble des quatre homologues sur le réseau. Les homologues exécutent le protocole de consensus PBFT, et conviennent d'exécuter cette demande et d'ajouter le résultat à leurs copies respectives du registre.  
6. Cette demande est aussi asynchrone. Après un court intervalle, vérifiez que l'opération d'appel est terminée :   
   a. Exécutez POST sur ***VP0 URL***/chaincode with payload:
```json
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
"args":["a"]
}
“secureContext”: “***test\_user1***”
},
"id": 3
}
```
   b. L'homologue retourne le contenu :
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "999"
},
"id": 3
}
```
   c. Comme prévu, la valeur de "a" est 1 ou moins.
7. Simulez l'homologue **VP2** qui se reconnecte en le redémarrant manuellement, à l'aide du bouton de démarrage dans l'interface.
8. Envoyez des opérations d'appel (invoke) à l'homologue VP0.
9. Interrogez les valeurs de code blockchain de “a” sur l'ensemble des quatre homologues. Tous les homologues retournent la même valeur pour “a".  (**Remarque **: Le temps nécessaire à l'homologue redémarré (**VP2**) pour exécuter la fonction `stateTransfer` dépend d'un certain nombre de paramètres.  Le rappel de ce PBFT ne requiert que 2f + 1 homologues pour l'obtention d'un consensus.  Par conséquent, un grand nombre d'appels peuvent être nécessaires pour que l'homologue **VP2** "se rattrape" étant donné qu'il n'est pas requis pour le consensus dans les circonstances actuelles.  Pour plus de détails sur l'implémentation de ce consensus, consultez la [spécification de protocole](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1) Hyperledger/Fabric du projet Hyperledger de Linux Foundation.

(FIN du test de consensus 4)
