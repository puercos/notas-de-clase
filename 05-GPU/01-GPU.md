# GPU (Apuntes tomados en clase - preliminar)

[TOC]

## Introducción

GPU es Graphics Processor Unit. Es decir, unidad de procesamiento de gráficos. Se trata de un componente masivamente paralelo para ejecución de tareas muy demandantes de procesamiento, específicamente para aplicaciones gráficas.
La GPU se considera una arquitectura configurable debido a que en tiempo de ejecución se adapta y se configura a lo que se requiere que haga.
Algo muy importante al hablar de GPU es el concepto de **pipeline**. Pipeline es una serie de pasos sobre la geometría y datos de entrada.
La GPU fue tradicionalmente un dispositivo utilizado para aplicaciones gráficas. Sin embargo, al brindar una gran potencia de cálculo, se comenzó a utilizar para aplicaciones de uso general, dando lugar al concepto de GPGPU (General programming graphics processor unit).
Para realizar programación de GPGPU se desarrollaron conjuntos de bibliotecas y herraminentas. 
Una de las herramientas notables que se han desarrollado con este propósito es **CUDA**, desarrollado por NVidia.
Por otra parte, **OpenCL** se desarrolla como contrapartida de NVidia pero open source, y permitiendo la programación tanto para la CPU como para la GPU.


## CPU vs GPU

|CPU | GPU|
|---|---|
|Pensada para acelerar un conjunto de aplicaciones(varias)| Pensada para mejorar el desempeño de una única aplicación con alta demanda de procesamiento paralelizable.
|Varios núcleos complejos e independientes|Vector de núcleos muy numerosos y muy simples|

## GPGPU

Inicialmente, se desarrollaban aplicaciones para la GPU utilizando el lenguaje [_shaders_](https://es.wikipedia.org/wiki/Shader) y solamente utilizando el pipeline gráfico.
La GPU tiene una gran capacidad de cálculo al estar preparada para lanzar miles de hilos en paralelo.
Actualmente se pueden utilizar lenguajes de propósito general para aplicaciones de propósito general utilizando la GPU.
A nivel de hardware, se han reemplazado procesadores dedicados para píxeles y texturas por procesadores de propósito general.
La GPU utiliza el modelo de ejecución SIMT (simple instruction, multiple threads). Se lanzan muchos hilos para ejecutar la misma instrucción sobre un conjunto de datos.
Como se ha dicho, ya no se utiliza unicamente el lenguaje Shaders, sino que se pueden utilizar lenguajes de propósito general, como C, con herramientas como CUDA o OpenCL.
Se introdujo memoria compartida y comunicación por barreras.

## Historia de las GPU

### Arquitecturas G80

Incluye 







