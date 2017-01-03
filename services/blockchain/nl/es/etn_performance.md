---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Rendimiento verificado
{: #etn_performance}
Última actualización: 07 de octubre de 2016
{: .last-updated}

IBM ha comprobado y verificado los siguientes comportamientos. Los resultados se lograron en una red de alta seguridad, salvo que se indique lo contrario:
{:shortdesc}

### Rendimiento/Estrés

Esta prueba se ha realizado para obtener las transacciones por segundo (TPS) de invocaciones y consultas bajo intervalos de prueba de corta duración, 10 minutos, e intervalos de prueba de larga duración, 60 minutos, con PBFT / Seguridad y Privacidad habilitados.  El rendimiento puede variar basándose en el entorno, el tipo de aplicación, valores de configuración/seguridad, tamaño de lotes de transacciones y otros factores.  (**Nota:** estas medidas se alcanzaron en una red distribuida multiarrendatario.)

- ejemplo 02 de código de encadenamiento
- nivel de registro: error
- número de hebra: 100
- tamaño de lote: 1000
- duración: 10 min. y 60 min.
- tipos de transacción: invocar a->b, invocar b->a, luego repetir y consultar a, consultar b, luego repetir

| Tipo de transacción | Número de iguales | Número de hebras | Duración ejecución (min) | Transacciones por segundo |
| ---------- |:-------:|:-----:|:------:|:------:|
| invocaciones   |  4  | 100 | 10 | 72  |
| invocaciones   |  4  | 100 | 60 | 66  |
| consultas   |  4  | 100 | 10 | 252 |
| consultas   |  4  | 100 | 60 | 248 |

### Capacidad de recuperación/Consenso

Esta prueba se ha realizado para asegurar la estabilidad y la capacidad de recuperación de PBFT cuando se producen errores bizantinos.  Las pruebas incluyeron:

- Detener 1 nodo y seguir enviando transacciones de despliegue, invocación y consulta.  La red sigue funcionando. Se ha realizado en cada nodo de la red.
- Detener 2 nodos, la red se detiene debido a la falta de consenso.
- Reiniciar uno de los nodos detenidos en la prueba anterior.  La red se reanuda y el nodo que ha reiniciado las sincronizaciones se sincroniza con los demás iguales de validación. Para obtener pasos detallados sobre las pruebas de PBFT, consulte el tema [Realización de pruebas de consenso y disponibilidad](etn_pbft.html).

Continúe con el tema [Prueba adicional](etn_next.html) para ver pruebas adicionales y funciones verificadas.  
