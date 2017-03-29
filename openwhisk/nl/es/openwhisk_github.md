---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Uso del paquete GitHub
{: #openwhisk_catalog_github}

El paquete `/whisk.system/github` ofrece una forma cómoda de utilizar las [API de GitHub](https://developer.github.com/).

El paquete incluye la información de entrada siguiente:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/github` | paquete | username, repository, accessToken | Interactuar con la API de GitHub |
| `/whisk.system/github/webhook` | canal de información | events, username, repository, accessToken | Activar sucesos desencadenantes en caso de actividad de GitHub |

Se recomienda la creación de un enlace de paquete con los valores de `username`, `repository` y `accessToken`.  Con enlace, no necesita especificar los valores cada vez que use la información de entrada en el paquete.

## Activación de un suceso desencadenante con actividad GitHub

La información de entrada `/whisk.system/github/webhook` configura un servicio para activar un desencadenante
cuando haya actividad en el repositorio de GitHub especificado. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario del repositorio GitHub.
- `repository`: el repositorio GitHub.
- `accessToken`: su señal de acceso personal de GitHub. Cuando [cree su
señal](https://github.com/settings/tokens), asegúrese de seleccionar los ámbitos repo:status y public_repo. Además, asegúrese de que no tiene webhooks ya definidos en su repositorio.
- `events`: el [tipo de suceso GitHub](https://developer.github.com/v3/activity/events/types/) de interés.

A continuación se muestra un ejemplo de creación de un desencadenante que se activará cada vez que haya una nueva confirmación con un
repositorio GitHub.

1. Generar una [señal de acceso personal](https://github.com/settings/tokens) de GitHub.
  
  La señal de acceso se usará en el paso siguiente.
  
2. Crear un enlace de paquete configurado para su repositorio de GitHub y con su señal de acceso.
  
  ```
  wsk package bind /whisk.system/github myGit \
    --param username myGitUser \
    --param repository myGitRepo \
    --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}
  
3. Crear un desencadenante para el tipo de suceso `push` de GitHub usando su información de entrada de `myGit/webhook`.
  
  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}
  
  Una confirmación en el repositorio GitHub utilizando `git push` provoca que el webhook active el desencadenante. Si existe una regla que coincide con el desencadenante, se invocará la acción asociada.
  La acción recibe la carga útil de webhook de GitHub como parámetro de entrada. Cada suceso de webhook de GitHub tiene un esquema JSON similar, pero es un objeto de carga útil exclusivo determinado por su tipo de suceso.
  Para obtener más información sobre el contenido de la carga útil, consulte la documentación de la API de
[Carga útil y sucesos GitHub](https://developer.github.com/v3/activity/events/types/).
  
