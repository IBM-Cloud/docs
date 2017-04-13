---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Modèles d'application et tutoriels
{: #1stanchor}


Les modèles ci-après illustrent le fonctionnement des
applications et de la fonction de code blockchain dans un réseau IBM
Blockchain. Pour en savoir plus sur le code Hyperledger Fabric v0.6
qui sous-tend les réseaux IBM Blockchain, consultez la section
[Fabric
Docs](https://github.com/hyperledger/fabric/tree/v0.6/docs) du projet Hyperledger de Linux Foundation.
{:shortdesc}

Pour expérimenter des applications de code blockchain en action, vous pouvez déployer immédiatement les démos Marbles (Billes), Commercial Paper (Document commercial) ou Car Lease (Location de voiture) ci-dessous (cliquer sur un bouton Déployer dans Bluemix). Vous pouvez aussi poursuivre votre lecture afin de parcourir le tutoriel Code blockchain Hello.

- [![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## Tutoriel d'apprentissage du code blockchain
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
Le code blockchain est du code Go (GoLang) ou Java qui permet
aux utilisateurs d'interagir avec un réseau de blockchain. Chaque fois que vous 'appelez' (invoke) une transaction sur le réseau, vous appelez une fonction en code blockchain qui lit et écrit des valeurs dans le registre.  

<br>
## Configuration de l'environnement de développement
Pour commencer à développer du code blockchain, installez
d'abord les dépendances et les outils recommandés suivants :

### Git

- [Page de téléchargement de Git](https://git-scm.com/downloads)
- [Livre Pro Git](https://git-scm.com/book/en/v2)
- [Git Desktop (alternative à l'interface de ligne de commande Git)](https://desktop.github.com/)

Git est un outil de contrôle des versions rapide et puissant
pour le développement de code blockchain, et pour le développement
logiciel en général. Le terminal de ligne de commande Git bash,
installé avec Git for
Windows, est recommandé.

Une fois les installations de Git
terminée, vérifiez que Git est
installé :

```
$ git version
git version 2.9.0.windows.1
```

Une fois Git installé, créez un compte pour vous sur [GitHub](https://github.com/). Le service IBM Blockchain sur Bluemix exige que le code
blockchain se trouve dans un référentiel GitHub pour le
déploiement via l'API REST.  

## Go

Go est actuellement le seul langage pris en charge pour
l'écriture de code blockchain sur Bluemix. L'installation de Go
inclut un ensemble d'outils CLI utiles pour l'écriture de code
blockchain. Par exemple, la commande `go build`
vous permet de compiler votre code blockchain avant d'essayer de
le déployer sur un réseau. Installez Go v1.6, version utilisée pour
développer Hyperledger Fabric v0.6 :  

- [Installation de Go 1.6](https://golang.org/dl/#go1.6.3)
- [Instructions d'installation de Go](https://golang.org/doc/install)
- [Documentation et tutoriels Go](https://golang.org/doc/)

Vérifiez que Go est correctement installé en exécutant les
commandes ci-après. Le résultat de la commande
`go version`
peut varier, en fonction de votre système d'exploitation :

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

Il n'est pas nécessaire que votre variable d'environnement
`GOPATH`
corresponde à l'exemple précédent, mais vous devez
utiliser un répertoire valide sur votre système de fichiers. Lorsque
vous exécutez `go build` pour vérifier que votre
code blockchain compile, Go recherche dans le répertoire
`$GOPATH/src` la présence de dépendances
non standard que vous indiquez dans le bloc `import`
de votre code blockchain. Le guide comportant
les [instructions
d'installation de Go](https://golang.org/doc/install) vous indique comment définir la
variable d'environnement GOPATH.  

<br>
## Hyperledger Fabric

Deux versions d'Hyperledger Fabric sont prises en charge pour
Blockchain on Bluemix : la v0.5 et la v0.6.  Comme décrit ci-après,
la version de votre code blockchain doit s'aligner sur la version
d'Hyperledger sur votre réseau Bluemix.

Attention :
1. Pour activer les fonctions de lecture et d'écriture sur
le registre, votre code blockchain doit importer la cale de code
blockchain d'Hyperledger Fabric.
2. Pour compiler votre code blockchain en local, il est
nécessaire d'indiquer l'emplacement du code
Hyperledger Fabric dans votre variable d'environnement
`GOPATH`.

Pour déterminer la version d'Hyperledger
Fabric exécutée par votre instance Bluemix, cliquez sur l'onglet
**Statut du service** sur le moniteur de votre
tableau de bord.  Faites défiler jusqu'à la section
**Notes sur l'édition** ; le panneau
`Votre réseau utilise cette version` affiche le
**Niveau de validation Hyperledger** que vous
exécutez :

![Version de

back end Bluemix](images/fabricversion.png "Version deback end Bluemix")
Figure 1. Version d'Hyperledger Fabric

La version de votre code blockchain doit s'aligner sur la
version d'Hyperledger Fabric
dans laquelle vous allez déployer votre code blockchain. Par
exemple, le réseau représenté à la Figure 1 requiert le clonage du
codebase Hyperledger Fabric v0.6-preview. Le codebase de matrice,
pour chaque version, doit être chemin dans votre chemin
`$GOPATH/hyperledger/fabric` :

- [v0.5
Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6
HHyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

Pour installer la codebase Hyperledger Fabric v0.5,
utilisez la commande git clone suivante :

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

Pour installer la codebase Hyperledger Fabric v0.6, utilisez la
commande git clone suivante :

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

Si la matrice n'est pas correctement
installée dans votre chemin `GOPATH`, la
génération de votre code blockchain va retourner une erreur
similaire à l'exemple suivant :
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### Configuration de votre pipeline de développement

Procédez comme suit pour configurer un
pipeline pour l'écriture, la génération et le test de votre code
blockchain. Vous devez écrire le code blockchain sur votre machine
locale, vérifier qu'il compile, puis le, charger dans GitHub. Vous
devez ensuite déployer et tester votre code blockchain sur votre
réseau Bluemix à l'aide de l'API REST de la matrice :

1. Déviez la version appropriée du référentiel
[learn
chaincode](https://github.com/IBM-Blockchain/learn-chaincode) pour votre version de réseau vers votre
compte GitHub. Déviez la v1.0 pour un réseau de matrice v0.5, ou déviez
la v2.0 pour un réseau de matrice v0.6. Il est aussi possible
d'utiliser le bouton **Déviation** situé dans
l'angle supérieur droit de la page de référentiel. La
déviation copie l'intégralité du référentiel sur votre machine
locale, y compris toutes les branches, qui s'affichent en cliquant
sur le bouton **Branche: ** dans l'angle
supérieur gauche de la page. Pour effectuer une déviation à l'aide de
l'interface de ligne de commande, entrez les commandes suivantes dans
votre interpréteur de commandes bash Git :

2. Clonez votre déviation dans votre chemin $GOPATH :

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  Vous disposez maintenant d'une copie de votre déviation sur
votre machine locale. Vous pouvez écrire du code blockchain en
modifiant ou en ajoutant des fichiers locaux, en les
insérant dans votre déviation sur GitHub,
puis déployer votre code blockchain sur votre réseau de blockchain à
l'aide de l'API REST API sur un homologue réseau.

3. Les deux versions du code blockchain utilisé dans ce
tutoriel sont fournies : **start** est le
squelette de code
blockchain à partir duquel vous allez commencer,
et **finished* est votre code blockchain terminé qui
est prêt pour la génération. Tout d'abord, assurez-vous que
**start** génère dans votre environnement local :

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

La version **start** de
learn-chaincode
doit se compiler sans erreurs ni messages. Si ce n'est pas le cas,
passez en revue les instructions précédentes pour une installation
correcte de Go.

5. Ecrivez les modifications apportées à vos fichiers de
code blockchain locaux, puis insérez les fichiers mises à jour dans
votre déviation GitHub :

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  # See what files have changed locally.  You should see chaincode_start.go
  git status
  # Stage all changes in the local repository for commit
  git add --all
  # Commit all staged changes.  Insert a short description after the -m argument
  git commit -m "Compiled my code"
  # Push local commits back to https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  git push
  ```

#### Implémentez l'interface de code blockchain
L'étape suivante consiste à implémenter l'interface shim du
code blockchain dans votre code Go. Les trois principales fonctions
sont : **Init**, **Invoke** et
**Query**. Ces trois fonctions prennent un nom de
fonction et un tableau de chaînes en entrée, mais elles sont
appelées à des points différents. Votre chemin de développement se
termine avec l'utilisation d'un code
blockchain qui crée des actifs génériques pour des échanges sur un
réseau de blockchain.

### Dépendances
L'instruction `import` répertorie les
dépendances pour la génération de votre code blockchain :
1. `fmt` - contient `Println` pour le débogage/la consignation.
2. `errors` - format d'erreur Go standard.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - code qui sert d'interface entre votre code Golang et un homologue réseau.

#### Init()
La fonction `Init` est appelée lors du
premier déploiement de votre code blockchain. Comme son nom l'indique, utilisez cette fonction pour initialiser votre code blockchain. Dans cet exemple,
`Init` configure l'état initial d'une
paire clé/valeur unique sur le registre.

Dans votre fichier `chaincode_start.go`, modifiez la fonction `Init` de sorte qu'elle stocke le premier élément `args` dans la clé "hello_world" :

```go
func (t *SimpleChaincode) Init(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
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

Cette opération est effectuée à l'aide de la fonction stub
`stub.PutState`. Cette fonction interprète le
premier argument envoyé dans la demande de déploiement
comme la valeur qui doit être stockée sous la clé
'hello_world'. Si une erreur se produit parce qu'un nombre
incorrect d'arguments a été transmis, ou parce qu'un incident s'est
produit lors de l'écriture dans le registre, cette fonction
renvoie une erreur. Dans le cas contraire, elle sort
proprement, sans retourner de messages.  

#### Invoke()
Utilisez la fonction `Invoke` pour
appeler des fonctions de code blockchain qui effectueront un "réel
travail" sur le réseau de blockchain. Les fonctions Invoke
sont capturées en tant que transactions, qui sont regroupées par
blocs pour une écriture dans le registre. La mise à jour du
registre est effectuée par l'appel de votre code blockchain. La
structure de la fonction `Invoke` est simple ; elle
reçoit une fonction et un tableau d'arguments. En fonction de la
fonction transmise par le paramètre de fonction dans la demande
d'appel, la fonction `Invoke` appelle une
fonction d'aide ou retourne une erreur.

Dans votre fichier `chaincode_start.go`,
modifiez la fonction `Invoke` de sorte qu'elle
appelle une fonction d'écriture générique.

```go
func (t *SimpleChaincode) Invoke(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
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

Le code recherche maintenant
`write`, de façon à ajouter la fonction d'écriture
à votre fichier `chaincode_start.go` :

```go
func (t *SimpleChaincode) write(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
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
La fonction `Query` est appelée pour
interroger
l'état votre code blockchain, et elle n'ajoute pas de blocs à la
chaîne (registre). Seules les fonctions deploy et invoke ajoutent de nouveaux blocs. Utilisez la valeur `Query` pour lire la valeur des paires clé/valeur de l'état de votre code blockchain.

Dans votre fichier `chaincode_start.go`, modifiez la fonction `Query` afin qu'elle appelle une fonction de lecture générique :

```go
func (t *SimpleChaincode) Query(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

Le code recherche maintenant `read`, afin
d'ajouter la fonction 'read' dans votre fichier
`chaincode_start.go` :

```go
func (t *SimpleChaincode) read(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
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

Cette fonction `read` utilise `GetState`, lequel est le complément de `PutState`. Cette fonction shim prend un seul argument de chaîne: nom
de la clé à extraire. Ensuite, cette fonction retourne la valeur, sous la forme d'un tableau d'octets, vers `Query`, lequel à son tour l'envoie au gestionnaire REST.

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
  - Remplissez la zone `Valeur` à l'aide de contenu JSON qui spécifie une valeur `enrollID` et `enrollSecret' de vos données d'identification :

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
1. Développez la section `POST/chaîne codée`.
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
  Le *Corps de la réponse" doit être similaire à l'exemple suivant :

  ![Exemple de requête](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Corps de réponse de l'exemple de requête")

  La valeur de `hello_world` est "hi there", laquelle a été définie par le corps de votre précédent appel de déploiement.

#### Invoke (Appeler)
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
  Le *Corps de la réponse" doit être similaire à l'exemple suivant :

  ![Exemple d'appel](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Corps de réponse de l'exemple d'appel")

  Réexécutez la requête ci-dessus ; vous devez obtenir la réponse suivante :

  ![Exemple Query2](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Réponse de l'exemple d'appel")

Vous venez d'écrire du code blockchain de base.  

<br>
## Conditions requises pour la démonstration
{: #requirements}

Les éléments prérequis ci-après, inclus avec votre service
Bluemix, sont nécessaire pour l'exécution des applications de
démonstration Marbles,
Commercial Paper et Car Lease. Votre environnement Bluemix clone Hyperledger pour fournir ces dépendances :

- ID Bluemix https://console.ng.bluemix.net/ (requis pour créer votre réseau IBM Blockchain et fournir des données d'identification de service pour les homologues et l'autorité de certification)
- Node.js 0.12.0+ et npm v2+
- Environnement Golang (requis uniquement pour générer votre propre code blockchain)

Les démos exigent également un niveau de compétence avec
Node.js et le
module express. Vous devez également avoir une compréhension conceptuelle des termes 'code blockchain', 'registre' et 'homologue' dans le contexte d'une chaîne de blocs (voir le [Glossaire Hyperledger Fabric](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md)).  

<br>
## Démo Marbles (Billes)
{: #marbles}

L'application Marbles permet de démontrer un transfert d'actifs simple entre deux parties. Elle est conçue pour tester le logiciel SDK JavaScript, orienter son développement et aider les développeurs à se familiariser avec le logiciel SDK et le code blockchain.

Découvrez les [Tutoriels Marbles](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) pour en savoir plus sur les interactions entre l'application Web, le logiciel SDK et le code blockchain. Si vous connaissez déjà le code blockchain et IBM Blockchain, vous pouvez [déployer manuellement](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) la démo dans Bluemix, ou bien cliquer sur le bouton Déployer dans Bluemix pour utiliser l'application Web :
  
[![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Démo Commercial Paper (Document commercial)
{: #commercialpaper}

L'application Commercial Paper permet de démontrer comment un réseau de commerce de papier commercial peut être implémenté à l'aide d'IBM Blockchain. La démo Commercial Paper explore un réseau de blockchain privé, sur lequel les participants disposent de rôles qui leur sont affectés et des niveaux d'accès correspondants. Consultez le [Readme Commercial Paper](https://github.com/IBM-Blockchain/cp-web#readme) pour en savoir plus sur les composants de cette démo, ou procédez à un déploiement dans Bluemix immédiat afin de voir le réseau de commerce en action :   
[![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Démo Car Lease (Location de voiture)
{: #carlease}

L'application Car Lease permet de démontrer le cycle de vie d'un véhicule, de sa fabrication à la mise à la casse, après être passé entre les mains de plusieurs propriétaires. La démo utilise Node.js pour la programmation côté serveur, et Golang pour l'exécution du code blockchain sur le réseau IBM Blockchain. Elle comporte deux instances du code blockchain : la première définit les règles relatives aux transactions de véhicule et la deuxième consigne toutes les transactions du véhicule tout au long de son cycle de vie. Les deux programmes de code blockchain utilisent des objets JSON pour le stockage des données. Consultez le [Readme Car Lease](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) pour en savoir plus sur l'architecture de l'application et les attributs de véhicule associés à cette démo, ou bien déployez la démo immédiatement dans Bluemix :
  
[![Déployer dans Bluemix ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>

<!-- comment out - moving to separate file for now jh
## Non-deterministic chaincode
{: #ndcc}

IBM Blockchain networks support deterministic chaincode only. Using non-deterministic chaincode is not supported, and will cause severe errors, on any blockchain network.

**Non-deterministic chaincode** is any chaincode that does **not** result in the same appended value, over time and across nodes, on the blockchain ledger. By contrast, **deterministic chaincode** always produces the same appended value, over time and across nodes, on the blockchain ledger.

### Deterministic chaincode example
An **invoke** transaction that always increments the value of a variable by one is deterministic, because the result is always the same, on every node, without variance. Whenever this transaction is run against a fixed value of five, for example, the appended value is always six, on every node, every time. The network outcome for deterministic chaincode is no divergence in the blockchain; the copy of the ledger on each node always indicates (after syncing) that the value is one greater than the previous invocation.

### Non-deterministic chaincode example
An **invoke** transaction that increments the value of a blockchain variable with the number of elapsed seconds since the start of the day (00:00) is non-deterministic, because over time the value will vary across nodes. Each time this transaction is run against a fixed value of five, for example, the appended value diverges across nodes (with rare exceptions), because the number of elapsed seconds since 00:00 will inevitably vary. The network outcome for this non-deterministic chaincode is divergent blockchains; all nodes will not agree on the value of five + the number of elapsed seconds since 00:00.

### Randomness
Chaincode must exhibit no randomness in the appended values, over time and across nodes. Any randomness produces divergent blockchains across nodes, which must then be resolved by the network. To avoid randomness, you must ensure that no parallel chaincode can affect the input value from invocation chaincode. For example, do not run any **query** transactions in parallel with **invoke** transactions, because parallel queries could produce variance in the invocation values across nodes.

### Using a global variable
Using a global or instance variable to store a value that was retrieved from the ledger, or to set a value on the ledger, can lead to non-determinism. Chaincode should not rely on global or instance variables that will not retain their state across restarts of a chaincode container. The following is an example that uses a global variable; the value of `key`, which is written to the ledger via the `stub.PutState` function, is derived from a global variable:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iterating over a map type
Iteration over a map type can lead to non-determinism, because order is not deterministic in the Go programming language. The following is an example of iteration over the map named `columnTypes`:

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

-->


<!-- ## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples. -->
