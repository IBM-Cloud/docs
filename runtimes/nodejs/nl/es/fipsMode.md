---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Modalidad FIPS
{: #fips_mode}

Las versiones del paquete de compilación de Nodejs v3.2-20160315-1257 y posteriores dan soporte a [FIPS ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards)  
{: shortdesc}

Para utilizar el motor de nodos habilitado para FIPS, establezca la variable de entorno FIPS_MODE en true.
Por ejemplo:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

Es importante comprender que cuando FIPS_MODE es true algunos módulos de nodo pueden no funcionar.  Por ejemplo, **los módulos de nodo que utilizan [MD5 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://en.wikipedia.org/wiki/MD5) fallarán**, como [Express ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://expressjs.com/).  Para Express, el establecimiento de [etag ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://expressjs.com/en/api.html) en false en la app
Expess puede ayudar a solucionar este problema. Por ejemplo, puede realizar lo siguiente en el código:
```
    app.set('etag', false);
```
{: codeblock}
Consulte esta [publicación de stackoverflow ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)
para obtener más información.

**NOTA** [App Management](/docs/manageapps/app_mng.html) y FIPS_MODE *NO* están soportados simultáneamente.  Si se ha establecido la variable de entorno BLUEMIX_APP_MGMT_ENABLE y la variable de entorno FIPS_MODE se ha establecido en true, la app no se podrá transferir.

A continuación se muestran varios métodos para comprobar el estado de FIPS_MODE:
<ul>
<li> Puede consultar los registros de la aplicación para ver si hay un mensaje parecido al siguiente:    

  <pre>
  Instalación de IBM SDK habilitado para FIPS para Node.js (4.4.3) desde la memoria caché
  </pre>
  {: codeblock}

Este mensaje indica que se está ejecutando un motor de node.js habilitado para FIPS pero no necesariamente que FIPS se está ejecutando
</li>

<li> Puede comprobar el valor de **process.versions.openssl**. Por ejemplo:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Si la versión SSL contiene "fips", la versión de SSL que está en uso da soporte a FIPS.  
</li>

<li> Para node.js versión 6 y posterior, puede comprobar el valor devuelto por crypto.fips en el código como el siguiente:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Si el valor devuelto es 1, FIPS está en uso. Tenga en cuenta que crypto.fips devolverá *undefined* para las versiones de node.js anteriores a 6.
</li>
</ul>

## Nodejs v4
{: #nodejs_v4_fips}

La siguiente tabla explica el comportamiento de node.js v4 con FIPS:

|                 | Result        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS está en uso.
  * Los registros incluirán el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl incluirá "fips".
* success (2)
  * FIPS *NO* está en uso.
  * Los registros *NO* incluirán el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl *NO* incluirá "fips".

## Nodejs v6
{: #nodejs_v6_fips}

Para ejecutar en modalidad FIPS con Node.js versión 6 además de establecer **FIPS_MODE=true**, también debe incluir
**--enable-fips** en el mandato de inicio como en el siguiente ejemplo:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

La siguiente tabla explica el comportamiento de node.js v6 con FIPS.

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS está en uso.
  * Los registros incluirán el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl incluirá "fips"
  * crypto.fips devolverá 1, lo que indica que FIPS está en uso
* success (2)
  * FIPS *NO* está en uso.
  * Los registros incluirán el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl incluirá "fips"
  * crypto.fips devolverá 0, lo que indica que FIPS *NO* está en uso
* failure (3)
  * FIPS *NO* está en uso.
  * Los registros *NO* incluirán el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * la transferencia fallará con el mensaje "ERR node: bad option: --enable-fips"
* success (4)
  * FIPS *NO* está en uso.
  * Los registros *NO* incluirán el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl *NO* incluirá "fips"
  * crypto.fips devolverá 0, lo que indica que FIPS *NO* está en uso
