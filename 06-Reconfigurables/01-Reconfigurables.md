# Arquitecturas Reconfigurables

Sistemas cuyos aspectos pueden cambiar de implementacion en tiempo de ejecucion (a diferencia de GPU). Por lo general, cuentan con un procesador secuencial RISC, y una parte reconfigurable.

*Ejemplo: arquitectura reconfigurable:*

> Adaptables:
Un sistema adaptativo es un sistema reconfigurable que cambia las implementacions de sus aspectos automaticamente segun su uso (son una mejora de las arquitecturas reconfigurables).

### Unidad Funcional (FU)

Componente fisico que tiene capacidad de calculo:
- ALU (la mayoria de las arquitecturas).
- Multiplexor.

Cada tipo de arquitectura define lo que es una unidad funcional.

### Granularidad

- **Grano grueso:** trabaja a nivel de palabra (Reconfigurables)
- **Grano fino:** trabaja a nivel de bits (FPGA)

### FPGA

Primer arquitectura reconfigurable.
Muy adaptable a distintas plataformas.
Compuesta de bloques de compuertas logicas programables.
En tiempo de ejecucion se pueden reconfigurar los bloques, segun sea necesario.

## Diferencias entre FPGA y Reconfigurable

|FPGA|Reconfigurable|
|---|---|
|Bloques de compuertas logicas|ALUs|
|Grano Fino (bits)|Grano Grueso(palabras)|
|Consume mas potencia|Consume menos potencia|
|Ocupa mayor espacio (bloques)|Ocupa menos espacio|
|Algunas versiones son lentas|Reduce el tiempo de retardo|
|Mayor tiempo de configuracion (se debe configurar compuerta por compuerta)|Reduce el tiempo de configuracion|

### Objetivo principal de las Arquitecturas Reconfigurables

1. Procesamiento de telecomunicaciones.
2. Multimedia .
3. Emulacion de Hardware (puedo emular el funcionamiento de distintas arquitecturas).
4. Desarrollo de Prototipos.

### Configuracion de las Arquitecturas Reconfigurables

|Comportamiento|Ventajas|Desventajas|
|---|---|---|
|El hardware RC solo proporciona FU al procesador principal.|Agrega funcionalidad a la programacion tradicional|Pierdo tiempo de trabajo del procesador principal|
|Unidad RC como coprocesador|Permite realizar calculos sin supervision del procesador principal|Elevada transimsion de datos (el procesador principal le pasa todo lo que tiene que hacer y todos los datos al RC)|
|Unidad RC como procesador adicional|El RC tiene su propia memoria de trabajo. El procesador principal no le tiene que pasar todos los datos a nivel de registros, solo le pasa la direccion de los datos|No comparten cache|
|Unidad RC como unidad de procesamiento externo|Casi ideal (comunicacion muy infrecuente)|Mayor complejidad de sintetizacion|



### Factores a considerar para sintetizar

1. Tecnologia (no es lo mismo FPGA que otra arq. RC). Tambien el lenguaje de programacion
2. Comunicacions entre matriz reconfigurable con parte secuencial (por registro, memoria, bus, etc.)
3. Software requerido.

### Estrategias de sintetizacion(*)

|Estrategia|Ventajas|Desventajas|
|---|---|---|
|Herramientas especializadas|El paso de un programa a una arquitectura depende de un flujo de diseño|Es diferente para cada arquitectura y menos optimo. (misma forma de compilar, distintas arquitecturas = poco optimo)
|Hacerlo todo manualmente|Metodo mas potente|Hay que profundizar en la arquitectura|
|Mezcla de ambas (la mejor)|Crea rapidamente un circuito para el reconfigurable y lo hace mas accesible a los programadores|Circuitos de eficiencia relativa|

# Arquitecturas Reconfigurables mas conocidas

## Arquitectura ADRES

* Utiliza procesador **VLIW**(**) como procesador principal **(secuencial)**

* El procesador trata de explotar el paralelismo a nivel de instruccion **(ILP)**(***)

* Grafo de dependencia lo arma el compilador

* El nucleo ADRES comparte memoria cache con el VLIW.

### Las FU del VLIW son mas potentes que las FU de RC. Si las FU de RC no dan abasto, le piden ayuda a las FU de VLIW.
(las FU de VLIW se usan solo para casos extremos).
(las FU de VLIW no se pueden reconfigurar).

*Grafico: celda reconfigurable (RC):*

Dentro de la celda reconfigurable hay multiplexores, que permiten diferenciar entre los distintos buses que llegan hasta la celda, cual es el que trae datos.

*Grafico: Lenguaje basado en C*

### Funcion del sistema operativo

Controla que el mapeo se realize correctamente, y le otorga los recursos.
Le indica a la parte reconfigurable como debe funcionar.

## Arquitectura XPP (Adaptable)

Reemplaza instruccion secuencial por configuracion secuencial.

Grafo de dependencia lo arma el hardware (siempre busca armar el grafo mas optimo).

>Configuracion secuencial: buscar definicion :p

## Flujo de datos (DataStream): 
Estados que atraviesa un dato desde su estado inicial hasta llegar a su estado final.

### XPP -> Caja negra. Conozco entradas y salidas

Se dice que XPP es una arquitectura adaptable porque se reconfigura en tiempo de ejecucion, y ademas lo hace buscando la forma mas optima.

*Grafico: XXP - Estructura del nucleo*

¿Como funciona la matriz RC en XPP?

Las ALUs funcionan igual que los bloques FPGA. El grafo de ejecucion lo arma la Function-PAE (Hardware). Cuando vienen los datos, la function pae arma el grafo, y cada grafo lo mapea a una unidad funcional (ALU).

*Ejemplo: Calculo simple:*

### Arquitectura Rapid

*Grafico: Estructura*

Las FU pueden ser ALUs, multiplexores, registros, etc. Se amplian las posibilidades en comparacion con las otras arquitecturas.

El controlador determina de que forma se comportara cada unidad funcional.

## El bus es configurable, no solos las FU.

El bus esta dividido en varios buses configurables.

### Interconexiones con FU: (Configuro FU)
Controlan el transito de los datos a traves de los buses. Multiplexor.

### Bus Connector: (Configuro Bus)
Cambia la direccion de los datos. Configura la direccion del bus

*Grafico: Bus Connector (BC)*

> Notas utiles:
> 
> Kernel: Instrucciones que consumen mucho CPU
> 
> Los hilos se dividen en bloques para la ejecucion paralela

> (*)Sintetizacion: decidir que parte va al procesador secuencial y que parte va a la matriz reconfigurable (el kernel va al reconfigurable)

>(**)VLIW: Very long instruction word
>Esta arquitectura de CPU implementa una forma de paralelismo a nivel de instrucción.

>(***)Instruccion ILP: Paralelismo a nivel de instruccion.









