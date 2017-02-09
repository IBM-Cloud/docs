---

copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Plug-in de igualdad de red privada para el Bluemix CLI
{: #private_network_cli}

Utilice la interfaz de línea de mandatos (CLI) de igualdad de red privada para configurar y gestionar la igualdad de red privada entre dos espacios de {{site.data.keyword.Bluemix}}. La igualdad de red privada está soportada para IBM Containers (contenedores de Docker). Los espacios de Bluemix se pueden localizar en distintas zonas de disponibilidad en la misma región o se pueden localizar en las distintas regiones. El plug-in de la CLI de igualdad de red privada está disponible para su uso con el plug-in del Bluemix CLI.

El plug-in de la CLI de igualdad de red privada está disponible para los sistemas operativos Windows, MAC y Linux. Asegúrese de utilizar el plug-in aplicable a su caso.

Antes de empezar, cree los espacios de Bluemix. Asegúrese de que cada contenedor de un espacio tenga una dirección IP desde una red distinta. Para obtener detalles, consulte [Utilización de su propia dirección IP privada](https://www.{DomainName}/docs/containers/container_security_network.html#container_cli_ips_byoip)

**Nota:** después de utilizar la igualdad de red privada con un espacio de Bluemix, si necesita suprimir el espacio, suprima en primer lugar las conexiones de la igualdad de red privada en dicho espacio.

Para empezar, instale el IBM Bluemix CLI. Consulte
[Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html) para obtener más información.

## Instale el plug-in de la CLI de igualdad de red privada

**Nota**: si tiene una versión anterior del plug-in que se instala, tendrá que desinstalarla. Utilice el mandato siguiente para desinstalar el plug-in:

```
bluemix plugin uninstall private-network-peering
```
### Instalar localmente
Descargue el plug-in de igualdad de red privada para la plataforma desde [Repositorio de plug-ins de IBM Bluemix CLI](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins).

Instale el plug-in de igualdad de red privada utilizando el mandato siguiente:

**Nota**: pase a la ubicación del plug-in o especifique la vía de acceso a la ubicación del plug-in.

* Para Microsoft Windows OS:

```
bluemix plugin install private-network-peering-windows-amd64.exe
```

* Para Apple MAC OS:

```
bluemix plugin install private-network-peering-darwin-amd64
```

* Para Linux OS:

```
bluemix plugin install private-network-peering-linux-amd64
```

**Nota**: mientras esté instalando el plug-in para Linux OS, si ve un mensaje de error que muestra que el permiso está denegado, ejecute el siguiente mandato y cambie los permisos:

```
chmod a+x ./private-network-peering-linux-amd64
```

### Instalar desde el repositorio de Bluemix

Siga estos pasos para instalar el plug-in desde el repositorio de Bluemix:

1. Añada el punto final de registro del plug-in de Bluemix:
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```

2. Ejecute el mandato siguiente:

	```
	bluemix plugin install private-network-peering -r bluemix-bx
	```

## Lista de mandatos de igualdad de red privada
Se da soporte a los mandatos siguientes. Utilice el mandato `bluemix network` para ver la lista de mandatos disponibles:

| Mandato     | Descripción                                    |
|-------------|------------------------------------------------|
| pnp-routers | Lista todos los direccionadores disponibles para la interconexión        |
| pnp-create  | Crea una conexión de igualdad de red privada   |
| pnp-delete  | Suprime una conexión de igualdad de red privada   |
| pnp-show    | Lista todas las conexiones de igualdad de red privada  |
{: caption="Table 1. Private network peering commands" caption-side="top"}


### Utilización del mandato
Para ver la información de ayuda para los mandatos, ejecute: `bluemix network [command] -h`.

#### Listar todos los direccionadores disponibles para la interconexión
```
bluemix network pnp-routers [--verbose (o -v)]
```

#####Parámetros opcionales
{: #op1}

* **--verbose (o -v)** (distintivo): Ver la información de red detallada sobre cada direccionador.

######Ejemplo de mandato
{: #ex1}

Para ver la información de red sobre todos los direccionadores:

	$ bluemix network pnp-routers
	Listando direccionadores disponibles...
	OK

	IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3


Para ver la información de red detallada sobre todos los direccionadores:


	$ bluemix network pnp-routers -v
	Listando direccionadores disponibles...
	OK

	Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
	FIELD          VALUE
	IP             129.41.234.246
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo1
	Networks       172.31.0.0/16

	Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
	FIELD          VALUE
	IP             129.41.237.172
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo2
	Networks       172.25.0.0/16

	...


#### Crear una conexión de igualdad de red privada utilizando las direcciones IP
```
bluemix network pnp-create <ip_direccionador> <ip_direccionador> <nombre>
```

#####Parámetros
{: #p1}

* **ip_direccionador**: direcciones IP de los dos direccionadores que desea conectar. Puede encontrar las direcciones IP utilizando el mandato: `bluemix network pnp-routers`
* **nombre**: nombre de la conexión de igualdad de red privada.

######Ejemplo de mandato
{: #ex2}

	$ bluemix network pnp-create 129.41.234.246 129.41.237.172 demo
	Creando conexión de igualdad de red privada 'demo'...
	Conectando 'default-router(129.41.234.246)' y 'default-router(129.41.237.172)'...
	OK

	Conexión de igualdad de red privada 'demo' creada.


####Crear una conexión de igualdad de red privada utilizando el nombre de la conexión

```
bluemix network pnp-create -i <nombre>
```

#####Parámetros
{: #p2}

* **--interactive (-i)** (distintivo): Modalidad interactiva para seleccionar direccionadores.
* **nombre**: nombre de la conexión de igualdad de red privada.

######Ejemplo de mandato
{: #ex3}

	$ bluemix network pnp-create -i demo
	Creando la conexión de igualdad de red privada 'demo'...
	Lista de direccionadores disponibles (seleccionar DOS para la interconexión):

	#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
	1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

	Seleccionar el primer direccionador para la interconexión> 1
	Seleccionar el segundo direccionador para la interconexión> 2

	Conectando 'default-router(129.41.234.246)' y 'default-router(129.41.237.172)'...
	OK

	Conexión de igualdad de red privada 'demo' creada.


#### Listar todas las conexiones de igualdad de red privada
```
bluemix network pnp-show [--verbose (o -v)]
```

#####Parámetros opcionales
{: #op2}

* **--verbose (o -v)** (distintivo): Ver la información de red detallada sobre cada direccionador.

######Ejemplo de mandato
{: #ex4}

Ver información básica:

	$ bluemix network pnp-show
	Listando conexiones de igualdad de red privada...
	OK

	ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

Ver información detallada:

	$ bluemix network pnp-show -v
	Listando conexiones de igualdad de red privada...
	OK

	Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
	FIELD              VALUE
	Name               demo
	Status             Active
	Router1 Name       default-router
	Router1 IP         129.41.234.246
	Router1 Networks   172.31.0.0/16
	Router2 Name       default-router
	Router2 IP         129.41.237.172
	Router2 Networks   172.25.0.0/16


#### Suprimir una conexión de igualdad de red privada
```
bluemix network pnp-delete [--force (o -f)] <id_conexión>
```
#####Parámetros
{: #p3}
* **id_conexión**: Uno o varios ID de conexión separados por una coma.

#####Parámetros opcionales
{: #op3}

* **--force (o -f)** (distintivo): Suprime la conexión sin solicitar la confirmación.

######Ejemplo de mandato:
{: #ex5}

Suprimir una conexión:

	$ bluemix network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Aviso: las conexiones suprimidas no se podrán restaurar.
	¿Está seguro de que desea suprimir la conexión? (sí/no)> sí

	Suprimiendo la conexión de igualdad de red privada '17b1c3c7-d614-4fc5-9afe-961e38ee79f8'...
	OK

	Conexión de igualdad de red privada '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' suprimida.


Suprimir varias conexiones:

```
bluemix network pnp-delete [-f] <id_conexión>,<id_conexión>,<id_conexión>
```
