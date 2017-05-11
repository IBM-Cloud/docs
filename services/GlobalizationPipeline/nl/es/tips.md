---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Consejos sobre traducción automática
{: #globalizationpipeline_tips}

La traducción automática puede ser eficaz en proporcionar una aproximación al significado del texto de origen. Sin embargo, la calidad y la utilidad de la traducción automática varía en gran medida en función del idioma de destino y del motor de traducción automática que utilice. Uno de los factores clave en la calidad de la traducción automática es la calidad de la fuente en sí misma. Es posible que no se traduzca de forma precisa el texto de origen que esté cargado con coloquialismos, frases incompletas, puntuación incorrecta y palabras y frases ambiguas.
{:shortdesc}

Al crear su interfaz de usuario de la app {{site.data.keyword.Bluemix_notm}}, siga algunas directrices de escritura básicas para mejorar no solo el idioma de origen, sino también la calidad de la traducción automática.

Además, solicite a un hablante nativo del idioma que revise y edite la traducción automática. Además, recopile comentarios de los usuarios de la app; son quizá los mejores jueces de la eficacia y precisión de la traducción.

## Consejos sobre el estilo de escritura
{: #writingstyletips}

* **Utilice frases sencillas de longitud corta a media (de 5 a 20 palabras):** Los motores de traducción automática con frecuencia tienen dificultades para traducir las frases compuestas y complejas, incluidas las frases con signos de punto y coma. Proporcione una idea por frase. Si una frase contiene dos verbos activos para proporcionar dos ideas, divida la frase en dos frases. Los motores de traducción automática también tienen problemas para analizar las frases que son demasiado cortas como para proporcionar suficiente contexto.
* **Evite las frases:** Utilice frases completas siempre que sea posible. Las frases son aceptables para cabeceras y subcabeceras, pero evite el estilo telegráfico de escritura de titulares. Utilice frases completas para introducir listas.
* **Evite expresiones idiomáticas, el argot y la jerga:** Sustituya frases para las que no tiene sentido una traducción literal. Por ejemplo, sustituya "on the fly" por "dynamic", "on the other hand" por "alternatively" y "keep in mind" por "remember".
* **Evite el humor, el sarcasmo, los coloquialismos, los emoticonos y las metáforas.**
* **Sea sucinto:** Elimine el texto innecesario y las redundancias. Por ejemplo, sustituya "It is useful to remember that large values increase the response time" por "Large values increase the response time".
* **Evite frases que se hayan escrito completamente en mayúsculas:** Las mayúsculas proporcionan claves para el significado de la palabra. Por ejemplo, si escribe "BILL", el motor de traducción automática no podrá determinar si quería decir el nombre "Bill" o la palabra "bill".
* **Evite palabras ambiguas:** Por ejemplo, no utilice "once" en lugar de "after" o "when". No utilice "while" en lugar de "although" o "whereas". No utilice "may" cuando quiere decir "might" o "can".
* **Evite pronombres:** Repita nombres o sintagmas nominales cuando sea posible. El pronombre "it" es particularmente problemático.
* **Escriba en voz activa cuando sea posible:** Las frases activas suelen ser más claras que las frases pasivas. Por ejemplo, escriba "The utility determines which path is most efficient" en lugar de "The most efficient path is determined".
* **Evite información específica culturalmente.**
* **Tenga en cuenta que los motores de traducción automática pueden traducir nombres de producto:** Muchos países conservan el nombre de producto original en inglés, pero los motores de traducción automática pueden intentar traducir nombres de producto, especialmente si los nombres contienen palabras reales. Antes de utilizar un nombre de producto, pruebe su traducción. Si encuentra problemas, modifique el texto o la traducción en consonancia.
* **Asegúrese de que toda la información se escribe en un idioma:** Los motores de traducción automática podrían presuponer que toda la información está en un solo idioma, incluso si el texto incluye una o dos palabras en otro idioma. Por ejemplo, si el texto incluye "en route" (francés), el motor de traducción automática seguirá intentando traducir dichas palabras como si fueran palabras en inglés.
* **Evite eslóganes de marketing:** Los eslóganes de marketing se basan a menudo en la comprensión de una audiencia de una determinada cultura. Evite estos tipos de eslóganes porque es probable que los motores de traducción automática tengan problemas al traducirlos correctamente.
* **Asegúrese de que los elementos de la lista estén completos y paralelos:** Por ejemplo, si un elemento empieza con un verbo, asegúrese de que todos los elementos comiencen por un verbo.
* **Evite utilizar please y thank you:** Estas palabras pueden parecer fuera de lugar o incluso paternalistas en algunas culturas.
* **Escriba las fechas en un formato no numérico:** Los formatos de fecha numéricos varían en función del país. Escriba el nombre del mes, el día y el año. Por ejemplo, utilice 1 de septiembre de 2003 en lugar de 9/01/03, lo que se puede interpretar como 1 de septiembre de 2003 o como 9 de enero de 2003.

## Consejos de gramática
{: #grammartips}

* **Utilice la puntuación correcta:** La omisión de puntos y comas puede hacer que un motor de traducción automática malinterprete la información.
* **Asegúrese de que los sujetos concuerdan con sus verbos:** Asegúrese de que los sujetos plurales tienen verbos en plural y que los sujetos singulares tienen verbos en singular.
* **Utilice verbos en tiempo presente simple:** Muchos otros idiomas no tienen calidades de verbo en inglés, como por ejemplo la voz y el tiempo. Evite los tiempos futuro y pasado siempre que sea posible. Por ejemplo, puede volver a escribir "If you run this program, DB2® will return an error message" como "If you run this program, DB2 returns an error message".
* **Asegúrese de que los pronombres concuerdan con sus antecedentes:** Por ejemplo, "A user should first determine their tasks" debería reescribirse como "Users should first determine their tasks"..
* **Evite los modificadores pendientes:** Coloque los modificadores correctamente, de forma que modifiquen el nombre que se pretende. Por ejemplo, "While typing in commands, the program does not send any messages to you" se puede volver a escribir como "While typing in commands, you do not receive any messages from the program".
* **Evite dobles negaciones:** Por ejemplo, "Do not omit the date" se puede sustituir por "Include the date".
* **Evite las formas de los verbos infinitivo (escribir), participio de presente (escribiendo) y participio de pasado (escrito) al principio de las frases:** Estas formas verbales son con frecuencia ambiguas y difíciles de traducir.
* **Evite series de nombres:** Limite las frases nominales compuestas, como por ejemplo "special filter factor estimate considerations" a no más de tres palabras.
* **Evite utilizar palabras en varias categorías gramaticales:** En inglés, muchas palabras, como "default", pueden ser un nombre o un verbo. Esta estructura no es correcta en muchos otros idiomas. Sea coherente en la forma de utilizar cada palabra. Por ejemplo, utilice siempre "default" como un nombre.
* **Asegúrese de que los elementos de una frase sean paralelos:** Por ejemplo, utilice todos los nombres o todos los verbos en una lista dentro de la frase; no mezcle nombres y verbos.
* **No omita palabras necesarias:** Por ejemplo, en lugar de "The file names are displayed in uppercase characters and the file extensions in lowercase", utilice "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters". Utilice la palabra "that" para proporcionar aclaración según sea necesario. Por ejemplo, sustituya "If you determine the problem is a missing file" por "If you determine that the problem is a missing file".
* **No utilice un guión como paréntesis:** Por ejemplo, no escriba "When you get to this point - the point when all data has been loaded - you need to test the system". Sustituya guiones por comas, o reescriba la frase.
 
## Consejos de terminología
{: #terminologytips}

* **Utilice la terminología de forma coherente:** Evite utilizar varios términos para hacer referencia a lo mismo. Evite utilizar un mismo término para hacer referencia a más de una cosa.
* **Incluya explicaciones para cualquier término especializado.**
* **Evite términos que tengan distintos significados en otros entornos y contextos:** Entre estos términos se incluyen "billion", "domestic" y "foreign".
* **Utilice de forma coherente y estandarizada las mayúsculas y minúsculas, la separación silábica y la formación de palabras:** Por ejemplo, escriba "fix pack" en lugar de "fix pack".
* **Utilice las minúsculas, a menos que el término sea un nombre propio.**
* **Evite símbolos especiales:** Si necesita utilizar el símbolo #, no haga referencia a él como el símbolo de almohadilla. En su lugar, llámelo el símbolo de número (#).
* **Evite las abreviaturas:** Los motores de traducción automática pueden reconocer abreviaturas comunes, como IBM y DB2, pero no las reconocen todas. Evite las abreviaturas cuando sea posible. No utilice abreviaturas en latín, como por ejemplo "i.e." y "etc.".

## Consejos de puntuación
{: #punctuationtips}

* **Evite utilizar una barra inclinada para indicar "and or":** Vuelva a escribir la frase para indicar el significado exacto. Por ejemplo, puede reescribir "You can view the draft copy and/or the review copy" como "You can view the draft copy, the review copy, or both".
* **No indique plurales añadiendo (s):** Utilice la frase "one or more" o utilice solo la forma plural.
* **No utilice un carácter &amp;amp; (&) para indicar y.**
* **Utilice comas para separar elementos en una lista dentro de la frase, y coloque una coma antes de la conjunción en la lista:** Por ejemplo, "Select your company, location, and profession".

## Consejos de ortografía
{: #spellingtips}

* **Compruebe la ortografía:** Las palabras mal escritas pueden provocar errores de traducción. Compruebe siempre en busca de errores tipográficos.
* **Utilice ortografía coherente:** Asegúrese de que los términos, los acrónimos y los nombres propios se escriban siempre de la misma manera, incluyendo el uso de letras en mayúscula y minúscula.

## Consejos de presentación visual
{: #visualtips}

* **Evite el texto en gráficos.**
* **Evite utilizar el formato para enfatizar.**

