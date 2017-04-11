---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Création et connexion d'un simulateur de terminal Node-RED
Utilisez Node-RED pour créer un simulateur de terminal et envoyer des données de terminal simulé à votre organisation {{site.data.keyword.iot_full}}.  
{:shortdesc}

Node-RED est un outil qui permet de relier des terminaux matériels, des API et des services en ligne selon des méthodes inédites et intéressantes. Pour plus d'informations, voir le site Web [Node-RED ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://nodered.org/){: new_window}.   

Vous pouvez exécuter votre instance Node-RED dans votre propre environnement ou l'utiliser en tant qu'application {{site.data.keyword.Bluemix_notm}}. Le processus suivant inclut les instructions relatives à {{site.data.keyword.Bluemix_notm}}.

Pour créer et connecter le simulateur de terminal Node-RED :

1. Créez le simulateur de terminal Node-RED
   Utilisez le simulateur de terminal pour envoyer des messages de terminal MQTT à {{site.data.keyword.iot_short_notm}}. Le simulateur de terminal a simulé l'envoi de données pour un conteneur de fret à un courtier MQTT, par exemple, {{site.data.keyword.iot_short_notm}}.
    1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} (https://console.ng.bluemix.net).
    2. Sélectionnez l'onglet **Catalogue**.
    3. Localisez la section Boilerplates du catalogue de service et cliquez sur **Node-RED Starter Community BETA**. **Astuce : ** Cliquez[ici ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/starters/node-red-starter/){: new_window} pour accéder directement à la page Node-RED Starter. 
    4. Sur la page Node-RED Starter, sélectionnez l'espace où vous souhaitez déployer Node-RED, vérifiez les sélections pour Créer une application, puis cliquez sur **Créer** pour ajouter Node-RED à votre organisation Bluemix.  
    Par exemple :  
     - Espace : dev
     - Nom : myDevice
     - Hôte : myDevice

    Conservez les valeurs par défaut des options restantes. Une fois l'application déployée, vous êtes conduit sur la page Start coding with Node-RED.  
    **Remarque :** Le processus de transfert peut prendre quelques minutes.

    3. Cliquez sur le lien Routes pour ouvrir Node-RED.  
    Exemple : `http://simulatedDevice.mybluemix.net`
    4. Cliquez sur **Go to your Node-RED flow editor** pour ouvrir l'éditeur.
    5. Copiez les données de flux Node-RED que vous avez trouvées dans la section [Données de flux de noeud Node-RED](#flow_data) du présent document.
    5. Dans l'éditeur de flux Node-RED, cliquez sur le menu situé dans l'angle supérieur droit, puis sélectionnez **Importer > Presse-papiers**.  
    6. Collez le contenu du presse-papiers dans la zone d'entrée des noeuds d'importation, puis cliquez sur **Ok**.
    Le flux du simulateur de terminal est importé dans l'éditeur de flux.

2. Enregistrez votre terminal auprès de {{site.data.keyword.iot_short_notm}}  . Pour connecter l'exemple de terminal Node-RED, procédez comme suit :
 1. Dans {{site.data.keyword.Bluemix_notm}}, accédez au tableau de bord.
 2. Sélectionnez l'espace dans lequel vous avez déployé {{site.data.keyword.iot_short_notm}}.
 3. Cliquez sur la vignette **{{site.data.keyword.iot_short_notm}}**.
 4. Cliquez sur **Lancer le tableau de bord** pour ouvrir le tableau de bord {{site.data.keyword.iot_short_notm}}.
 5. Sélectionnez **Terminaux**.
 6. Cliquez sur **Ajouter un terminal**.
 7. Cliquez sur **Créer un type de terminal**.
 9. Entrez un nom descriptif et une description pour le type de terminal, par exemple, `sample_device`.
 10. Facultatif : Entrez des attributs de type de terminal.
 11. Facultatif : Entrez des métadonnées de type de terminal.
 12. Cliquez sur **Créer** pour ajouter le nouveau type de terminal.
 13. Cliquez sur **Suivant** pour ajouter votre terminal.
 14. Entrez un ID de terminal, tel que `Device001`.
 15. Facultatif : Entrez des métadonnées de terminal.
 16. Cliquez sur **Suivant** pour ajouter une connexion de terminal à l'aide d'un jeton d'authentification généré automatiquement.
 17. Vérifiez que les informations récapitulatives sont correctes, puis cliquez sur **Ajouter** pour ajouter la connexion.
 18. Sur la page Informations sur le terminal qui s'affiche, copiez et sauvegardez les informations sur le terminal :  
  <ul>
  <li> ID d'organisation
  <li> Type de terminal
  <li> ID de terminal
  <li> Méthode d'authentification
  <li> Jeton d'authentification
  </ul>
  **Astuce :** Vous aurez besoin des informations ID d'organisation, Jeton d'authentification, Type de terminal et ID de terminal au cours des quelques étapes suivantes pour finaliser la configuration de l'application Node-RED et établir la connexion.

2. Connectez votre terminal à {{site.data.keyword.iot_short_notm}}.  
 1. Ouvrez l'éditeur de flux Node-RED.
 2. Cliquez deux fois sur le noeud Publish to IoT.
 3. Vérifiez que l'entrée de sujet est `iot-2/evt/event_name/fmt/json` **Astuce :** La partie /event_name du sujet définit le nom des événements publiés.
 4. Cliquez sur l'icône d'édition en regard de la zone Serveur.
 5. Mettez à jour le nom de serveur pour qu'il corresponde à votre organisation {{site.data.keyword.iot_short_notm}}.  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 Où {organization_ID} correspond à l'*ID d'organisation* que vous avez sauvegardé précédemment.
 6. Mettez à jour l'ID de client avec votre ID d'organisation, votre type de terminal et votre ID de terminal :
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   Où {organization_ID}, {device_type} et {device_ID} correspondent aux valeurs que vous avez sauvegardées précédemment.
 7. Cliquez sur l'onglet **Sécurité**.
 8. Vérifiez que la zone Nom d'utilisateur a pour valeur `use-token-auth`.
 9. Mettez à jour la zone Mot de passe avec le *jeton d'authentification* que vous sauvegardé précédemment.
 10. Cliquez sur **Mettre à jour**, puis sur **OK**.
 12. Dans l'angle supérieur droit de l'éditeur de flux Node-RED, cliquez sur **Déployer**.
 13. Vérifiez que la connexion du noeud Publish to IoT a pour statut *Connecté*.  **Astuce :** Si la connexion n'est pas établie, revérifiez les paramètres que vous avez saisis. Une simple petite erreur de copier-coller peut provoquer l'échec de la connexion.

4. Validez la connexion de terminal.
 1. Dans un autre onglet de navigateur ou une autre fenêtre de navigateur, ouvrez le tableau de bord {{site.data.keyword.iot_short_notm}}.
 2. Sélectionnez **Terminaux** et cliquez sur **Device001** ou sur le nom du terminal que vous avez ajouté, s'ils sont différents.  
 La page Informations sur le terminal s'ouvre. Cette vue vous permet d'afficher l'état de connexion pour votre terminal. A ce stade, le terminal doit apparaître comme étant déconnecté.   
 3. De retour dans l'éditeur de flux Node-RED, cliquez sur le bouton du noeud Inject afin de générer un contenu d'actif.  
 Le contenu comporte les points de données suivants :  
 ```
 {"d":
  { "name":"My Device",
    "location":
    {
      "longitude":-87.90,
      "latitude":43.03
    },
    "velocity":13,
    "type":"GPS"
  }
 }
 ```
  {:codeblock}  

 3. Dans l'onglet de débogage du panneau de droite, vérifiez que des messages sont créés.  
 4. De retour sur la page d'informations sur le terminal {{site.data.keyword.iot_short_notm}}, le terminal doit à présent apparaître comme étant connecté. Assurez-vous que vous voyez les mêmes points de données que ceux reçus du terminal.  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 Vous avez connecté votre exemple de terminal IoT à {{site.data.keyword.iot_short_notm}} et vous pouvez voir les données le concernant.

## Données de flux de noeud Node-RED
{: #flow_data}  
Copiez le texte suivant dans votre presse-papiers et collez-le dans le presse-papiers d'importation lorsque vous importez des noeuds dans l'éditeur de flux Node-RED.   
**Important :** Prenez soin de copier tout le texte, y compris les crochets de début et de fin.  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Cliquez deux fois sur le noeud.\n2. Cliquez sur l'icône d'édition en regard de la zone Serveur.\n3. Mettez à jour le nom de serveur pour qu'il corresponde à votre organisation Watson IoT Platform.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Mettez à jour l'ID de client avec votre ID d'organisation, votre type de terminal et votre ID de terminal :\n `d:organization_ID:device_type:device_ID`\n\n5. Cliquez sur l'onglet Sécurité.\n6. Vérifiez que la zone Nom d'utilisateur a pour valeur use-auth-token.\n7. Mettez à jour la zone Mot de passe avec le jeton d'authentification que vous avez sauvegardé précédemment.\n8. Cliquez sur Mettre à jour, puis sur OK.\n9. Dans l'angle supérieur droit de l'éditeur de flux Node-RED, cliquez sur Déployer. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"Le noeud Function vous permet de transmettre chaque message via une fonction JavaScript.\n\nLa fonction Javascript crée le contenu de message qui est envoyé à votre organisation Watson IoT Platform.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"Le noeud Debug entraîne l'affichage des messages dans la barre latérale Debug. Par défaut, seul le contenu du message est affiché, mais il est possible d'afficher la totalité de l'objet message.,"x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"Le noeud Inject vous permet d'injecter des messages dans un flux, soit en cliquant sur le bouton sur le noeud, soit en définissant un intervalle entre les injections.,"x":75,"y":236,"wires":[]}]
```
{:codeblock}
