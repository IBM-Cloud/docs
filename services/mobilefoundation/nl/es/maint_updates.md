---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mantenimiento y actualizaciones
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} suministra un {{site.data.keyword.mfserver_short_notm}} <!--on {{site.data.keyword.containerlong}} as a container group-->. Las actualizaciones del servidor de {{site.data.keyword.mobilefoundation_short}} se notifican a los usuarios. Puede actualizar el servidor de {{site.data.keyword.mobilefoundation_short}} cuando le convenga.
{:shortdesc}

## Estrategia de mantenimiento
{: #maintupdate_strategy_mf}

Cuando haya una actualización de {{site.data.keyword.mobilefoundation_short}}, se notificará su disponibilidad al usuario.  Se mostrará una notificación en el panel de control de la instancia del servicio. El usuario puede decidir aplicar la actualización a {{site.data.keyword.mobilefoundation_short}} durante la ventana de mantenimiento que considere.

La actualización de servicio de {{site.data.keyword.mobilefoundation_short}} estará disponible cuando se actualice uno de los componentes siguientes.

* {{site.data.keyword.mfserver_short_notm}}.
* La versión subyacente de Liberty.
* La versión subyacente de Java Developer Kit.


## Aplicación de las actualizaciones
{: #apply_update_mf}

La actualización de {{site.data.keyword.mobilefoundation_short}} se puede aplicar pulsando **Recrear**.

Al aplicar la actualización, la versión del servidor, que se muestra en {{site.data.keyword.mfp_oc_short_notm}}, se modificará y pasará a indicarse la versión de la actualización del servidor.

**Nota:**
* Los usuarios no pueden aplicar sus propios arreglos y actualizaciones a su instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.
* Consulte [Recreación del servidor en el plan Developer](c_using_mfs_p1.html#recreate_mobilefoundation_p1) y [Recreación del servidor en el plan Professional 1 Application](c_using_mfs_p2.html#recreate_mobilefoundation_p2) para conocer la diferencia de comportamiento en los planes cuando se pulsa **Recrear**.
