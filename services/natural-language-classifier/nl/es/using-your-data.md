---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Utilización de sus propios datos
Después de crear, entrenar y consultar un {{site.data.keyword.nlclassifierfull}} con los datos del ejemplo de [Cómo empezar](/doc/natural-language-classifier/getting-started.html), deseará crear un clasificador que trabaje con sus propios datos. Debe ensamblar y proporcionar estos datos de entrenamiento.
{:shortdesc}

## Estructura de los datos de entrenamiento
Puede proporcionar los datos para entrenar el servicio {{site.data.keyword.nlclassifiershort}} en formato de valores separador por comas (CSV). 

En el formato CSV, una fila del archivo representa un registro del ejemplo. Cada registro tiene dos o más columnas. La primera columna es el texto representativo que hay que clasificar. Las columnas adicionales son clases que se aplican a dicho texto. En la imagen siguiente se muestra un archivo CSV que tiene cuatro registros. Cada registro del ejemplo incluye la entrada de texto y una clase, separados por una coma: 

![](images/train_sample.png)

Este es un pequeño ejemplo. Los datos de entrenamiento correctos incluyen muchos más registros. 

Descargue el archivo <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> para ver un archivo de datos de entrenamiento de ejemplo. 

### Metadatos adicionales

Además del texto y las clases, la solicitud para crear un clasificador incluye información adicional. Los metadatos identifican el idioma de los datos; también puede incluir un nombre para ayudarle a identificar el clasificador. 

### Formato del archivo de datos de entrenamiento CSV

Asegúrese de que los datos de entrenamiento CSV cumplen los siguientes requisitos de formato: 

- Los datos deben tener la codificación UTF-8. 
- Separe los valores de texto y cada valor de clase por una coma como delimitador. Cada registro (fila) debe terminar con un carácter de fin de línea, que es un carácter especial o secuencia de caracteres que indica el fin de línea. 
- Cada registro debe tener un valor de texto y al menos un valor de clase. 
- Los valores de clase no pueden incluir tabuladores ni caracteres de fin de línea. 
- Los valores de texto no pueden contener tabuladores ni nuevas líneas sin manejo especial. Para conservar los tabuladores o nuevas líneas, utilice un carácter de espacio del tabulador, `\t`, y uno de líneas nuevas, `\r`, `\n` o `\r\n`.

	Por ejemplo, `Texto de ejemplo\tcon un tabulador` es válido, pero `Texto de ejemplo    con un tabulador` no es válido.
- Especifique siempre los valores de texto o de clase entre comillas dobles en los datos de entrenamiento cuando incluyan los siguientes caracteres: 
	- Comas: `"Texto de ejemplo, con coma"`.
	- Comillas dobles. Además, si hay comillas dobles hay que especificar el carácter de espacio con comillas dobles: `"Texto de ejemplo con ""comillas"""`.

## Limitaciones de tamaño
Hay límites mínimo y máximo para los datos de entrenamiento: 

-   Los datos de entrenamiento deben tener al menos cinco registros (filas) y no pueden superar los 15000 registros. 
-   La longitud máxima total de un valor de texto es 1024 caracteres. 

## Idiomas
Aunque el idioma predeterminado es el inglés, puede especificar el idioma de los datos de entrenamiento cuando cree el clasificador. El idioma de los datos de formación debe coincidir con el idioma del texto que tiene intención de clasificar. Para ver detalles, vea [Consulta de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/natural-language-classifier/api/v1/){:new_window}.

El clasificador admite los idiomas inglés (en), árabe (ar), francés (fr), alemán (de), japonés (ja), italiano (it), portugués de Brasil (pt) y español (es).

## Directrices para un buen entrenamiento
La API no impone las siguientes directrices. Sin embargo, el clasificador tiende a ofrecer un mejor rendimiento cuando los datos de entrenamiento las cumplen: 

- Limite la longitud del texto de entrada a menos de 60 palabras. 
- Limite el número de clases a unos cuantos cientos de clases. Es posible que se incorpore soporte para un mayor número de clases en posteriores versiones del servicio. 
- Asegúrese de que cada clase coincida con al menos 5 - 10 registros cuando cada registro de texto tiene una sola clase. Este número ofrece suficiente entrenamiento en dicha clase. 
- Evalúe la necesidad de disponer de varias clases. Hay dos motivos comunes por los que disponer de varias clases: 
	- Cuando el texto implica cierta ambigüedad, el hecho de identificar una sola clase no siempre ofrece resultados claros. 
	- Cuando los expertos interpretan el texto de distintas maneras, varias clases dan soporte a dichas interpretaciones. 

	Sin embargo, si muchos textos de los datos de entrenamiento incluyen varias clases, o si algunos textos tienen más de tres clases, es posible que tenga que definir mejor las clases. Por ejemplo, revise si las clases son jerárquicas. Si lo son, incluya el nodo hoja como la clase.
-  Incluya términos estándares con guiones cuando forman parte de los datos de entrenamiento (por ejemplo, `calidad-precio` o `inglés-español`).

	Sin embargo, no conecte palabras adyacentes para crear nuevos términos que no estén en el idioma de los datos de entrenamiento. Por ejemplo, en lugar de definir `plato-escurrido` o `con_la_cuchara`, defina las frases como palabras separadas (`plato escurrido` y `con la cuchara`) con la clase adecuada. 

## Construcción de datos de entrenamiento
El aprendizaje de máquina describe el proceso de aprender algunas propiedades a partir de un conjunto de datos y luego aplicar las propiedades a datos nuevos. El servicio {{site.data.keyword.nlclassifiershort}} sigue este proceso. Está entrenado para conectar clases predefinidas a textos de ejemplo y luego aplicar dichas clases a entradas nuevas. 

Por lo tanto, el clasificador entrenado es tan bueno como los datos de entrenamiento. Cada valor de texto de los datos debe representar los tipos de textos sobre los que desea que el clasificador realice su predicción. Cada clase que espera devolver debe estar en los datos de entrenamiento, y las clases que asocie a cada texto deben ser las correctas. 

Por ejemplo, si los textos de los datos de entrenamiento son preguntas, utilice preguntas que representen y sean las preguntas típicas que realizan sus usuarios. Puede recopilar estos textos de datos reales de los usuarios o puede utilizar textos creados por personas que sean expertas en el campo. 

Esta naturaleza representativa y precisa de los datos es importante, ya que controla todos los procesos y resultados del clasificador. Además, cuantos más registros incluya en los datos de entrenamiento, más posibilidades tiene el clasificador de encontrar una coincidencia. 
