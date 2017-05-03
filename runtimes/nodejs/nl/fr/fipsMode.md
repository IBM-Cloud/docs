---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Mode FIPS
{: #fips_mode}

Les packs de construction Nodejs versions v3.2-20160315-1257 et ultérieur prennent en charge [FIPS![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).    
{: shortdesc}

Pour utiliser un moteur de noeud activé par FIPS, affectez la valeur true à la variable d'environnement FIPS_MODE.
Par exemple :

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

Il est important de comprendre que lorsque la variable d'environnement FIPS_MODE a pour valeur true, certains modules de noeud peuvent ne pas fonctionner.  Par exemple, les **modules de noeud qui utilisent [MD5 ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/MD5) échoueront**, par exemple, [Express![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://expressjs.com/). Pour Express, le fait d'affecter la valeur false à [etag![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://expressjs.com/en/api.html) dans votre application Express peut vous permettre de contourner ce problème. Ainsi, vous pouvez introduire la commande suivante dans votre code :
```
    app.set('etag', false);
```
{: codeblock}
Pour plus d'informations, consultez cet [article (post) stackoverflow ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js).

**REMARQUE** : Les variables d'environnement [App Management](/docs/manageapps/app_mng.html) et FIPS_MODE *NE PEUVENT PAS* être utilisées en même temps.  Si la variable d'environnement BLUEMIX_APP_MGMT_ENABLE est définie et que la variable d'environnement FIPS_MODE a pour valeur true, la reconstitution de l'application échoue.

Il existe diverses méthodes permettant de vérifier l'état de FIPS_MODE :
<ul>
<li> Vous pouvez rechercher, dans les fichiers journaux de votre application, un message semblable au suivant :    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

Ce message indique qu'un moteur node.js activé par FIPS est en cours d'exécution, ce qui ne signifie pas nécessairement que FIPS est actif.
</li>

<li> Vous pouvez vérifier la valeur de **process.versions.openssl**. Par exemple :

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Si la version de SSL contient "fips", la version de SSL utilisée prend en charge FIPS.  
</li>

<li> Pour node.js version 6 ou ultérieure, vous pouvez vérifier la valeur renvoyée par crypto.fips dans du code tel que le suivant :

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Si la valeur renvoyée est 1, cela signifie que FIPS est utilisé. Notez que crypto.fips renverra *undefined* pour les versions de node.js antérieures à la version 6.
</li>
</ul>

## Nodejs v4
{: #nodejs_v4_fips}

Le tableau suivant explique le comportement de node.js V4 avec FIPS :

|                 | Résultat        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS est utilisé.
  * Les journaux contiendront le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl contiendra "fips".
* success (2)
  * FIPS n'est *PAS* utilisé.
  * Les journaux ne contiendront *PAS* le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl ne contiendra *PAS* "fips".

## Nodejs v6
{: #nodejs_v6_fips}

Pour exécuter le mode FIPS avec Node.js version 6 en plus de définir **FIPS_MODE=true**, vous devez également inclure **--enable-fips** dans votre commande start, comme dans l'exemple suivant :
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

Le tableau suivant explique le comportement de node.js V6 avec FIPS :

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS est utilisé.
  * Les journaux contiendront le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl contiendra "fips".
  * crypto.fips renverra 1 pour indiquer que FIPS est utilisé.
* success (2)
  * FIPS n'est *PAS* utilisé.
  * Les journaux contiendront le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl contiendra "fips".
  * crypto.fips renverra 0 pour indiquer que FIPS n'est *PAS* utilisé.
* failure (3)
  * FIPS n'est *PAS* utilisé.
  * Les journaux ne contiendront *PAS* le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La reconstitution échouera avec le message "ERR node: bad option: --enable-fips".
* success (4)
  * FIPS n'est *PAS* utilisé.
  * Les journaux ne contiendront *PAS* le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl ne contiendra *PAS* "fips".
  * crypto.fips renverra 0 pour indiquer que FIPS n'est *PAS* utilisé.
