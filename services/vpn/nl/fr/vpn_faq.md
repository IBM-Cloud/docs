---

copyright :

  années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# FAQ - {{site.data.keyword.vpn_short}}
{: #vpn_faq}
*Dernière mise à jour : 17 mars 2016*

La section ci-dessous contient les réponses aux questions les plus fréquentes.
{:shortdesc}

1. Quels dispositifs de fournisseur tiers sont habilités dans les labos IBM pour l'interopérabilité avec le service IBM VPN ?

	Le labo IBM a testé les périphériques de passerelle VPN suivants pour l'inter-opération avec le service IBM VPN :

	* Cisco Adaptive Security Appliance (ASA) Software Version 8.2(1). [Voir exemple de configuration](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7. [Voir exemple de configuration](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic. [Voir exemple de configuration](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic. [Voir exemple de configuration](vpn_onpremises.html#strongswan){: new_window}

	De plus, un périphérique de passerelle VPN conforme aux normes IPSec d'un autre fournisseur doit pouvoir fonctionner correctement avec le service IBM VPN.

2. Avec quelle rapidité un échec d'homologue pourra-t-il être détecté ?
 
	Un échec d'homologue est détecté conformément à la valeur configurée pour l'intervalle de signal de présence. Le paramètre par défaut est de 60 secondes.

3. Combien de passerelles VPN et de connexions peut-on créer par service VPN ?
 
	Vous pouvez créer un dispositif de passerelle VPN par service VPN dans un espace Bluemix. Vous pouvez définir jusqu'à 16 connexions à différentes destinations par passerelle VPN. 

4. Quand doit-on utiliser le service IBM VPN et quand doit-on utiliser le service Bluemix Secure Gateway ?

	Les deux services sont utilisés pour offrir une connectivité sécurisée entre vos ressources Bluemix et votre centre de données sur site. 

	Utilisez le service IBM VPN lorsque vous souhaitez assurer la connectivité entre deux noeuds finaux. Le service VPN forme une connexion IPSec Layer 3 sécurisée entre
vos réseaux sur site et l'environnement de cloud IBM Bluemix. Le service IBM VPN est uniquement disponible pour accéder aux conteneurs IBM (conteneurs Docker). 

	Utilisez le service Bluemix Secure Gateway si vous souhaitez établir une connexion sécurisée entre le noeud final d'une application spécifique dans Bluemix et un autre noeud
final au sein de votre centre de données sur site. 

5. Puis-je utiliser le service IBM VPN pour accéder à mes conteneurs et serveurs virtuels au sein de l'environnement de cloud IBM Bluemix à l'aide de leurs adresses IP privées ?
 
	A l'heure actuelle, le service IBM VPN permet uniquement d'accéder aux conteneurs Bluemix.

6. Puis-je définir le service IBM VPN au niveau de l'organisation Bluemix ?

	A l'heure actuelle, le service IBM VPN est uniquement disponible au niveau de l'espace Bluemix. Si votre organisation Bluemix possède plusieurs espaces, un service
VPN séparé peut être défini pour chaque espace.

7. Comment peut-on connecter le service IBM VPN avec le service GaaS (SoftLayer Gateway Appliance) ?

	Vous pouvez créer un tunnel IPSec pour établir une communication sécurisée entre le service IBM VPN et le service SoftLayer GaaS. [Voir exemple de configuration.](vpn_onpremises.html#gaas){: new_window}
