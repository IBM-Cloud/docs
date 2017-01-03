---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Resolución de problemas
{: #errors}
Última actualización: 07 de diciembre de 2016
{: .last-updated}

Utilice esta sección como guía para la resolución de problemas comunes de {{site.data.keyword.mobilepushshort}}.


### Se ha producido un error de servidor interno. Póngase en contacto con el administrador. (Código de error interno: PUSHD102E)

**Explicación**: Este error puede producirse si ha creado una instancia de push antes de noviembre de 2015.  

**Respuesta del usuario**: Para resolver el problema, suprima la instancia push y cree una nueva. Tenga en cuenta que cuando suprima la instancia de push, sus etiquetas no se conservarán.


### UnauthorizedRegistration

**Explicación**: Chrome Web Push no funciona con claves de Firebase Cloud Messaging (FCM). Si no puede recibir notificaciones push web en Chrome después de pasar de FCM a GCM, se debe a que el sitio web estaba configurado anteriormente para trabajar con el proyecto GCM y el nuevo proyecto se ha creado en FCM. El navegador Chrome coloca en la memoria caché las señales generadas que identifican el navegador.

**Respuesta del usuario**: Para solucionar este problema, elimine las cookies y restablezca los permisos del navegador. Este solicitará permisos para habilitar las notificaciones push. 

