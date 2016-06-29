---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Agregación de API
{: #api_aggregation}

*Última actualización: 31 de marzo de 2016*

Se pueden agregar algunas API de Insights for Weather. Puede utilizar la agregación para combinar dos o más llamadas de API
atómicas en una única solicitud HTTP.
{: shortdesc}

Una llamada de API atómica hace referencia a cualquiera de las API que definen un alias para la
agregación. Cada documento de usuario de API contiene el alias para el nombre de agregación en la sección de
formato de URL si está disponible para la agregación. Por ejemplo, la API de previsión diaria estándar
tiene un alias para la agregación de `v2fcstdaily10` que se puede utilizar para recuperar la previsión
diaria de 10 días como parte de una solicitud agregada.

La agregación tiene las limitaciones siguientes:

* El tamaño total no comprimido de respuestas para la agregación completa debe ser inferior a
1 megabyte.
* Los URL deben tener una longitud inferior a 4.096 caracteres aproximadamente (incluidos el protocolo, el
nombre de host, la vía de acceso y la serie de consulta).
* Puede agregar hasta 10 API atómicas.

**Nota:** Si la solicitud o respuesta viola alguna de estas limitaciones, recibirá una
respuesta de error con un código de estado HTTP 500 (normalmente 500 o 502, aunque se pueden devolver
otros). 

## URL de API de agregado
El URL de API agregado empieza con `/v2/aggregate/` y va seguido de alias separados por punto y coma.
Por ejemplo, para agregar la API de previsión diaria de 10 días (`v2fcstdaily10`) con observaciones actuales (`v2obscurrent`), utilice este formato: 

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## Reglas de parámetro de consulta para las API atómicas y la agregación
Se necesitan parámetros de consulta para todas las solicitudes. Los parámetros de consulta para la agregación se pasan de la misma manera que para las llamadas de API atómicas
con algunas reglas adicionales. En las secciones siguientes se describe cómo
pueden aplicarse para formar agregaciones diferentes. 

### Especificar parámetros de consulta que se aplican a todas las API atómicas

La forma más sencilla de agregación se produce cuando los parámetros de consulta se aplican a todas
las API atómicas. En este caso, los parámetros de consulta tienen el formato estándar de `?param1=value1&amp;param2=value2`.

El ejemplo siguiente aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` a la solicitud para las API atómicas `v2fcstdaily10` y `v2obscurrent`. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### Especificar qué API atómicas reciben qué parámetros de consulta

Si es necesario especificar parámetros para API atómicas específicas, los parámetros de consulta pueden utilizar la notación de posición de `?R1.param1=value1&amp;R2.param2=value2`. Este formato utiliza `param1`
para la primera API atómica y `param2` para la segunda API atómica. 

El siguiente ejemplo aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` para `v2fcstdaily10` y `geocode=44.44,50.23&amp;language=en&amp;units=e`
para `v2obscurrent`.

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### Parámetros de consulta de grupo para API atómicas específicas

Puede agrupar parámetros utilizando la notación de posición en un formato separado por comas: `?R1,R2.param1=value1&amp;param2=value2`.
Este formato utiliza `param1` para la primera y segunda API atómica y `param2` para todas las demás API atómicas. 

El siguiente ejemplo aplica `geocode=34.06,84.21&amp;language=enUS&amp;units=e` para `v2fcstdaily10` y `v2obscurrent`. Aplica `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` para
`v2loc`:

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### Solicite el mismo recurso de varias formas

Puede solicitar el mismo recurso de varias formas,
como en distintos idiomas o con una unidad de medida diferente. Con este formato, la API atómica puede repetirse en la solicitud: `/v2/aggregate/v2fcstdaily10;v2fcstdaily10` y puede utilizarse la notación de posición del parámetro para indicar en qué forma solicitar cada API: `?R1.param1=value1&amp;R2.param1=value2`. En este caso, el usuario
recibe el mismo recurso que se formatea o traduce de diferentes formas.

El siguiente ejemplo aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` a la primera aparición de `v2fcstdaily10` y `geocode=31.44,84.33&amp;language=fr&amp;units=m`
a la segunda aparición de `v2fcstdaily10`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

El siguiente ejemplo aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` a la primera aparición de `v2fcstdaily10` y `geocode=33.54,85.43&amp;language=en&amp;units=e` a la segunda aparición de `v2fcstdaily10` para recuperar varias ubicaciones para los mismos datos. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```





	years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Agregación de API
{: #api_aggregation}

*Última actualización: 31 de marzo de 2016*

Se pueden agregar algunas API de Insights for Weather. Puede utilizar la agregación para combinar dos o más llamadas de API
atómicas en una única solicitud HTTP.
{: shortdesc}

Una llamada de API atómica hace referencia a cualquiera de las API que definen un alias para la
agregación. Cada documento de usuario de API contiene el alias para el nombre de agregación en la sección de
formato de URL si está disponible para la agregación. Por ejemplo, la API de previsión diaria estándar
tiene un alias para la agregación de `v2fcstdaily10` que se puede utilizar para recuperar la previsión
diaria de 10 días como parte de una solicitud agregada.

La agregación tiene las limitaciones siguientes:

* El tamaño total no comprimido de respuestas para la agregación completa debe ser inferior a
1 megabyte.
* Los URL deben tener una longitud inferior a 4.096 caracteres aproximadamente (incluidos el protocolo, el
nombre de host, la vía de acceso y la serie de consulta).
* Puede agregar hasta 10 API atómicas.

**Nota:** Si la solicitud o respuesta viola alguna de estas limitaciones, recibirá una
respuesta de error con un código de estado HTTP 500 (normalmente 500 o 502, aunque se pueden devolver
otros). 

## URL de API de agregado
El URL de API agregado empieza con `/v2/aggregate/` y va seguido de alias separados por punto y coma.
Por ejemplo, para agregar la API de previsión diaria de 10 días (`v2fcstdaily10`) con observaciones actuales (`v2obscurrent`), utilice este formato: 

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## Reglas de parámetro de consulta para las API atómicas y la agregación
Se necesitan parámetros de consulta para todas las solicitudes. Los parámetros de consulta para la agregación se pasan de la misma manera que para las llamadas de API atómicas
con algunas reglas adicionales. En las secciones siguientes se describe cómo
pueden aplicarse para formar agregaciones diferentes. 

### Especificar parámetros de consulta que se aplican a todas las API atómicas

La forma más sencilla de agregación se produce cuando los parámetros de consulta se aplican a todas
las API atómicas. En este caso, los parámetros de consulta tienen el formato estándar de `?param1=value1&amp;param2=value2`.

El ejemplo siguiente aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` a la solicitud para las API atómicas `v2fcstdaily10` y `v2obscurrent`. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### Especificar qué API atómicas reciben qué parámetros de consulta

Si es necesario especificar parámetros para API atómicas específicas, los parámetros de consulta pueden utilizar la notación de posición de `?R1.param1=value1&amp;R2.param2=value2`. Este formato utiliza `param1`
para la primera API atómica y `param2` para la segunda API atómica. 

El siguiente ejemplo aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` para `v2fcstdaily10` y `geocode=44.44,50.23&amp;language=en&amp;units=e`
para `v2obscurrent`.

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### Parámetros de consulta de grupo para API atómicas específicas

Puede agrupar parámetros utilizando la notación de posición en un formato separado por comas: `?R1,R2.param1=value1&amp;param2=value2`.
Este formato utiliza `param1` para la primera y segunda API atómica y `param2` para todas las demás API atómicas. 

El siguiente ejemplo aplica `geocode=34.06,84.21&amp;language=enUS&amp;units=e` para `v2fcstdaily10` y `v2obscurrent`. Aplica `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` para
`v2loc`:

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### Solicite el mismo recurso de varias formas

Puede solicitar el mismo recurso de varias formas,
como en distintos idiomas o con una unidad de medida diferente. Con este formato, la API atómica puede repetirse en la solicitud: `/v2/aggregate/v2fcstdaily10;v2fcstdaily10` y puede utilizarse la notación de posición del parámetro para indicar en qué forma solicitar cada API: `?R1.param1=value1&amp;R2.param1=value2`. En este caso, el usuario
recibe el mismo recurso que se formatea o traduce de diferentes formas.

El siguiente ejemplo aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` a la primera aparición de `v2fcstdaily10` y `geocode=31.44,84.33&amp;language=fr&amp;units=m`
a la segunda aparición de `v2fcstdaily10`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

El siguiente ejemplo aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` a la primera aparición de `v2fcstdaily10` y `geocode=33.54,85.43&amp;language=en&amp;units=e` a la segunda aparición de `v2fcstdaily10` para recuperar varias ubicaciones para los mismos datos. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




