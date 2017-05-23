---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Git Repos e Issue Tracking (Beta)
{: #git_working}

Colabore con su equipo y gestione su código fuente con un repositorio Git (repositorio) y un rastreador de problemas alojado en IBM que se basa en [GitLab Community Edition ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://about.gitlab.com/){:new_window}.
{: shortdesc}

La integración de la herramienta Git Repos and Issue Tracking permite a los equipos gestionar código y colaborar de varias formas:
   * Gestionar repositorios Git a través de controles de acceso que mantienen el código seguro
   * Revisar el código y mejorar la colaboración mediante solicitudes de fusión
   * Hacer un seguimiento de problemas y compartir ideas mediante el rastreador de problemas
   * Documentar proyectos en el sistema de wiki

**Nota:** Dado que esta integración de herramientas se basa en GitLab Community Edition y está alojada en IBM en Bluemix, algunas opciones de GitLab no están disponibles. Por ejemplo, Delivery Pipeline proporciona integración continua y entrega continua para Bluemix; por lo tanto, las funciones de integración continua de GitLab no reciben soporte. Además, las funciones de administración no están disponibles las gestiona IBM.

## Límites en el tamaño de archivos y repositorios
{: #git_limits}

Los archivos están estrictamente limitados a 100 MB. El límite recomendado de tamaño de repositorios es 1 GB. Si el repositorio supera 1 GB, es posible que reciba un mensaje de correo electrónico con una solicitud para reducir el tamaño del repositorio.

## Utilización de Git Repos and Issue Tracking localmente
{: #git_authentication}

Puede acceder localmente a los repositorios Git almacenados en Git Repos and Issue Tracking. Para ver instrucciones sobre cómo configurar Git localmente, consulte [Empezar a utilizar Git en la línea de mandatos![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}.

### Creación de una señal de acceso personal o una clave SSH para la autenticación  
Para realizar operaciones Git remotas, como `clone` o `push`, desde su repositorio local de Git, debe utilizar una señal de acceso personal o una clave SSH para autenticarse con GitLab.

* Para configurar una señal de acceso personal, consulte [Señales de acceso personales ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}.
* Para configurar una clave SSH, consulte [SSH ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git.ng.bluemix.net/help/ssh/README){:new_window} o [Cómo crear claves SSH ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}. Para acceder a los repositorios con autenticación SSH es posible que se requiera cierta configuración adicional para proxies y cortafuegos.
