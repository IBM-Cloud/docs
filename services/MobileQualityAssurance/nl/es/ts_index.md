---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Resolución de problemas para {{site.data.keyword.mqa}} 
{: #tsmqa}
Aquí se muestran las respuestas a algunas preguntas comunes sobre el uso de {{site.data.keyword.mqa}}.
{:shortdesc}

## La compilación híbrida JavaScript falla
{: #ts_js_build_fail}

La compilación de la aplicación híbrida JavaScript {{site.data.keyword.mqa}} falla, aún cuando el SDK híbrido JavaScript&tm; para el componente IBM MobileFirst Platform Foundation esté en la aplicación y se añada el código necesario.


Al intentar ejecutar la compilación de la aplicación {{site.data.keyword.mqa}} se produce un error.
{: tsSymptoms notoc} 


1. Los componentes de SDK híbridos específicos de las plataformas Android e iOS no se instalan en el proyecto.
2. Los componentes de SDK híbridos específicos de las plataformas Android e iOS que se instalan no son compatibles con el componente de SDK JavaScript instalado.
3. El SDK Android nativo, el SDK iOS nativo o ambos se instalan, pero los componentes de SDK híbrido específicos de la plataforma Android e iOS no se instalan.
{: tsCauses notoc} 
 

Algunas sugerencias para resolver este problema incluirían los pasos siguientes:
{: tsResolve notoc}
  1.  Asegúrese de que ha instalado todos los componentes de SDK híbrido específicos de las plataformas Android e iOS, así como los SDK nativos de Android o iOS para las plataformas admitidas por su aplicación.  
  2. Asegúrese de que los componentes de SDK híbrido específicos de las plataformas Android e iOS sean de la misma versión principal que el componente JavaScript o de una versión principal superior. En la tabla siguiente se muestran algunos ejemplos:
  
| Versión del componente JavaScript | Versión del componente específico de la plataforma | ¿Es compatible? |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | Sí |
| 1.2.3 | 1.2.1 | No |
| 1.2.3 | 1.3.2 | Sí |
| 1.2.3 | 2.0.0 | No |

  3. Asegúrese de que ha instalado los componentes de SDK híbrido específicos de la plataforma Android e iOS. Si bien el SDK nativo de Android y el SDK nativo de iOS son necesarios si la aplicación se ejecuta en dichas plataformas, las aplicaciones híbridas debe tener también los componentes SDK híbridos específicos de la plataforma Android e iOS instalados para cada plataforma.

  
## No se puede abrir el análisis de opinión o distribuir apps de prueba
{: #ts_sent_fail}

No puede abrir el análisis de opinión o distribuir su app de prueba.

No puede abrir el análisis de opinión o distribuir su app de prueba porque el navegador está bloqueando las ventanas emergentes.
{: tsSymptoms notoc} 

Mobile Quality Assurance utiliza ventanas emergentes y cookies para comunicarse con el servidor de Mobile Quality Assurance.
{: tsCauses notoc}


Para establecer comunicación entre Mobile Quality Assurance y el servidor de Mobile Quality Assurance, es posible que deba configurar el navegador de forma que permita ventanas emergentes y cookies. Por ejemplo, cuando pulsa una opción de la interfaz de usuario, como la Puntuación de opinión, es posible que Mobile Quality Assurance no pueda comunicarse con el servidor. El análisis de opinión no se puede mostrar si se bloquean las ventanas emergentes y cookies. Para obtener más información sobre cómo configurar los valores del navegador, consulte la documentación específica del navegador.
{: tsResolve notoc}


## No se puede ejecutar una aplicación caducada
{: #ts_app_expired}

No puede ejecutar su aplicación Mobile Quality Assurance.

Al intentar ejecutar su aplicación Mobile Quality Assurance, se muestra el mensaje siguiente: Su aplicación ha caducado y no se puede ejecutar en este momento.
{: tsSymptoms notoc} 

La aplicación se marca como inhabilitada en la página Compilaciones de Mobile Quality Assurance.
{: tsCauses notoc}


Compruebe la página Compilaciones de Mobile Quality Assurance para asegurarse de que ninguna aplicación esté marcada como inhabilitada. Normalmente, las aplicaciones se marcan como inhabilitadas para informar a los comprobadores (mediante la propia aplicación) de que no utilicen una versión específica de la compilación. Para obtener más información sobre los valores de la página Compilaciones de Mobile Quality Assurance, consulte Gestión de compilaciones en IBM Knowledge Center.
{: tsResolve notoc}

