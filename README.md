# Postgres SandBox: Creating Data Bases with GenAI

## Introducción

La irrupción de la IA generativa ha abierto un mundo de posibilidades para todas aquellas personas que no poseen las habilidades necesarias para desarrollar una tarea concreta, como puede ser la composición de música, imágenes, código, … pero también ha significado un aumento de las habilidades y la productividad de aquellos que sí que poseen dichas habilidades. 

En medio de esta proliferación de distintas herramientas que emplean la IA nace postgres, una herramienta que permite crear bases de datos a partir de lenguaje natural. 

Postgres es capaz de traducir las instrucciones escritas en un lenguaje humano a un lenguaje SQL que le permita crear una base de datos tanto en estructura, como de rellenarla con datos. La capacidad de personalizar las tablas creadas y de crear las relaciones entre estas es algo que podría ayudar enormemente a los arquitectos e ingenieros de datos, pues con su conocimiento tan avanzado serán capaces de emplear esta herramienta con todo su potencial.

## Objetivos

En este proyecto vamos a hacer un uso simple, a nivel de usuario, de esta IA para crear una tabla que simulará las ventas que ha tenido una tienda textil de venta al pormenor a lo largo de un año (2023). 

La idea es familiarizarnos con la herramienta y ver qué tan útil puede ser para, posteriormente, practicar el análisis de los datos.

## Desarrollo del proyecto

Empezamos el proyecto haciendo un boceto de cómo queremos que sea la tabla que vamos a crear para nuestra base de datos, así como las condiciones a la hora de rellenarla. En principio, la tabla va a tener seis columnas (ID, que será la primary key; artículo, que será el nombre del artículo vendido; color, que será el color del artículo; pecio; fecha_venta, que es cuándo se vendió; cantidad, que es el número de unidades que se han vendido de un mismo artículo). 

En cuanto a las condiciones, se pretende que se rellenen datos para todos los días del año, excluyendo algunos días festivos que vamos a indicarle, así como los fines de semana, los cuales los toma como días no laborables por defecto. 

![image](https://github.com/user-attachments/assets/d7492aef-e7c3-49be-8192-2a6c52dd23fd)

<b>Figura 1:</b> Prompt inicial con las conodiciones para crear la tabla y su resultado.

También se han incluido algunas condiciones extra para intentar hacer que los datos se asemejen un poco más a la realidad, siendo que en enero los precios tendrán un descuento aplicado sobre estos (rebajas de enero) y que hay ciertos artículos que no se venden en ciertos meses o que se compran en mayor medida en otros.

La figura 1 muestra tanto la entrada dada inicialmente como la tabla resultante de dichas instrucciones, mientras que en la figura 2 podemos ver el código que se ha empleado tanto para crear la tabla como para introducir datos en esta.

![image](https://github.com/user-attachments/assets/18282674-5dcf-4749-b60b-51a0127c8773)

<b>Figura 2:</b> Código empleado para la creación de la tabla (izq) y el llenado de esta (dcha).

En la GUI se pueden emplear sentencias SQL para ver los datos contenidos dentro de la tabla, pero postgres suele limitarlo a 5 filas como máximo. Si pretendemos ver todas las filas, postgres creará un archivo CSV que podremos descargarlo y visualizarlo en nuestra aplicación favorita. Los datos, sin embargo, puede que no se pasen del todo bien en los formatos deseados a la hora de cargarlos en programas como Power BI, algo que puede verse en la figura 3, siendo necesario un pequeño proceso de limpieza y transformación para prepararlos para su posterior visualización y análisis. 

![image](https://github.com/user-attachments/assets/454b26a9-52b0-4ae1-9fbb-0875412bb9d7)

<b>Figura 3:</b> Datos cargados en Power BI previos a su limpieza y transformación.

Como el objetivo de este proyecto es familiarizarse con la herramienta y ver sus capacidades, todo el proceso de tratamiento de los datos se sale del enfoque del proyecto, dejando esto como una tarea a realizar en un futuro trabajo donde se realizará un pequeño análisis de los datos obtenidos.

Pese a la gran capacidad de trabajo de la IA, si observamos algunos de los datos que ha introducido en la tabla (figura 2), vemos que hay saltos en las fechas, pasando de tener entradas en marzo, a tenerlas en junio. También vemos que no todos los días tienen entradas, solo un pequeño puñado. Esto ya nos viene avisando que las instrucciones dadas en la figura 1 no han sido suficientes para crear una tabla que nos satisfaga (de cara a usar la tabla como un set de datos de entrenamiento para los analistas), por lo que será necesario ir afinando la tabla con instrucciones extra, como puede verse en la figura 4.

![image](https://github.com/user-attachments/assets/0865f63c-d088-4335-bfa4-f7de9307582e)

<b>Figura 4:</b> Prompt con el que se van ajustando los datos a lo que se pretendía obtener originalmente.

Una vez ya hemos comprobado que los cambios han surtido efecto y que la tabla se ajusta mucho más a lo que deseábamos obtener en un inicio, basta con realizar una query donde le pidamos todos los datos de la tabla para que postgres haga una copia de la tabla en formato csv y nos permita descargarlo, dando por finalizado el proyecto.

## Palabras Finales

Postgres ha resultado ser una herramienta muy potente ya a nivel usuario para crear tablas y rellenarla con datos. Ser capaz de usar lenguaje natural y que la IA lo convierta a lenguaje SQL, así como darnos el código empleado ayuda mucho en las fases de aprendizaje, pues un completo novato puede pedirle a la IA que haga una tabla con unas condiciones específicas usando un lenguaje que usaría a la hora de comunicarse con otra persona y podría ver cómo eso se traduce a un lenguaje que las bases de datos puedan entender para, a futuro, ser el propio usuario el que crea sus propias bases de datos o trabajar con lenguaje SQL.

Hay que tener cuidado con lo que se crea. Al igual que con todas las GenAI disponibles en internet, la IA puede cometer errores o no entender al 100% lo que le estamos pidiendo. También, su incapacidad de entender realmente lo que está haciendo puede llevar a datos erróneos, como hemos podido comprobar a lo largo del proyecto.

Esto es una llamada de atención a aquellos profesionales que vayan a animarse a usar la herramienta, así como para los iniciados que deseen aprender usándola. La herramienta es tan poderosa como nosotros sepamos usarla, por lo que debemos tener un enfoque de supervisor y siempre confirmar que el output obtenido se corresponde con lo que deseamos obtener, estando pendientes a posibles errores.

Por último, decir que esta herramienta posee mucho más poder del que he mostrado en este proyecto. Es posible, por ejemplo, hacer varias tablas y postgres sería capaz de crear las relaciones entre estas a la vez que las va creando, siendo necesario solo el confirmar que todo esté en orden. Ya dependerá del uso que se le quiera dar y el nivel de experticia del usuario para poder exprimir al máximo esta herramienta.
