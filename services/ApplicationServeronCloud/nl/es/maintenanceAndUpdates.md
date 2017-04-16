---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Mantenimiento y actualizaciones de las VM
{: #maintenance_and_vm_updates}

## Estrategia de mantenimiento
{: #maintenance_strategy}

IBM WebSphere Application Server for Bluemix se actualiza de forma periódica, garantizando que las nuevas instancias de servicio se creen con los fixpacks y parches actuales. La nube ofrece de forma rápida y sencilla nuevas instancias de servicio para la gestión de middleware. Se espera que muchos consumidores actualicen a una nueva instancia de servicio cuando deseen aplicar mantenimiento. Para dichos consumidores que desean retener instancias de servicio a largo plazo, hay repositorios de mantenimiento disponibles para el
middleware y el invitado operativo subyacente. Estos repositorios permiten a los usuarios realizar el mantenimiento de su entorno del mismo modo que lo harían de forma local.

## Actualizaciones de VM

En el siguiente apartado se describe cómo aplica cambios del sistema en la máquina virtual.

Puede actualizar su VM del mismo modo que actualiza cualquier otro sistema RHEL normal. Mediante el gestor de paquetes "Yum" de Red Hat, puede instalar, actualizar, desinstalar y realizar muchas otras acciones con sus paquetes.

El sistema está configurado para recibir estas actualizaciones del IBM Red Hat Satellite Server. Este satélite proporciona paquetes seguros de la red de Red Hat a través del gestor de paquetes Yum.

Satellite Server está gestionado por IBM y no puede modificarse desde el sistema.

Para obtener más información, consulte [Aplicación de actualizaciones de paquetes en Red Hat Enterprise Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} y [Yum, el gestor de paquetes de Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}.
