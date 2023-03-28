# Insfraestrutura de datos moderna

Antes de poder construir pipelines es necesario conocer las distintas tecnologias que pueden emplearse para este lograr este objetivo, no hay una sola forma correcta de hacer el diseño, pero si se deben tener en cuenta unos conceptos y necesidades claves para estar en el estandar de esta insdustria y ejecutar las mejores pŕacticas para implementar los pipelines, entre los cuales tenemos:

- **Diversidad de fuentes de datos**  
> La mayoria de organizaciones cuentan con decenas sin cientas de fuentes de datos que alimentas sus trabajos de analisis, estas fuentes tienen varias dimensiones.


|Concepto|Definicion|
|---|---|
|Propiedad del sistema fuente|Es normal apra equipo de analsis ingestar datos desde un sistemas fuente del cual es propietario la empresa, herramientas de terceros y vendedores. Entender la propiedad del sistema fuente es importante, Unos terceros pueden limitar el acceso y como es que tu puedes acceder, dificilmente te daran acceso a su información en forma de base de datos de SQL, y muy pocos te daran un nivel de personalización de la data a la que accedes. Construir de forma interna el sistemas ofrece al equipo de analisis un nivel de personalización superior un metodos de accesos mas cómodos.|
|Interfaz de ingestion y Estructura de datos|Dejando de lado quien es el propietario de la fuente de datos, como conseguirla y en que forma se encuentra es la primera cosa a lo que un ingeniero de datos se enfrenta cuando se construye un nuevo sistema de ingestion. Las **interfaces de ingestion** que se presentan pueden ser: Bases de datos Postgres o MySQL, REST API, Apache Kafka, una red de trabajo compartida o un almacen de registros, CSV o otros archivos planos, data warehouses o data lakes, HDFS o base de datos HBase. Como **estrucrturas de datos** tenemos: JSON para REST API, data bien estructura para base de datos MySQL, JSON dentrO de las columnas de una tabla de una base de datos MySQL, data semiestructurada de registros, CSV - FWF - otros archivos planos, JSON en un archivo plano, flujo de salida de Kafka.|
|Volumen de datos|La realidad que muy pocas empresas cuentan con una cantidad de datos que tengan el valor que tienen las empresas grandes. Para este concepto es mejor relacionarlo en terminos de espectro en vez de peso.|
|Limpieza y vigencia de datos|Existe una diversidad muy grade en las fuentes de datos por lo cual la calidad de la data varia significativamente. Las caracteristicas que pueden presentar esta data de **calidad menor** pueden ser: Registros ambiguos o duplicados, Registros abandonado, Registro imcompleto o perdido, Errores al ingles tecto, Formatos inconsistentes, Mal etiquetado o ningun etiquetado de la data. **No hay forma de asegurar esta caracteristica** por lo cual es necesario trabajar bajo el siguiente enfoque si es necesario: Asume lo peor, espera lo mejor; Limpia y valida la data en el mejor sistema para hacerlo; y valida frecuentemente.|
|Latencia y Ancho de banda del sistema fuente|La necesidad de extraer frecuentemente altos volumenes de data desde los sistema es un caso común. Sin embargo, esto presneta desafios, la extración de datos por medio de los pipelines se enfrenta a limitacion de la tasa de la API, tiempo muertod e la conexión, descargas lentas, propietarios de los sistemas fuente.|


|Conceptos adicionales|Definicion|
|---|---|
|Data bien estructurada|Es la más fácil con la cual trabajar, pero normalmente esta estructurada en interes al trabajo con la web o aplicaciones|
|Data semi-estructurada|Como JSON es increibremente común y tiene la ventaja de contar pares atributos valor y objetos unos dentro de otros ( nesting objects ), pero no hay garantia de que cada objeto tenga la misma estructura.|
|Data no estructurada|Es común para algunos trabajos de analisis, modelos de NLP (Natural Language Processin) necesitan una cantidad muy grade de tecto libre para entrenar y validar, proyectos de CV (Computer Vision) requieren contenido de imagenes y videos.|

- Cloud data warehouses y data lakes
> Los Data Warehouses son bases de datos donde la data de diferentes sistemas es almacenada y modelada para ayudar al analisi de otras actividades relacionas con responder las interrogantes que se presenten. La data en los Data Warehouses es estruturada y optimizada para solicitudes de analiisi y reportes.

> Los Data Lakes es donde data es almacenda pero sin la estructura y optimización de un Data Warehouse. Este contiene un alto volumen de data y una gran vartiedad de data.
- Herramientas de ingesta de datos
>Las más comunes herramientas y frameworks incluyen: Singer, Stitch y Fivetran. La ingesta de datos incluye tradicionalmente los pasos de extraer y cargar de los procesos ETL ( Extraer - Transformar - Cargar) y ELT ( Extraer - Cargar - Transformar ). algunas ehrramientas se enfocan en estos pasos, mientras otros tambien aportan capacidades de transformación de datos.
- Herramientas de modelado y frameworks
> La transformación de datos puede ser simple como convertir el formato de hora en una tabla o algo más conplejo como crear una nueva medida a partir de otras columnas por medio de lógica de negocios.

> Modelado de datos es un tipo de trnasformación de datos mas especifico, un modelos de datos estructura y define datos en un formato que es entendido y opstimizado para el analisis, un modelos de datos es usado para representar una o mas tablas en un data Warehouse.
- Plataformas de orquestación de flujo de trabajo
> Estas plataformas administran el horario y flujo de tareas en una pipeline. Existen algunas plataformas como: Apache Airflow, Luigi, AWS Glue y estan diseñadas para casos de uso generales y son empleados ppara una gran variedad de pipelines.
> Las tareas de los pipelines son siempre directas, estas inician con una o varias tareas cuando una o varias tareas especificas terminan, esto es requerido para garantizar la ejecución. en otras palabras se asegura que estas tareas no se ejecuten antes que sus tareas dependientes y se completen corectamente. Esto genera un **grafico aciclico** indicando que una tarea no puede ir hacia una tarea completada previamente.
---
