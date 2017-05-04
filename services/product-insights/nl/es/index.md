---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Iniciación a {{site.data.keyword.product-insights_short}}
{: #product-insights}

{{site.data.keyword.product-insights_full}} conecta con productos de software locales de IBM para crear un inventario entre productos y ofrecer detalles de las métricas de uso de cada producto. 

{:shortdesc}

El servicio {{site.data.keyword.product-insights_short}} se ejecuta en IBM Bluemix y recibe información de los productos de software locales de IBM habilitados. Esta información se muestra dentro del panel de control de la instancia de servicio.
Para utilizar el servicio, debe tener una cuenta de Bluemix y crear el servicio en una organización y un espacio. La información del producto y de uso de los productos locales habilitados se guarda de forma segura y se puede consultar en el ámbito o contexto de dicho servicio exclusivo.  

Consejo: para simplificar, inicialmente puede utilizar una sola instancia de servicio. 

Para comenzar a utilizar {{site.data.keyword.product-insights_short}}, siga estos pasos: 

1.  En el separador **Gestionar**, pulse el botón **Registrar un producto** para ver una lista de los productos admitidos y el nivel de versión necesario. Se ofrecen instrucciones para cada tipo de producto; así podrá conectar las instancias del producto local con el servicio {{site.data.keyword.product-insights_short}}. Si es necesario, actualice los productos de software locales de IBM habilitados al nivel mínimo requerido. En el caso de un producto que necesite un nivel admitido mínimo, instale el fix pack o el arreglo intermedio para permitir la integración con {{site.data.keyword.product-insights_short}}. 
2.  Conecte los productos de software locales de IBM habilitados al servicio {{site.data.keyword.product-insights_short}}. Como parte del proceso de configuración de cada producto, necesita las credenciales de servicio (es decir, los valores apikey y apihost). Encontrará las credenciales de servicio en el separador **Credenciales de servicio** del panel de control del servicio.  
3.  Después de habilitar y conectar cada instancia de producto, es posible que tenga que iniciar o reiniciar los productos y las instancias de los productos para que proporcionen información del producto y de uso al servicio {{site.data.keyword.product-insights_short}}.  

Para ver detalles sobre cómo habilitar productos, sobre el nivel de soporte mínimo necesario para cada producto y sobre cómo habilitar cada producto para integrarlo con {{site.data.keyword.product-insights_short}}, únase a la {{site.data.keyword.product-insights_full}} [Comunidad técnica](https://developer.ibm.com/product-insights/).

Para ver el inventario, seleccione **Gestionar** en el panel de control del servicio.   

* En el panel de control del servicio, los nombres de los productos que se han conectado se muestran en el panel **Productos**.  
* Para mostrar todas las instancias de productos, seleccione **Ver todo**. Para ver las instancias correspondientes a un producto, seleccione dicho producto en el panel **Productos** y sus instancias se mostrarán en el panel **Instancias**. 
* Para ver los detalles de una sola instancia de un producto, seleccione la instancia del producto en el panel **Instancias**. Se llena el panel **Detalles**. El panel **Detalles** muestra detalles de la instancia del producto y la información de uso que se ha enviado desde la instancia. 
* El separador **Uso** muestra información sobre uso del producto en formato gráfico. En función del producto, puede especificar el tipo de información que desea ver y el periodo de muestreo. 
* El separador **Detalles** muestra información sobre la instancia del producto, incluida información del producto, información del entorno e información del componente. 
* El separador **Asesor**, en su separador **Servicios**, proporciona detalles sobre servicios adicionales que pueden resultar beneficiosos en relación con la instancia del producto actual. En su separador **Actualizaciones**, proporciona información sobre el nivel de versión de la instancia del producto e indica si está actualizado. 










