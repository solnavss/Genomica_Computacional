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

* **Alineamiento local**

Los **alineamientos locales** identifican regiones similares dentro de largas secuencias que normalmente son muy divergentes entre sí. A menudo se prefieren los alineamientos locales, pero pueden ser más difíciles de calcular porque se añade el desafío de identificar las regiones de mayor similitud.

* **Alineamiento global**

Calcular un **alineamiento global** es una forma de optimización global que forza al alineamiento a ocupar la longitud total de todas las secuencias introducidas (secuencias problema). Una estrategia general de alineamiento global es el algoritmo Needleman-Wunsch basado en programación dinámica.

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_01.jpg)

Un diagrama de trabajo nos indicaría como primer paso la selección de nuestra **referencia** y una vez con esta utilizamos alguno(s) de los programas existentes para hacer el alineamiento (mapeo) de secuencias sobre la referencia. La mayoría de los alineadores de secuencias inician con un proceso de generación de un **índice** que no es otra cosa que la creación de un *“diccionario”* para buscar las distintas secuencias.

Existen muchos programas para alinear (mapear), la mayoría son software libre. 

Por ejemplo: Bowtie, Bowtie2, SMALT, MAQ, BWA, SOAP2, SHRIMP, BFAST, Eland, etc.

¿Cuál es el mejor? ¿Cuál utilizar? Esto dependerá de los siguientes criterios:

• Tipo de datos

• Tiempo de procesamiento

• Recursos (hardware) que consume

• Precisión

• Sensibilidad

• Otros

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_02.png)


