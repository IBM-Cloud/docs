---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# High Security Business Network (HSBN) vNext Beta
{: #etn_overview}

**HSBN vNext Beta** propose une solution clé en main pour la génération d'un réseau métier de blockchain. Ce service met rapidement à disposition le réseau et offre une surveillance pour une gestion et une maintenance simplifiées de vos ressources.  Ce processus de création et de gouvernance d'un réseau permet de consacrer davantage de temps et d'attention au développement et au déploiement de solutions métier.
{:shortdesc}

Les réseaux **HSBN vNext Beta** s'exécutent dans un environnement hautement sécurisé sur LinuxONE, où toutes les ressources réseau (homologues, auteurs de commande, AC, code source, registre) figurent tous au sein d'un **IBM Secure Service Container** (SSC). Ils offrent les fonctionnalités suivantes :
* Optimisation des performances pour la communication d'égal à égal
* Haute disponibilité et infrastructure pour l'évolutivité 
* Chiffrement matériel, clés de chiffrement infalsifiables, et machines virtuelles chiffrées de manière sécurisée
* Amorçage sécurisé avec logiciel infalsifiable
* Aucun droit d'accès de l'utilisateur root
* Conformité FIP, protection élevée de niveau Evaluation Assurance, vérifiabilité et optimisation du chiffrement

Un abonnement au plan **HSNB vNext bêta** inclut la prise en charge des ressources réseau suivantes :

- Un service de commande tolérant aux pannes
- 2 homologues par membre
- Jusqu'à 5 membres réseau supplémentaires
- 5 codes blockchain instanciés par membre
- Une autorité de certification spécifique aux membres
- Jusqu'à 100 canaux
- Des règles de gouvernance par défaut (tous les membres sont des administrateurs et ils peuvent émettre des invitations à rejoindre le réseau)

Pour plus de détails sur les fonctions de sécurité de l'environnement, consultez la section [IBM Secure Service Container](etn_ssc.html).

## Utilisation du plan HSBN vNext bêta
{: #use_hsbn}

### Accès au plan

Le plan **HSBN vNext bêta** d'IBM Blockchain sur Bluemix est garanti à la demande. Lorsque vous sélectionnez HSBN vNext bêta dans le catalogue Bluemix et créez une instance de service, votre demande de participation à la dernière version bêta est envoyée à l'équipe IBM Blockchain. Une fois la demande acceptée, vous recevez une invitation par e-mail pour participer au plan ; suivez les instructions pour lancer le tableau de bord HSBN vNext bêta.

Sur le tableau de bord HSBN vNext bêta, sélectionnez l'une des trois options possibles :
1. **Network Quick Start** : Créez un réseau HSBN vNext bêta et invitez d'autres organisations Bluemix à rejoindre le réseau. 
2. **Join Network** : Consultez les invitations qui vous sont adressées pour rejoindre d'autres réseaux HSBN vNext bêta.
3. **Monitor Network** : Gérez vos ressources réseau: homologues, canaux et code blockchain.

<!-- to do - the rest of this page final edit -->

### Exemple de scénario

Supposons que vous soyez un fabricant de billes et vous souhaitez utiliser le réseau IBM Blockchain pour effectuer des transactions avec différents vendeurs. Comment pourriez-vous procéder ? Vous pourriez créer un canal de consortium contenant tous les membres réseau et l'état actuel de votre référentiel de billes accessible au public. Toutes les transactions ayant lieu sur ce canal seront visibles et pourront être interrogées pour tous les membres du réseau. Vous pourriez cependant créer également des "sous-canaux" ou des canaux autonomes pour répondre aux questions de vie privée et de confidentialité. Disons par exemple que vous proposez un meilleur prix à certains vendeurs s'ils remplissent un certain nombre de conditions. Cette transaction peut être menée dans le sous-canal, avec l'impact qui s'ensuit sur votre approvisionnement en billes qui est mis à jour sur le canal de consortium. Ou encoure, vous souhaitez peut-être échanger un classe particulière de billes qui n'est même pas disponible sur le canal de consortium. Vous effectueriez simplement des transactions avec la partie concernée sur un canal autonome et le registre du consortium ne serait pas concerné. Les canaux constituent un puissant mécanisme pour la confidentialité des données car ils disposent tous de registres uniques, et seuls les membres qui sont abonnés et authentifiés auprès d'un canal peuvent interagir avec le registre.  

### Création d'un réseau
{: create_a_network}
Le réseau inclut les composants suivants :
* Un service de commande chargé de l'authentification des transactions et de leur classement en blocs pour les registres des canaux. 
* Une autorité de certification spécifique aux membres chargée d'émettre un matériel de vérification d'identité pour les composants réseau de chaque membre.
* Des homologues spécifiques aux membres qui exécutent et valident des transactions, et gèrent le registre d'un canal.

Sur le tableau de bord du service Blockchain, cliquez sur le bouton **Network Quick Start** et suivez les instructions de l'assistant :
1. Sur la page **Name your Network**, entrez le nom du réseau de blockchain et le nom de société qui représentera votre identité de membre, puis cliquez sur **Next** ;
2. Sur la page suivante **Invite members**, indiquez les informations pertinentes concernant l'organisation pour les participants que vous voulez inviter. Un homologue et une autorité de certification seront mis à disposition de chaque participant qui rejoint le réseau, et tous les membres réseau gèrent un registre pour chaque canal qu'ils ont rejoint. <br>
   **Remarque :** Vous pouvez inviter au maximum 5 membres au sein d'un réseau.
3. Sur la page **Define Governance Rules**, vous pouvez voir les paramètres de stratégie réseau. Par défaut, toute personne sur le réseau peut créer de nouveaux canaux et inviter des membres.  
4. Sur la page **Generate Certificate**, utilisez l'option **Auto generated** afin de créer les certificats pour les composants réseau de votre organisation. Ces certificats x509 ne sont pas présentés à l'utilisateur.  
5. Enfin, sur la page **Review summary**, passez en revue la configuration de votre réseau et cliquez sur **Done** pour amorcer votre réseau.

Ce processus termine la configuration initiale de votre réseau.

### Rejoindre un réseau
{: invite_members}

Une fois le réseau initialisé, vos invités reçoivent un e-mail indiquant le réseau que vous les avez invités à rejoindre et les instructions à suivre. Les invités peuvent voir que le bouton **Pending invites** est activé sur le tableau de bord du plan HSBN vNext. Cliquez sur ce bouton pour rejoindre le réseau :

1. Sélectionnez le réseau dans la liste et cliquez sur **Join Network**.
2. A l'écran suivant, passez en revue la gouvernance et cliquez sur **Next**.
3. Sur la page **Generate Certificate**, entrez le nom de votre organisation, puis sélectionnez l'option **Auto generated**.
4. Sur la page **Review Network Summary**, passez en revue les paramètres du réseau et cliquez sur **Done**. Les paramètres indiquent également les **participants invités** qui ont reçu les invitations à rejoindre le réseau.

Pour plus de détails sur la création de canaux et l'installation/instanciation de code blockchain, consultez la section [Surveillance](v10_dashboard.html).

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
