# Genómica Computacional: Grupo 7075, Semestre 2020-2
## Práctica 03 - Genómica y Filogenómica (Entrega: 15.05.20/23:59)

**Indicaciones:** La práctica esta compuesta de dos partes con ejercicios. Deberán resolver **de manera individual** los ejercicios conforme se indique y anotar los comandos y respuestas que se piden en un archivo tipo [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) `.md`. Es responsabilidad de los alumnos subir el directorio correspondiente a su cuenta de [git](https://github.com/) y corroborar que se encuentre toda la información que se les pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a la cuenta de `git` donde se realizó la práctica antes de que cierre la asignación **(15.05.20/23:59)**. **Nota:** Si existen dudas al respecto de la práctica, favor de escribir a mi correo. **Estaré respondiendo dudas a más tardar el viernes 15.05.20 a las 11:59.**

***

**Objetivo:** En esta práctica, se espera que los alumnos revisen los flujos de datos posibles desde la salida del secuenciador, hasta una aplicación final. Se revisarán los conceptos básicos y software específico de alineamientos, ensambles, predicción de genes y filogenias.

01. ^En su directorio `genomica_2020-2` deberán crear uno nuevo de la siguiente manera (minúsculas): `inicialdelnombre+apellido+_p03`. **Ejemplo:** Equipo: Marisol Navarro -> `mnavarro_p03`. 
02. ^Cada que se indique **(Ej. 1. ^)** deberán anotar los comandos que utilizaron en un archivo denominado `comandos_p03.md`. Este archivo deberán crearlo dentro de su directorio.  
03. Deberá subir el link de su git a Google Classroom una vez finalizada la práctica. 
04. En el nuevo directorio deberán crear los directorios correspondientes: `data/`, `data/filtered/`, `data/raw_data/`, `meta/`, `scripts/`, `figures/` y `archive/`. 

Los comandos y outputs de los ejercicios marcados **(Ej. 1. ^)** en el archivo `comandos_p03.md` deberán seguir el siguiente formato : 

```
# Comandos de la Práctica 03
## Nombre y Apellidos

## Parte I. 
01. [comando] [opciones] [argumentos]
02. [comando] [opciones] [argumentos]
…

# Parte II.
...
```

## Parte I. __ / 25

**Alineamientos**

Un alineamiento es un proceso que recibe como datos de entrada un conjunto secuencias en formato `fastq`, generadas por alguna metodología de secuenciación masiva, y un archivo de referencia (genoma completo, transcritos, etc) en formato `fasta`. *El objetivo del alineamiento es localizar la posición donde se encuentra la máxima semejanza entre cada una de las secuencias cortas respecto a la referencia.* En este sentido, es importante mencionar que existe la posibilidad de encontrar más de una solución y que la complejidad es grande dado el tamaño de los archivos de entrada. *En términos generales, el resultado del alineamiento será la posición en la que cada secuencia alinea con respecto a la referencia o un asterisco en caso de no alinear y el formato de salida más utilizado en el que se reporta el resultado es BAM/SAM.* 

* **Alineamiento local** = encuentra regiones de similitud en partes de las secuencias 

Los **alineamientos locales** identifican regiones similares dentro de largas secuencias que normalmente son muy divergentes entre sí. A menudo se prefieren los alineamientos locales, pero pueden ser más difíciles de calcular porque se añade el desafío de identificar las regiones de mayor similitud.

* **Alineamiento global** = encuentra el mejor alineamiento a través de las dos secuencias completas 

Calcular un **alineamiento global** es una forma de optimización global que forza al alineamiento a ocupar la longitud total de todas las secuencias introducidas (secuencias problema). Una estrategia general de alineamiento global es el algoritmo Needleman-Wunsch basado en programación dinámica.

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_01.jpg)

Un diagrama de trabajo nos indicaría como primer paso la selección de nuestra **referencia** y una vez con esta utilizamos alguno(s) de los programas existentes para hacer el alineamiento (mapeo) de secuencias sobre la referencia. La mayoría de los alineadores de secuencias inician con un proceso de generación de un **índice** que no es otra cosa que la creación de un *“diccionario”* para buscar las distintas secuencias.

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_01.png)

Existen muchos programas para alinear (mapear), la mayoría son software libre. Por ejemplo: `Bowtie`, `Bowtie2`, `SMALT`, `MAQ`, `BWA`, `SOAP2`, `SHRIMP`, `BFAST`, `Eland`, etc.

¿Cuál es el mejor? ¿Cuál utilizar? Esto dependerá de los siguientes criterios:

* Tipo de datos
* Tiempo de procesamiento
* Recursos (hardware) que consume
* Precisión
* Sensibilidad
* Otros

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_02.png)

A grandes rasgos, buscar regiones idénticas entre cadenas de texto pudiera parecer una tarea sencilla y rápida. Sin embargo el volumen de datos generados con las nuevas tecnologías (plataformas) de secuenciación masiva y los problemas con los que deben de lidiar estos algoritmos como son: inserciones o ausencias de bases en nuestras secuencias o en la referencia, bases diferentes, y las regiones repetidas, hacen de esta búsqueda de identidad algo complejo algorítmicamente y por lo tanto computacionalmente. 

Para entender cómo funcionan estos algoritmos es necesario entender un concepto que todos estos programas manejan.

**¿Qué es un k-mero?**

Un `k-mero` es una palabra de tamaño k. Debemos saber que `N-k+1` sería el total de palabras contenidas en un `read` de longitud N. Por otro lado, la importancia de estos es la velocidad con la que nos permite reconstruir las palabras, estos nos permitirán conectar reads de una manera más eficiente. La mayoría de los algoritmos de alineamientos funcionan haciendo primero un **índice** (con estructura de árbol) de la **referencia** con la queremos trabajar. Esto con la finalidad de que la búsqueda de nuestras lecturas pueda ser de manera rápida, aunque algunas veces parcial, necesitando de programación dinámica para comprobar la posición exacta de la lectura. 

Dentro de los programas más utilizados, se encuentran dos algoritmos para hacer estos índices, el de **hashing** que se define como la transformación de una cadena de caracteres en un valor que suele ser más corto de longitud (un k mero) y que sirve para representar la cadena original. Esto nos permitirá entender las transformadas de `Burrow-Wheeler (TBW)`, que es un algoritmo usado en técnicas de compresión de datos. Ambos algoritmos tienen sus fortalezas, los programas que utilizan las TBW como `BWA` y `Bowtie`, suelen ser más rápidos en la búsqueda de **matches** exactos. Por otro lado el programa `SMALT` que utiliza **hashing** es un poco más lento y requiere de mayor cantidad de memoria RAM, sin embargo es menos sensible a regiones repetidas y tolera mejor la variabilidad entre los genomas.
