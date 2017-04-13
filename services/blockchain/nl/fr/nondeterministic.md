---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# code blockchain non déterministe
{: #ndcc}


Les réseaux IBM Blockchain prennent en charge le code blockchain déterministe uniquement. L'utilisation de code blockchain non déterministe n'est pas possible et pourrait entraîner des erreurs graves sur le réseau de blockchain.
{:shortdesc}

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
