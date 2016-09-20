---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administración de Trajectory Pattern Analysis
{: #tp_iotdriverinsights_admin}

Última actualización: 22 de julio de 2016
{: .last-updated}

Para administrar el servicio Trajectory Pattern Analysis, utilice la consola de administración en el panel de control de {{site.data.keyword.Bluemix_notm}}. En la consola de administración se pueden configurar parámetros para Trajectory Pattern Analysis y gestionar los datos almacenados en el servicio. También puede ver la información de arrendatario y restablecer la contraseña de arrendatario.

{:shortdesc}

## Inicio de la consola de administración
{: #start-admin-console}

Para acceder a la consola de administración para el servicio Trajectory Pattern Analysis de {{site.data.keyword.iotdriverinsights_full}}

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el mosaico del  servicio {{site.data.keyword.iotdriverinsights_short}}.
2. Seleccione la vista **Gestionar** de la instancia de servicio.
Anote las credenciales de nombre de usuario y contraseña porque las necesitará más adelante. Para acceder a la consola de administración, es necesario el ID de IBM, que puede que no sea el mismo que sus credenciales de {{site.data.keyword.Bluemix_notm}}.
3. Pulse **Iniciar** y, cuando se le solicite, escriba las credenciales de ID de IBM. 
4. Pulse **INICIAR SESIÓN**. Se abre la ventana **Consola de administración**. 


## Gestión de la información de arrendatario
{: #viewtenantinfo}

Para ver la información de arrendatario, pulse **Información de arrendatario**.

### Restablecimiento de la contraseña de arrendatario
{: #resettenantpassword}

Para restablecer la contraseña de arrendatario:

1. En la ventana **Información de arrendatario**, pulse **RESTABLECER**.
2. En el cuadro de diálogo de confirmación, pulse **Aceptar**.
Se genera una nueva contraseña y se visualiza en la vista **Información de arrendatario**.
**Importante:** Asegúrese de que actualiza la contraseña en todas las aplicaciones que acceden a la API de {{site.data.keyword.iotdriverinsights_short}}.

## Configuración de parámetros de servicio
{: #configureparameters}

Los parámetros de servicio controlan cómo se analizan los datos de trayectos. Para modificar los parámetros de servicio de Trajectory Pattern Analysis:

1. Abra la vista **Parámetros**.
2. Pulse el separador **Parámetros del patrón de trayectorias** y actualice los [parámetros de análisis de patrones de trayectorias](#tp_parameters) de modo que satisfagan sus necesidades.
3. Pulse **GUARDAR**.
4. Pulse **Aceptar**.

Los valores de parámetros actualizados se aplican al próximo trabajo que se someta.

### Parámetros de umbral de soporte

La siguiente tabla describe los parámetros de umbral de soporte que puede configurar en el separador **Parámetros del patrón de trayectorias**.

|Nombre de parámetro|Descripción|Valor predeterminado|
|:--------|:--------|:-------|
|Soporte mínimo de números de trayectorias para un O/D|Los números de trayectoria de soporte absolutos mínimos que son necesarios para un patrón de O/D (Origen/Destino)|4 (debe ser mas de cero)|
|Soporte mínimo de números de trayectorias para una ruta|Los números de trayectoria de soporte absolutos mínimos que son necesarios para un patrón de rutas|2 (debe ser mas de cero)|

## Gestión de datos de resultados
{: #managedata}

Los datos de resultados generados por el análisis del servicio Trajectory Pattern Analysis se almacenan en el sistema hasta que se suprimen. 

Para suprimir los datos de resultados:

1. Pulse **Gestión de datos** > **Resultado de patrón de trayectorias**. Se visualizan los datos de resultados. 
2. Seleccione un registro y, a continuación, pulse **SUPRIMIR**.
