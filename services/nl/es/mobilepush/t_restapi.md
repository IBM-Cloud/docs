---

copyright:
 years: 2015, 2016

---

# Utilización de API REST
{: #push-api-rest}

Puede utilizar una API (application program interface, interfaz de programa de aplicaciones) REST (Representational State Transfer) para notificaciones push. También puede utilizar las API SDK y [Push](https://mobile.{DomainName}/imfpushrestapidocs/) para desarrollar más las aplicaciones de cliente.

Con
                la API REST Push, los clientes y las aplicaciones de servidor de fondo pueden acceder a las funciones Push.

- Registros de dispositivos
- Registros
- Mensajes
- Suscripciones
- Etiquetas

Para obtener la URL base para la API REST:

1. Cree una aplicación de fondo en el catálogo Bluemix® de la sección de Contenedores modelo, que enlaza automáticamente el servicio Push a esta aplicación. Si ya ha
                        creado una app de fondo, asegúrese de que enlace la app al Servicio de notificaciones
                        Push. 

1. En la página principal del panel de instrumentos de Bluemix, vaya al área **Aplicaciones** y, a continuación, pulse la app.

3. Pulse MOBILE OPTIONS. Se mostrarán la ruta y los valores GUID de la app en la parte
                        superior de la página de detalles de su app.



## Cabecera Accept Language
{: #push-api-rest-accept}

La cabecera "Accept-Language" especifica qué idioma se utilizará para los mensajes de error que resultan de la [API REST de Push](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. Se da soporte a los siguientes idiomas para ver si contienen mensajes de error:
                chino (simplificado), chino (tradicional), inglés (EE.UU.), alemán,
                francés, italiano, japonés, coreano, portugués y español.

## appSecret
{: #push-api-rest-secret}

Cuando una aplicación se enlaza a las notificaciones Push, el servicio generará un
                appSecret (una clave exclusiva) y la pasa en la cabecera de respuesta. Si está utilizando las Notificaciones Push de IBM® para la API REST de Bluemix, utilice la referencia de la API REST para obtener información sobre qué API se deben proteger. Para obtener información sobre la API REST, consulte Referencia de API REST.

La cabecera de la solicitud debe contener el appSecret. Si no, el servidor devuelve un código 401
                Unauthorized Error. Cuando se añade la Notificación
                Push a una aplicación, se creará una AppID específica. Como parte de la respuesta, obtiene una cabecera denominada appSecret que se utiliza para crear Etiquetas o para enviar mensajes. La operación sucede a través de servicios del catálogo o del
                contenedor modelo.

Para obtener el valor de appSecret:

1. Pulse el *app-name* que está enlazado al servicio
                        push.
2. Pulse el enlace **Mostrar credenciales** para visualizar el
                        appSecret (AppID).

La pantalla **Mostrar credenciales** muestra información sobre el
                AppSecret:

```
{
 "imfpush_Dev": [
   {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Filtros API REST de Push
{: #push-api-rest-filters}

Los filtros definen los criterios de búsqueda que restringen los datos devueltos de una API GET
                de Push. Aplique los filtros con el resultado de la operación Get que desee filtrar. El filtro restringe el número de entradas incluidas en el resultado. Por ejemplo, puede utilizar un filtro para buscar una etiqueta que empiece por "test". Puede
                generar un filtro utilizando la sintaxis siguiente:

**name**
El nombre del campo en el que se está aplicando el filtro.

**operator**
== (Coincidencia exacta) o =@ (Contiene subserie) que describe la coincidencia de filtro que se debe utilizar.

**expression**
Los valores que se deben incluir en el resultado.

Cuando se visualizan en una expresión una coma y una barra inclinada invertida, se deben
                poder escapar con la barra inclinada invertida.

Al utilizar varios filtros, se pueden combinar mediante la lógica AND y OR.\

- Para la lógica AND, utilice varios filtros en la consulta.
- Para la lógica OR, utilice una coma (,) dentro de la expresión de filtro.
- Para la lógica AND y OR: una única consulta puede tener la lógica AND y OR. Cada filtro se evalúa de forma individual antes de que los filtros se combinen en una
                        expresión AND.

Para la API GET del dispositivo, se da soporte a las siguientes combinaciones:
-El nombre es el campo plataforma.
- Excepto para la plataforma, el operador puede ser == o =@
- Para la plataforma, el operador debe ser ==. Si se utiliza el operador =@, el valor puede ser una subcadena.
- Si se utiliza ==, el valor debe ser una cadena de caracteres de coincidencia exacta.

Para la API GET de suscripción, se da soporte a las siguientes combinaciones:

- El nombre puede ser uno de estos campos: tagName o deviceId
- Excepto para la plataforma, el operador puede ser == o =@
- Para la plataforma, el operador debe ser ==
- Si se utiliza el operador =@, el valor puede ser una subcadena. Si se utiliza el operador ==, el valor debe ser una cadena de caracteres de coincidencia exacta.
- Para la API GET de la etiqueta, se da soporte a las siguientes combinaciones:
- El nombre puede ser uno de estos campos: “name” o “description”
- Si se utiliza el operador =@, el valor puede ser una subcadena.
- Si se utiliza ==, el valor debe ser una cadena de caracteres de coincidencia exacta.
