---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Environnement réseau
{: #networkEnvironment}

Une fois mise à disposition votre instance de service WebSphere Application Server pour {{site.data.keyword.Bluemix_notm}}, vous pouvez accéder à votre machine virtuelle de plusieurs façons. Vous pouvez vous connecter via un VPN (réseau privé virtuel) sécurisé pour obtenir le SSH, la console d'administration WebSphere traditionnelle et l'accès aux applications sur votre machine virtuelle. Vous pouvez également connecter votre machine virtuelle à Internet avec une adresse IP publique.

Le diagramme suivant montre ces chemins réseau :

Figure 1. Vue du client de la mise en réseau multilocation avec IP publique 

![Figure 1. Vue du client de la mise en réseau multilocation avec IP publique](images/wasaas_multi_tenantPublicIP.gif) 

## Accès au VPN (réseau privé virtuel) 
{: #vpnAccess}

Après avoir configuré une instance de service WebSphere Application Server pour {{site.data.keyword.Bluemix_notm}} à partir du Tableau de bord du service dans l'interface graphique {{site.data.keyword.Bluemix_notm}}, vous pouvez télécharger vos données d'identification VPN et établir une connexion OpenVPN. Vous pouvez ensuite accéder à votre machine virtuelle via SSH. Vous pouvez également accéder à votre centre d'administration Liberty, à la console d'administration WebSphere traditionnelle et aux applications.

## Accès public à Internet
{: #publicInternetAccess}

En option, vous pouvez demander une adresse IP publique pour votre machine virtuelle du serveur WebSphere en cliquant sur **Manage Public IP** sur le Tableau de bord du service dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}} et en demandant une IP publique. Ce processus réserve l'adresse IP pour ce serveur. Ensuite, cliquez sur **Open IP** pour ouvrir la connexion depuis Internet vers votre instance de service WebSphere Application Server pour {{site.data.keyword.Bluemix_notm}}.

## Ports d'adresses IP publiques
{: #publicIPports}

Lorsque vous ouvrez l'accès à votre IP publique, l'adresse IP est associée à votre machine virtuelle et les ports 80 et 443 sont ouverts à la passerelle. Toutefois, par défaut, Liberty Core et les serveurs WebSphere Base traditionnels n'ouvrent pas les ports 80 et 443. À l'inverse, les ports 80 et 443 sont ouverts par défaut sur le serveur IBM HTTP. Par conséquent, vous devrez peut-être configurer vos serveurs Liberty Core et WebSphere Base traditionnels pour écouter le trafic d'application sur le port 80/443 lorsque vous utilisez une adresse IP publique.
* Pour configurer votre serveur Liberty Core, voir [Configurer le serveur Liberty Core pour l'accès public](networkEnvironment.html#configureLibertyForPublicAccess).
* Pour configurer votre serveur WebSphere Base traditionnel, ajoutez une chaîne de transport de conteneur Web écoutant le port 80/443 comme décrit dans [Configuration des chaînes de transport](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window}.

## Ports d'adresses IP privées de réseau privé virtuel
{: #privateIPports}

Vous vous connectez à l'adresse IP privée de votre machine virtuelle sur la connexion de réseau privé virtuel. Votre centre d'administration Liberty (9080, 9443), la console d'administration WebSphere traditionnelle (9060, 9043), SSH (22) et les ports autres que 80/443 ne sont accessibles que par la connexion VPN comme illustré à la Figure 1. Voir l'exemple Liberty Core **server.xml** et **ibm-web-bnd.xml** pour plus de détails sur la séparation du centre d'administration Liberty d'avec vos ports d'application.

**Évitez les problèmes :** pour les serveurs Liberty Core et WebSphere Base traditionnels, les ports de port de pare-feu sont préconfigurés lorsque votre machine virtuelle est configurée. Toutefois, pour les configurations de déploiement réseau où le gestionnaire de déploiement ou le contrôleur collectif est localisé avec IBM HTTP Server, vous devrez peut-être ouvrir des ports sur le pare-feu. Voir [Ports de pare-feu](systemAccess.html#firewall_ports) pour plus de détails.

## Configurer le serveur Liberty Core pour l'accès par adresse IP publique
{: #configureLibertyForPublicAccess}

Vous devez configurer Liberty Core pour écouter le trafic d'application sur le port 80/443 lorsque vous utilisez l'adresse IP publique.

Par défaut, Liberty est configuré avec le centre d'administration Liberty et les applications disponibles sur l'hôte virtuel **default_host**qui est associé au **defaultHttpEndpoint** sur les ports 9080 et 9443. Reconfigurez votre serveur pour séparer le centre d'administration Liberty de l'hôte virtuel d'application et du noeud final et pour les rendre disponibles sur des ports distincts.

Le fragment de code suivant est un exemple de réglages de configuration de server.xml : 

```    
    <!-- open port 9080/9443 for incoming http connections -->
    <httpEndpoint id="defaultHttpEndpoint"
        host="*"
        httpPort="9080"
        httpsPort="9443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!-- define a new endpoint for public app traffic -->
    <httpEndpoint id="publicHttpEndpoint"
        host="*"
        httpPort="80"
        httpsPort="443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!– restrict default_host to vpn so the Liberty Admin Center is not public -->
    <virtualHost id="default_host" allowFromEndpointRef="defaultHttpEndpoint">
      <hostAlias>*:9080</hostAlias>
      <hostAlias>*:9443</hostAlias>
    </virtualHost>

    <virtualHost id="external_host">
      <hostAlias>*:80</hostAlias>
      <hostAlias>*:443</hostAlias>
    </virtualHost>
```
{: codeblock}

Ensuite, associez votre application à l'hôte virtuel **external_host** en incluant le fragment suivant dans le fichier **META-INF/ibm-web-bnd.xml** de votre application :

```
    <?xml version="1.0" encoding="UTF-8"?>
    <web-bnd
        xmlns="http://websphere.ibm.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://websphere.ibm.com/xml/ns/javaee   
        http://websphere.ibm.com/xml/ns/javaee/ibm-web-bnd_1_0.xsd"
        version="1.0">

        <virtual-host name="external_host" />
    </web-bnd>
```
{: codeblock}
