# Arquitecturas no configurables

* [Introducción.](#Introduccion)
* [Técnicas de Paralelismo.](#Tecnicas-de-paralelismo)
	* [Procesador vectorial.](#Procesador-vectorial)
	* [Procesador Escalar Segmentado.](#Procesador-escalar-segmentado)
	* [Procesador Escalar Supersegmentado.](#Procesador-escalar-supersegmentado)
	* [Procesador Escalar Superescalar.](#Procesador-escalar-superescalar)
	* [Procesador VLIW.](#Procesador-vliw)
	* [Técnicas Multihilos.](#Tecnicas-multihilos)
* [Taxonomía Flynn.](#Taxonomia-flynn)
	* [Una instrucción, un dato (SISD).](#SISD)
	* [Múltiples instrucciones, un dato (MISD).](#MISD)
	* [Una instrucción, múltiples datos (SIMD).](#SIMD)
	* [Múltiples instrucciones, múltiples datos (MIMD).](#MIMD)
* [Medición del rendimiento.](#Medicion-del-rendimiento)
	* [Rendimiento.](#Rendimiento)
	* [Speed-Up.](#Speed-up)
* [MIMD.](#MIMD-extendido)
* [OpenMP y MPI.](#OpenMP-y-MPI)
* [Cluster, Grid y Cloud Computing.](#Cluster-grid-y-cloud-computing) 
	* [Cluster.](#Cluster)
	* [Grid.](#Grid)
	* [Cloud Computing.](#Cloud-computing)
	* [Comparación.](#Comparacion)

## <a name="Introduccion"></a> Introducción

**Ventajas de la computación secuencial:** 
* Programación más sencilla

**Desventajas de la computación secuencial:** 
* Secuencialidad del trabajo
* No se aprovechan todos los recursos


**Surge la necesidad de paralelismo**
* por las limitaciones físicas de la computación secuencial
* por la complejidad en los problemas


## <a name="Tecnicas-de-paralelismo"></a>Técnicas de Paralelismo

### <a name="Procesador-vectorial"></a>Procesador vectorial

Es un diseño de CPU capaz de ejecutar operaciones matemáticas sobre múltiples datos de forma simultánea (**SIMD**).
Su uso fue declinando tras las mejoras en los procesadores escalares, particularmente en los microprocesadores. Sin embargo, casi todas las CPU de hoy en día incluyen algunas instrucciones de procesamiento de tipo vectorial.
Los procesadores vectoriales proporcionan operaciones de alto nivel que trabajan sobre vectores.
**Una máquina vectorial consta de una unidad escalar segmentada y una unidad vectorial.** La unidad vectorial dispone de M registros vectoriales de N elementos y de unidades funcionales vectoriales (de suma/resta, multiplicación, división, de carga/almacenamiento, etc.) que trabajan sobre los registros vectoriales, y un conjunto de registros escalares.
Dispone de un conjunto de instrucciones vectoriales. Por ejemplo addv v1,v2,v3.
Una operación vectorial equivale a un bucle completo que procesaría los N elementos del registro vectorial.

### <a name="Procesador-escalar-segmentado"></a>Procesador Escalar Segmentado
Los procesadores Escalares son el tipo más sencillo de procesadores. Cada instrucción de un procesador escalar opera sobre un dato cada vez (SISD). 
Se vale de la técnica de segmentación (pipelining), en la cual se solapa la ejecución de múltiples instrucciones. Cada instrucción se ejecuta en cuatro segmentos: búsqueda, decodificación, ejecución y almacenamiento. Cuando se cumple un segmento de una instrucción se puede seguir con el siguiente segmento de otra.

### <a name="Procesador-escalar-supersegmentado"></a>Procesador Escalar Supersegmentado
Igual que el anterior con la diferencia que la instrucción se divide en seis segmentos: búsqueda, dirección efectiva, memoria, decodificación, ejecución y postescritura.

### <a name="Procesador-escalar-superescalar"></a>Procesador Escalar Superescalar
Superescalar es el término utilizado para designar un tipo de microarquitectura de procesador capaz de ejecutar más de una instrucción por ciclo de reloj (
).
O sea es lo mismo que el anterior (mantiene los seis segmentos) y utiliza pipelining para paralelizar el flujo de una instrucción, pero para paralelizar instrucciones utilizan varias unidades funcionales (ALUs, Unidades de lectura/escritura en memoria, Unidades de coma flotante, Unidades de salto), lo que incrementa el hardware.

### <a name="Procesador-vliw"></a>Procesador VLIW
Del inglés Very Long Instruction Word. Esta arquitectura de CPU implementa una forma de paralelismo a nivel de instrucción, por lo que también podría ser un MIMD.
Es similar a las arquitecturas superescalares, ambas usan varias unidades funcionales (por ejemplo varias ALUs, varios multiplicadores, etc) para lograr ese paralelismo.
Los procesadores con arquitecturas VLIW se caracterizan, como su nombre indica, por tener juegos de instrucciones muy simples en cuanto a número de instrucciones diferentes, pero muy grandes en cuanto al tamaño de cada instrucción. Esto es así porque en cada instrucción se especifica el estado de todas y cada una de las unidades funcionales del sistema, con el objetivo de simplificar el diseño del hardware al dejar todo el trabajo de planificar el código en manos del programador/compilador, en oposición a un procesador superescalar, en el que es el hardware en tiempo de ejecución el que planifica las instrucciones.

**Ventajas:**
Simplificación de la arquitectura hardware al no tener que planificar el código.
Menor potencia y consumo.

**Inconvenientes:**
Requiere compiladores mucho más complejos.
Cualquier mejora en la arquitectura hardware implica un cambio en el juego de instrucciones (compatibilidad hacia atrás nula).


### <a name="Tecnicas-multihilos"></a>Técnicas Multihilos
Un hilo es simplemente una tarea que puede ser ejecutada al mismo tiempo con otra tarea.
Los hilos de ejecución que comparten los mismos recursos, sumados a estos recursos, son en conjunto conocidos como un proceso. El hecho de que los hilos de ejecución de un mismo proceso compartan los recursos hace que cualquiera de estos hilos pueda modificar estos. Cuando un hilo modifica un dato en la memoria, los otros hilos acceden a ese dato modificado inmediatamente.

## <a name="Taxonomia-flynn"></a>Taxonomía Flynn


Las cuatro clasificaciones definidas por Flynn se basan en el número de instrucciones concurrentes (control) y en los flujos de datos disponibles en la arquitectura:


### <a name="SISD"></a>Una instrucción, un dato (SISD)
Computador secuencial que no explota el paralelismo en las instrucciones ni en flujos de datos. Ejemplos de arquitecturas SISD son las máquinas con uni-procesador o monoprocesador tradicionales como el PC o los antiguos mainframe.

### <a name="MISD"></a>Múltiples instrucciones, un dato (MISD)
Poco común debido al hecho de que la efectividad de los múltiples flujos de instrucciones suele precisar de múltiples flujos de datos. Sin embargo, este tipo se usa en situaciones de paralelismo redundante, como por ejemplo en navegación aérea, donde se necesitan varios sistemas de respaldo en caso de que uno falle. También se han propuesto algunas arquitecturas teóricas que hacen uso de MISD, pero ninguna llegó a producirse en masa. Algunos autores consideran que las arquitecturas vectoriales supersegmentadas o vectorial escalar forman parte de este modelo ya que en un momento dado se pueden estar manipulando un dato (el vector) por varias instrucciones, no obstante no existe consenso al respecto.

### <a name="SIMD"></a>Una instrucción, múltiples datos (SIMD)
Un computador que explota varios flujos de datos dentro de un único flujo de instrucciones para realizar operaciones que pueden ser paralelizadas de manera natural. Por ejemplo, un procesador vectorial.

### <a name="MIMD"></a>Múltiples instrucciones, múltiples datos (MIMD)
Varios procesadores autónomos que ejecutan simultáneamente instrucciones diferentes sobre datos diferentes. Los sistemas distribuidos suelen clasificarse como arquitecturas MIMD; bien sea explotando un único espacio compartido de memoria, o uno distribuido.

## <a name="Medicion-del-rendimiento"></a>Medicion del rendimiento


### <a name="Rendimiento"></a>Rendimiento:
Indica el rendimiento de un procesador al ejecutar un algoritmo secuencial. Se puede medir en:
	
1. MIPS: Millones de Instrucciones por Segundo.
2. MFLOPs: Millones de Operaciones de Punto Flotante por Segundo


### <a name="Speed-up"></a>Speed-Up:
Indica la mejora que el algoritmo/hardware paralelos tienen sobre la mejor solución secuencial


	Speed-Up = Rendimiento paralelo / Rendimiento secuencial


Si da mayor a 1 es un speed-up bueno, si por el contrario da menor que 1 se considera malo.
Teniendo en cuenta que:


	Speed-up optimo = Rendimiento secuencial / Nro de cores


Podemos obtener la eficiencia, que indica cuanto provecho se esta sacando de la arquitectura paralela, y cuanto mas se podria sacar.


	Eficiencia = Speed-up obtenido / Speed-up optimo


Cuanto mas cerca este de 1, indicara un uso optimo de los recursos paralelos, pero si esta mas cerca del 0, quiere decir que los recursos paralelos se estan desaprovechando.


## <a name="MIMD-extendido"></a>MIMD


Este se clasifica a su vez en dos grandes grupos:
	
1. los MIMD con memoria compartida (MULTIPROCESADORES)
2. los MIMD con memoria distribuida (MULTICOMPUTADORES)


Los **multiprocesadores** son computadores que tienen memoria compartida y se pueden clasificar en UMA (uniform memory access), NUMA (nonuniform memory access).
Los nombres que reciben las arquitecturas multiprocesador UMA y NUMA tienen que
ver con el tiempo de acceso a la memoria principal.

**UMA:** en este tipo de arquitectura, como bien dice su nombre, todos los accesos a memoria tardan el mismo tiempo.

**NUMA:** en los multiprocesadores NUMA, a diferencia de los UMA, los accesos a memoria pueden tener tiempos distintos.
**Están fuertemente acoplados y no son escalables.**


Los **multicomputadores** consisten en un conjunto de procesadores y bancos de memoria que se conectan a través de una red de interconexión con una determinada topología de red.
La característica más importante de estos sistemas es que tienen la memoria distribuida.
Esta arquitectura también es conocida como arquitectura basada en el paso de mensajes, ya que los procesos deben realizar comunicaciones (mensajes) a través de la red de interconexión para poder compartir datos. Estas máquinas, por consiguiente, no están limitadas por el ancho de banda de memoria, sino más bien por el de la red de interconexión.
**Están débilmente acoplados y son escalables.**
Dentro de los multicomputadores se encuentran los MPP (massively parallel processors) y los clusters.




## <a name="OpenMP-y-MPI"></a>OpenMP y MPI

[OpenMP]() -> memoria compartida
[MPI]() -> memoria distribuida


## <a name="Cluster-grid-y-cloud-computing"></a>Cluster, Grid y Cloud Computing


### <a name="Cluster"></a>Cluster
nodos homogéneos centralizados en un unico nodo front-end. 
Mejora el rendimiento dedicando mas recursos.

### <a name="Grid"></a>Grid
nodos heterogéneos más dispersos geográficamente que en el cluster. 
Mejora el rendimiento compartiendo recursos sub-utilizados de otros equipos.

### <a name="Cloud-computing"></a>Cloud Computing 
nodos heterogéneos muy dispersos, no son colaborativos.
se alquilan recursos. 

### <a name="Comparacion"></a>Comparación
Cluster difiere del grid y de la computación en la nube en que un cluster es un grupo de ordenadores conectados en una red de área local (LAN), mientras que la nube y el grid son de escala más amplia y pueden ser distribuidos geográficamente. Otra forma de decirlo es decir que las máquinas de un cluster están estrechamente unidas (fuertemente acoplados), mientras que en un grid o la nube están débilmente acoplados. También, los clusters se componen de máquinas con hardware similar, mientras que las nubes y las redes se componen de máquinas con posiblemente muy diferentes configuraciones de hardware.
