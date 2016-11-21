---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Modèles d'application et tutoriels
{: #1stanchor}
Dernière mise à jour : 5 octobre 2016
{: .last-updated}

Les modèles ci-après illustrent le fonctionnement des applications et de la fonction de code blockchain dans un réseau IBM Blockchain. Pour en savoir plus sur le code Hyperledger Fabric v0.5 qui sous-tend votre réseau de blockchain, consultez la section [Fabric Docs](https://github.com/hyperledger/fabric/tree/master/docs) du projet Hyperledger de Linux Foundation.  
{:shortdesc}

Pour expérimenter des applications de code blockchain en action, vous pouvez déployer immédiatement les démos Marbles (Billes), Commercial Paper (Document commercial) ou Car Lease (Location de voiture) ci-dessous (cliquer sur un bouton Déployer dans Bluemix). Vous pouvez aussi poursuivre votre lecture afin de parcourir le tutoriel Code blockchain Hello.

- [![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## Utilisation du tutoriel Code blockchain Hello
{: #hellocc}
Ce tutoriel vous guide tout au long de l'utilisation de blocs de construction de base pour le codage d'une application de code blockchain élémentaire. Vous allez générer de manière incrémentielle un code blockchain opérationnel qui crée des actifs génériques pour la réalisation d'échanges sur un réseau. Vous allez ensuite interagir avec votre code blockchain via l'API réseau. A l'issue de ce tutoriel, vous saurez répondre aux questions suivantes :
- Qu'est-ce que le code blockchain ?
- Comment puis-je implémenter du code blockchain ?
- Existe-t-il des dépendances ?
- Quelles sont les fonctions principales ?
- Comment puis-je transmettre différentes valeurs à mes arguments ?
- Comment puis-je inscrire de manière sécurisée un utilisateur sur mon réseau ?
- Comment puis-je compiler mon code blockchain ?
- Comment puis-je interagir avec mon code blockchain via l'API REST ?

### Qu'est-ce que le code blockchain ?
Le code blockchain est du code Go (GoLang) ou Java qui permet aux utilisateurs d'interagir avec un réseau de blockchain. Chaque fois que vous 'appelez' (invoke) une transaction sur le réseau, vous appelez une fonction en code blockchain qui lit et écrit des valeurs dans le registre.

### Implémentation de votre premier code blockchain
Suivez les procédure des rubriques ci-après pour implémenter du code blockchain sur un réseau IBM Blockchain sur Bluemix :
#### Configuration de l'environnement
1. Téléchargez et installez Golang pour votre système d'exploitation à partir de : [GoLang](https://golang.org/dl/).
2. Définissez votre chemin GOPATH :
	- $GOPATH est le chemin d'une **variable d'environnement** pour votre code Go et vos projets. Votre chemin $GOPATH doit être défini pour l'obtention, la génération et l'installation de packages à l'extérieur de l'arborescence Go standard. Par conséquent, $GOPATH doit être unique et différent du chemin $GOROOT dans lequel réside votre arborescence Go d'origine. Créez simplement un répertoire et faites pointer votre chemin $GOPATH dessus.
	- Pour définir votre chemin $GOPATH sous Windows :
		- Créez un répertoire d'espace de travail pour votre projet, par exemple C:\Users\ADMIN\Documents\GoProjects.
		- Cliquez sur le menu **Démarrer** de Windows et recherchez "variables d'environnement système".
		- Cliquez sur **Modifier les variables d'environnement système**.
		- Sous l'onglet **Paramètres système avancés**, cliquez sur **Variables d'environnement**.
		- Localisez vos variables d'environnement système GOPATH et GOROOT. Si vous devez créer GOPATH, cliquez sur **Nouvelle**.  
		- Vos valeurs GOROOT et GOPATH doivent être uniques. La valeur GOROOT est générée automatiquement lors de l'installation de Go. Il doit s'agir de C:\Go\.
		- Définissez votre valeur GOPATH sur le répertoire d'espace de travail que vous avez créé. Dans cet exemple, **GOPATH** est défini sur **C:\Users\ADMIN\Documents\GoProjects**.  
		- Pour plus de détails, exécutez la commande `go help gopath` ou consultez le site Web de la [Documentation Go](https://golang.org/doc/install).
3. Ajoutez le code shim Hyperledger Faric v0.5 dans votre chemin Go en exécutant la commande suivante :

	```
	go get github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview/core/chaincode/shim
	```

4. **Remarque **: Assurez-vous de suivre le lien ci-dessus pour importer le code shim hyperledger-archives v0.5. Le back end Bluemix est créé avec cette même gestion des versions ; par conséquent, il est important d'aligner la version shim et la version Bluemix.

#### Configuration de GitHub
Dans les plans Blockchain sur Bluemix, votre code blockchain doit se trouver dans un référentiel [GitHub](https://Github.com/). Créez un compte GitHub et configurez Git comme décrit dans [Set Up Git](https://help.github.com/articles/set-up-git/). Une fois GitHub configuré, procédez comme suit :
1. Accédez à la section [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) et déviez le référentiel.  
2. Clonez la déviation dans le répertoire indiqué dans votre valeur $GOPATH.  
3. Le référentiel inclut deux répertoires de code blockchain : [Start](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go) est le code blockchain à partir duquel vous allez démarrer la génération. [Finished](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go) est le code blockchain que vous allez générer au final.
4. Assurez-vous que le code blockchain est généré dans votre environnement local. Ouvrez une invite de commande, puis accédez au dossier contenant `chaincode_start.go`. Entrez la commande suivante :

	```
	go build ./
	```
La commande ne doit retourner aucune erreur ni aucun message.

#### Implémentation de l'interface de code blockchain
L'étape suivante consiste à implémenter l'interface shim du code blockchain dans votre code Golang. Les trois principales fonctions sont : **Init**, **Invoke** et **Query**. Ces trois fonctions prennent un nom de fonction et un tableau de chaînes en entrée, mais elles varient en fonction du moment où elles sont appelées. Vous allez générer un code blockchain qui crée des actifs génériques pour des échanges sur un réseau de blockchain.

### Dépendances
L'instruction `import` répertorie les dépendances qui sont requises pour la génération de votre code blockchain :
1. `fmt` - contient `Println` pour le débogage/la consignation.
2. `errors` - format d'erreur Go standard.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - code qui sert d'interface entre votre code Golang et un homologue réseau.

### Transmission de valeurs

Les valeurs de code blockchain suivantes sont transmises :
#### Init()
La valeur Init est appelée pour initialiser votre code blockchain lorsque vous effectuez un premier déploiement sur le réseau. Dans cet exemple, vous utilisez `Init` pour configurer l'état initial d'une variable dans le registre.

Dans votre fichier `chaincode_start.go`, modifiez la fonction `Init` de sorte qu'elle stocke le premier élément `args` dans la clé "hello_world" :

```go
func (t *SimpleChaincode) Init(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting 1")
	}

	err := stub.PutState("hello_world", []byte(args[0]))
	if err != nil {
		return nil, err
	}

	return nil, nil
}
```

Cette opération est effectuée à l'aide de la fonction shim `stub.PutState`. Le premier argument est la clé sous forme de chaîne, et le second argument est la valeur sous la forme d'un tableau d'octets. Cette fonction peut retourner une erreur, que votre code inspecte et retourne, le cas échéant.

#### Invoke()
La valeur `Invoke` est appelée pour ajouter une demande de transaction à la chaîne. La structure de `Invoke` est simple ; elle reçoit un argument `function`, et en fonction de cet argument, appelle des fonctions Go dans le code blockchain.

Dans votre fichier `chaincode_start.go`, modifiez la fonction `Invoke` de sorte qu'elle appelle une fonction d'écriture générique.

```go
func (t *SimpleChaincode) Invoke(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("invoke is running " + function)

	// Handle different functions
	if function == "init" {
		return t.Init(stub, "init", args)
	} else if function == "write" {
		return t.write(stub, args)
	}
	fmt.Println("invoke did not find func: " + function)

	return nil, errors.New("Received unknown function invocation")
}
```

Le code recherche maintenant `write`, afin d'ajouter cette fonction dans votre fichier `chaincode_start.go` :

```go
func (t *SimpleChaincode) write(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
	var name, value string
	var err error
	fmt.Println("running write()")

	if len(args) != 2 {
		return nil, errors.New("Incorrect number of arguments. Expecting 2. name of the variable and value to set")
	}

	name = args[0]                            //rename for fun
	value = args[1]
	err = stub.PutState(name, []byte(value))  //write the variable into the chaincode state
	if err != nil {
		return nil, err
	}
	return nil, nil
}
```

Cette fonction `write` doit être similaire à votre modification précédente de la valeur `Init`. Vous pouvez maintenant définir la clé et la valeur de `PutState`, ce qui vous permet de stocker une paire clé/valeur dans le registre de chaîne de blocs.

#### Query()
La valeur `Query` est appelée pour interroger l'état votre code blockchain, et elle n'ajoute pas de blocs à la chaîne. Seules les fonctions deploy et invoke ajoutent de nouveaux blocs. Utilisez la valeur `Query` pour lire la valeur des paires clé/valeur de l'état de votre code blockchain.

Dans votre fichier `chaincode_start.go`, modifiez la fonction `Query` afin qu'elle appelle une fonction de lecture générique :

```go
func (t *SimpleChaincode) Query(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

Le code recherche maintenant `read`, afin d'ajouter cette fonction dans votre fichier `chaincode_start.go` :

```go
func (t *SimpleChaincode) read(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
	var name, jsonResp string
	var err error

	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting name of the var to query")
	}

	name = args[0]
	valAsbytes, err := stub.GetState(name)
	if err != nil {
		jsonResp = "{\"Error\":\"Failed to get state for " + name + "\"}"
		return nil, errors.New(jsonResp)
	}

	return valAsbytes, nil
}
```

Cette fonction `read` utilise `GetState`, lequel est le complément de `PutState`. Cette fonction shim prend un seul argument de chaîne, qui est le nom de la clé à extraire. Ensuite, cette fonction retourne la valeur, sous la forme d'un tableau d'octets, vers `Query`, lequel à son tour l'envoie au gestionnaire REST.

#### Main()
La fonction `main` s'exécute lorsque chaque homologue déploie son instance du code blockchain. Elle démarre le code blockchain et l'enregistre auprès de l'homologue. Aucune mise à jour du code n'est nécessaire pour 'main' ; chaincode_start.go et chaincode_finished.go incluent une fonction `main` en haut de chaque fichier :

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### Interaction avec votre code blockchain
Le moyen le plus rapide de tester votre code blockchain est d'utiliser l'interface REST sur vos homologues.
L'interface utilisateur swagger sur le moniteur de votre tableau de bord Bluemix vous permet de vous exercer au déploiement de code blockchain, sans l'écriture d'aucun code supplémentaire.  

<br>
#### API swagger
Pour utiliser l'API, procédez comme suit :

1. Connectez-vous à [Bluemix](https://console.ng.bluemix.net/login) et assurez-vous d'être au niveau de l'onglet **Tableau de bord**.
1. Vérifiez que vous êtes dans le même "espace" Bluemix que celui contenant votre service IBM Blockchain. La navigation dans l'espace s'effectue à gauche.
1. Un panneau **Services** se trouve dans la partie inférieure ; cliquez sur votre service IBM Blockchain.
1. Vous devez voir un message "Bienvenue dans le service IBM Blockchain..." ; cliquez sur le bouton **LANCER** situé à droite.
1. Sur la page du moniteur, vous devez voir deux tableaux ; la tableau inférieur peut être vide.
	- **Onglet Réseau :**
		- Les **journaux de l'homologue** figurent dans le tableau supérieur. Sur la ligne de l'**homologue 1**, cliquez sur l'icône du fichier afin d'afficher le journal. En plus de cette vue statique, des **journaux d'homologue de diffusion** en temps réel figurent sous l'onglet **Journaux** dans la partie supérieure de la page.
		- Les **journaux de code blockchain** figurent dans le tableau inférieur. Chaque code blockchain est libellé à l'aide du hachage de code blockchain qui a été retourné lors de son déploiement. Sélectionnez l'homologue sur une ligne de code blockchain, puis cliquez sur l'icône de fichier afin d'afficher le journal.
	- **Onglet API **: Affiche la page de documentation d'API swagger.
1. Procédez ensuite comme indiqué ci-dessous pour implémenter l'inscription sécurisée. Les appels du noeud final `/chaincode` dans l'interface REST requièrent un ID de contexte sécurisé. Pour que les appels REST soient acceptés, vous devez transmettre un *enrollID* enregistré à partir de la liste des données d'identification de service :
  - Cliquez sur **+ ID d'inscription du réseau** pour développer la liste des valeurs *enrollID* et leurs secrets.
  - Copiez l'ensemble de données d'identification dans un fichier texte à des fins d'utilisation ultérieure.
  - Développez la section API du **Registraire**.
  - Développez la section `POST/registraire`.
  - Remplissez la zone ``Valeur`` à l'aide de contenu JSON qui spécifie une valeur ``enrollID` et `enrollSecret' de vos données d'identification :

  ![Exemple d'enregistrement](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Exemple d'enregistrement")

  Le *Corps de la réponse* doit être similaire à l'exemple suivant :

  ![Exemple d'enregistrement](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Corps de réponse de l'exemple d'enregistrement")

A présent qu'un ID `enrollID` est configuré, vous pouvez l'utiliser lors du déploiement, de l'appel et de l'interrogation de code blockchain dans les étapes ci-après.
### Déploiement de votre code blockchain
Pour pouvoir déployer votre code blockchain via l'interface REST, il est nécessaire que ce code blockchain soit stocké dans un référentiel GitHub public. Lorsque vous envoyez une demande de déploiement à un homologue, vous indiquez l'URL du référentiel de code blockchain, ainsi que les paramètres permettant d'initialiser le code blockchain.

**Avant de déployer** votre code blockchain, vérifiez qu'il peut être généré en local :
1. Ouvrez une invite de commande, puis accédez au répertoire contenant `chaincode_start.go`. Entrez la commande suivante :
	```
	go build ./
	```
1. Développez la section API de **Code blockchain**.
1. Développez la section `POST/code blockchain`.
1. Définissez la zone de texte `DeploySpec` (laissez les autres zones à blanc) à l'aide de l'exemple de code ci-dessous, en spécifiant le chemin de référentiel de votre code blockchain, ainsi que l'ID `enrollID` de l'étape `/registrar` précédente. La valeur `"path":` doit être semblable à : `"https://github.com/johndoe/learn-chaincode/finished"`. Il s'agit du chemin de votre déviation de référentiel, et du chemin d'accès au fichier chaincode_finished.go :

	```
	{
		"jsonrpc": "2.0",
		"method": "deploy",
		"params": {
			"type": 1,
			"chaincodeID": {
				"path": "https://github.com/ibm-blockchain/learn-chaincode/finished"
			},
			"ctorMsg": {
				"function": "init",
				"args": [
					"hi there"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 1
	}
	```

  Le *Corps de la réponse* doit être similaire à l'exemple suivant :

  ![Exemple de déploiement](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Corps de réponse de l'exemple de déploiement")

  La réponse au déploiement contiendra l'ID de ce code blockchain. Il s'agit d'un hachage alphanumérique à 128 caractères, que vous pouvez utiliser dans des appels ou des demandes de requête futures. Copiez cet ID dans votre éditeur de texte.

#### Interrogation
Interrogez votre code blockchain afin d'obtenir la valeur de la clé `hello_world`, que vous définissez à l'aide de la fonction `Init` :
1. Développez la section API de **Code blockchain**.
1. Développez la section `POST/chaîne codée`.
1. Remplissez la zone de texte `QuerySpec` (laissez les autres zones à blanc) à l'aide de l'exemple ci-dessous, en spécifiant l'ID de chaîne codé de l'étape de déploiement précédente, ainsi que l'ID `enrollID` de l'étape `/registrar` précédente :

	```
	{
		"jsonrpc": "2.0",
		"method": "query",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "read",
				"args": [
					"hello_world"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 2
	}
	```
Le *Corps de la réponse" doit être similaire à l'exemple suivant :  ![Exemple de requête](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Corps de réponse de l'exemple de requête")

  La valeur de `hello_world` est "hi there", laquelle a été définie par le corps de votre précédent appel de déploiement.

#### Appel
Appelez votre fonction d'écriture générique avec `invoke`. Définissez la valeur de `hello_world` sur "go away":
1. Développez la section API de **Code blockchain**.
1. Développez la section `POST/chaîne codée`.
1. Remplissez la zone de texte `InvokeSpec` (laissez les autres zones à blanc) à l'aide de l'exemple ci-dessous, en spécifiant l'ID de chaîne codé de l'étape de déploiement précédente, ainsi que l'ID `enrollID` de l'étape `/registrar` précédente :

	```
	{
		"jsonrpc": "2.0",
		"method": "invoke",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "write",
				"args": [
					"hello_world",
					"go away"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 3
	}
	```
Le *Corps de la réponse" doit être similaire à l'exemple suivant :  ![Exemple d'appel](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Corps de réponse de l'exemple d'appel")

  Réexécutez la requête ci-dessus ; vous devez obtenir la réponse suivante :

  ![Exemple Query2](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Réponse de l'exemple d'appel")

Vous venez d'écrire du code blockchain de base.  

<br>
## Eléments prérequis pour les démos Marbles (Billes), Commercial Paper (Document commercial) et Car Lease (Location de voiture)
{: #requirements}

Les éléments prérequis ci-après sont inclus avec votre service Bluemix pour l'exécution en local des applications Marbles, Commercial Paper et Car Lease. Votre environnement Bluemix clone Hyperledger pour fournir ces dépendances :

- ID Bluemix https://console.ng.bluemix.net/ (requis pour créer votre réseau IBM Blockchain et fournir des données d'identification de service pour les homologues et l'autorité de certification)
- Node.js 0.12.0+ et npm v2+
- Environnement Golang (requis uniquement pour générer votre propre code blockchain)

Les démos exigent un niveau de compétence avec Node.js et le module express. Vous devez également avoir une compréhension conceptuelle des termes 'code blockchain', 'registre' et 'homologue' dans le contexte d'une chaîne de blocs (voir le [Glossaire Hyperledger Fabric](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md)).  

<br>
## Utilisation de la démo Marbles (Billes)
{: #marbles}

L'application Marbles permet de démontrer un transfert d'actifs simple entre deux parties. Elle est conçue pour tester le logiciel SDK JavaScript, orienter son développement et aider les développeurs à se familiariser avec le logiciel SDK et le code blockchain.

Découvrez les [Tutoriels Marbles](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) pour en savoir plus sur les interactions entre l'application Web, le logiciel SDK et le code blockchain. Si vous connaissez déjà le code blockchain et IBM Blockchain, vous pouvez [déployer manuellement](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) la démo dans Bluemix, ou bien cliquer sur le bouton Déployer dans Bluemix pour utiliser l'application Web :
  
[![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Utilisation de la démo Commercial Paper (Document commercial)
{: #commercialpaper}

L'application Commercial Paper permet de démontrer comment un réseau de commerce de papier commercial peut être implémenté à l'aide d'IBM Blockchain. La démo Commercial Paper explore un réseau de blockchain privé, sur lequel les participants disposent de rôles qui leur sont affectés et des niveaux d'accès correspondants. Consultez le [Readme Commercial Paper](https://github.com/IBM-Blockchain/cp-web#readme) pour en savoir plus sur les composants de cette démo, ou procédez à un déploiement dans Bluemix immédiat afin de voir le réseau de commerce en action :   
[![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Utilisation de la démo Car Lease (Location de voiture)
{: #carlease}

L'application Car Lease permet de démontrer le cycle de vie d'un véhicule, de sa fabrication à la mise à la casse, après être passé entre les mains de plusieurs propriétaires. La démo utilise Node.js pour la programmation côté serveur, et Golang pour l'exécution du code blockchain sur le réseau IBM Blockchain. Elle comporte deux instances du code blockchain : la première définit les règles relatives aux transactions de véhicule et la deuxième consigne toutes les transactions du véhicule tout au long de son cycle de vie. Les deux programmes de code blockchain utilisent des objets JSON pour le stockage des données. Consultez le [Readme Car Lease](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) pour en savoir plus sur l'architecture de l'application et les attributs de véhicule associés à cette démo, ou bien déployez la démo immédiatement dans Bluemix :
  
[![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>
## Code blockchain non déterministe
{: #ndcc}

Les réseaux IBM Blockchain prennent en charge le code blockchain déterministe uniquement. L'utilisation de code blockchain non déterministe n'est pas possible et pourrait entraîner des erreurs graves sur le réseau de blockchain.

Le **code blockchain non déterministe** est un code blockchain qui ne produit **pas** de résultat dans la même valeur ajoutée, dans la durée et entre les noeuds, dans le registre de chaîne de blocs. En revanche, le **code blockchain déterministe** produit systématiquement la même valeur ajoutée, dans la durée et entre les noeuds, dans le registre de chaîne de blocs.

### Exemple de code blockchain déterministe
Une transaction **invoke** qui incrémente toujours la valeur d'une variable de un est déterministe, car le résultat est toujours le même, invariable, sur chaque noeud. Chaque fois que cette transaction est appliquée à la valeur cinq, par exemple, la valeur ajoutée est toujours six, sur chaque noeud, tout le temps. L'incidence sur le réseau d'un code blockchain déterministe est aucune divergence dans la chaîne de blocs ; la copie du registre sur chaque noeud indique toujours (après synchronisation) que la valeur est augmentée de un par rapport à l'appel précédent.

### Exemple de code blockchain non déterministe
Une transaction **invoke** qui incrémente la valeur d'une variable de chaîne de blocs avec le nombre de secondes écoulées depuis le début de la journée (00:00) est non déterministe, car sur la durée la valeur va varier entre les noeuds. Chaque fois que cette transaction est appliquée sur la valeur fixe cinq, par exemple, la valeur ajoutée diverge entre les noeuds (à de rares exceptions) car le nombre de secondes écoulées depuis 00:00 va inévitablement varier. L'incidence sur le réseau de ce code blockchain non déterministe est des chaînes de code divergentes ; tous les noeuds ne sont pas d'accord sur la valeur de cinq + le nombre de secondes écoulées depuis 00:00.

### Caractère aléatoire
Le code blockchain ne doit présenter de caractère aléatoire dans les valeurs ajoutées, dans la durée et entre les noeuds. Tout caractère aléatoire produirait des chaînes de blocs divergentes entre les noeuds, ce qui devrait ensuite être résolu par le réseau. Pour éviter cela, vous devez vous assurer qu'aucun code blockchain parallèle ne peut affecter la valeur en entrée du code blockchain d'appel. Par exemple, vous ne devez pas exécuter de transactions de **requête** en parallèle avec des transactions **invoke**, car les requêtes parallèles peuvent produire des écarts dans les valeurs d'appel entre les noeuds.

### Utilisation d'une variable globale
L'utilisation d'une variable globale ou d'une variable d'instance pour stocker une valeur qui a été extraire du registre, ou pour définir une valeur sur le registre, peut conduire à un non déterminisme. Le code blockchain ne doit pas reposer sur des variables globales ou des variables d'instance qui ne conserveront pas leur état entre les redémarrages d'un conteneur de code blockchain. L'exemple suivant utilise une variable globale. La valeur de `key`, qui est écrite dans le registre via la fonction `stub.PutState`, est dérivée d'une variable globale :

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Itération sur un type de mappe
L'itération sur un type de mappe peut mener au non déterminisme, car l'ordre n'est pas déterministe dans le langage de programmation Go. Voici un exemple d'itération sur la mappe nommée `columnTypes` :

```go
 func generateColumns(colTypes map[string]string, colKeys []bool) ([]*shim.ColumnDefinition, error) {
	var tableColumns []*shim.ColumnDefinition
	keyIndex := 0
	for k, _ := range colTypes {
		tableColumns = append(tableColumns, &shim.ColumnDefinition{k, shim.ColumnDefinition_STRING, colKeys[keyIndex]})

		keyIndex++
	}
	return tableColumns, nil
}
```

<!---## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples.--->
