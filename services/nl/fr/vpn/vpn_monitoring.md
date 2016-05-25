---

copyright :

  années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Surveillance de l'état et du flux de trafic
{: #monitor}  
*Dernière mise à jour : 17 mars 2016*  

Utilisez la fonction de surveillance pour afficher l'état de connexion et le débit du flux de trafic entre votre passerelle VPN de serveur SoftLayer ou sur site et la passerelle
{{site.data.keyword.vpn_short}}. 
{:shortdesc}  
##Surveillance sur le tableau de bord du service
{: #dashboard}

Sélectionnez l'onglet **Monitoring** pour afficher les statistiques de connexion suivantes.

* **Connection Status :** Etat de la connexion VPN entre votre passerelle VPN de serveur SoftLayer ou sur site et la passerelle IBM VPN. Valeurs : 1=UP, -1=DOWN 
* **Outbound Traffic Rate in bytes/second and packets/second :** Débit du trafic allant de la passerelle IBM VPN à votre passerelle VPN de serveur SoftLayer ou sur site.  
* **Inbound Traffic Rate in bytes/second and packets/second :** Débit du trafic allant de votre passerelle VPN de serveur SoftLayer ou sur site à la passerelle IBM VPN.  

Les statistiques de surveillance s'affichent sous forme de graphique et contiennent les données des dernières 48 heures. Les graphiques sont automatiquement mis à jour toutes les 20 minutes. Cependant,
vous pouvez extraire les données les plus récentes à tout moment en sortant de l'onglet Monitoring et en y accédant à nouveau.

**Remarque :** Les graphiques utilisent l'heure UTC et non l'heure locale.  
##Surveillance sur Logmet
{: #logmet}

Utilisez [Logmet](https://logmet.{DomainName}) pour afficher des statistiques de connexion détaillées. 

1. Connectez-vous avec vos données d'identification Bluemix et l'espace et le nom d'organisation sur lesquels vous avez créé l'instance de service IBM VPN.  
2. Sélectionnez l'icône de dossier (![](images/folder.png)) dans l'angle supérieur droit.
3. Sélectionnez **VPN Service Monitoring** dans la liste des tableaux de bord pour afficher les graphiques. Les graphiques utilisent l'heure locale.  

**Remarque :** Vous devez sélectionner l'onglet **Monitoring** sur le tableau de bord du service IBM VPN au moins une fois pour envoyer
une requête à Logmet afin de créer le tableau de bord du service VPN dans Logmet. Une fois la connexion au VPN établie, Logmet met jusqu'à 10 minutes pour afficher les statistiques de connexion.


