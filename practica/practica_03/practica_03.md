# Genómica Computacional: Grupo 7075, Semestre 2020-2
## Práctica 03 - Genómica y Filogenómica (Entrega: 15.05.20/23:59)

**Indicaciones:** La práctica esta compuesta de cuatro partes con ejercicios. Deberán resolver **de manera individual** los ejercicios conforme se indique y anotar los comandos y respuestas que se piden en un archivo tipo [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) `practica_03.md`. Es responsabilidad de los alumnos subir el directorio correspondiente a su cuenta de [git](https://github.com/) y corroborar que se encuentre toda la información que se les pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a la cuenta de `git` donde se realizó la práctica antes de que cierre la asignación **(15.05.20/23:59)**. **Nota:** Si existen dudas al respecto de la práctica, favor de escribir a mi correo. **Estaré respondiendo dudas a más tardar el viernes 15.05.20 a las 11:59.**

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
01. Tabla
02. [comando] [opciones] [argumentos]
…

# Parte II.
...
```

## Parte I. __ / 30

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

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_03.png)

Dentro de los programas más utilizados, se encuentran dos algoritmos para hacer estos índices, el de **hashing** que se define como la transformación de una cadena de caracteres en un valor que suele ser más corto de longitud (un k mero) y que sirve para representar la cadena original. Esto nos permitirá entender las transformadas de `Burrow-Wheeler (TBW)`, que es un algoritmo usado en técnicas de compresión de datos. Ambos algoritmos tienen sus fortalezas, los programas que utilizan las TBW como `BWA` y `Bowtie`, suelen ser más rápidos en la búsqueda de **matches** exactos. Por otro lado el programa `SMALT` que utiliza **hashing** es un poco más lento y requiere de mayor cantidad de memoria RAM, sin embargo es menos sensible a regiones repetidas y tolera mejor la variabilidad entre los genomas.

*** 
01. BLAST es una herramienta que busca alinear segmentos de secuencias en lugar de toda la secuencia, es capaz de detectar relaciones entre secuencias que comparten regiones aisladas de similitud. Ingresa a [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) (Basic Local Alignment Search Tool) de NCBI. Realiza un alineamiento de nucleótidos e identifica la secuencia problema `sequence_x.fasta` puedes subirla como archivo o copiarla directamente. Responde: 1.1 ¿A qué organismo pertenece? 1.2 ¿Es un gen o una región genómica de importancia? 1.3 ¿Qué es un marcador molecular? 1.4 ¿Cuál es la importancia de este tipo de marcador en particular?      
02. Existen diferentes programas/tipos de BLAST por ejemplo: `blastn` es que utilizaste en el ejemplo anterior. Realiza una tabla de tres columnas donde indiques `BLAST`-tipo de BLAST-, `Definición`-en qué consiste-, `Aplicación`-para qué tipo de análisis lo usarías-.
03. Realiza la búsqueda de un artículo científico de tu interés dónde utilicen software específico de mapeo. Describe en un breve párrafo la metodología que utilizaron para realizar el mapeo. No olvides incluir la referencia del artículo.

## Parte II. __ / 30

Las estrategias de secuenciación consisten en la **fragmentación** al azar del genoma para obtener fragmentos de uno o varios tamaños para poder obtener lecturas o reads ya sea de cada extremo de la molécula para su posterior reconstrucción.

Un `read` es una lectura obtenida de un fragmento de DNA o de cDNA a partir de moléculas de RNA. Con las tecnologías de secuenciación se puede determinar el orden de los nucleótidos de una o varias moléculas de DNA ya sean por uno o ambos lados. *El tamaño del fragmento dependerá en gran medida del tipo de análisis y tecnología de secuenciación que utilicemos.*

Por ejemplo, la secuenciación tipo Sanger, dependía de que los fragmentos fueran primero puestos en un vector de clonación por dos principales razones: 

* El vector contiene secuencias que nos permiten insertar fragmentos de DNA en una región cuya secuencia es conocida y así iniciar el proceso de secuenciación.
* Permite “amplificar” y preservar el fragmento dentro de un organismo hospedero como lo es una bacteria. 

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_04.png)

En las tecnologías de segunda y tercera generación, no se requieren ni de vectores ni de hospederos para la manipulación de los fragmentos a secuenciar. Sin embargo, existe un límite de tamaño dependiendo de las tecnologías de segunda generación principlamente. 

Por ejemplo, `Illumina`, `454` y `Ion Torrent`, tienen un límite de aproximadamente 1,000 pares de bases y en el caso de las últimas dos tecnologías, no es posible realizar la secuenciación por ambos lados a menos que se utilice un protocolo especial llamado **mate pair**. Para obtener lecturas mate pair, se requieren de fragmentos mayores a 2,000 pares de bases los cuales son circularizados uniendo los extremos con una secuencia especial que permite seleccionar dicha región del círculo después de un proceso de fragmentación. Este tipo de reads son extremadamente útiles para unir fragmentos reconstruidos o `contigs` y darle una mayor continuidad y orientación al genoma.

Un `contig` se define como la representación de un set de reads que sobrelapan y que constituyen el consenso de una región de DNA secuenciada. Como se mencionó antes, estos contigs pueden ser comunicados o unidos en fragmentos aún más grandes gracias a las secuencias con paridad como las secuencias mate pair. A estos fragmentos más grandes se les llama `scaffolds` y son contigs unidos por Ns que según el código IUPAC, representa cualquier nucleótido. El número de Ns corresponderá a la distancia que existe entre dos contigs, que a su vez está determinada por el tamaño del fragmento (circulo) que se eligió.

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_05.png)

**Overlap-Layout-Consensus**

Este método es un método para reconstruir genomas o bien, ensamblarlos *de novo*. Esto quiere decir que no conocemos el orden ni la relación entre las secuencias obtenidas para un organismo y no existe un genoma de referencia que podamos usar para orientar y ubicar las secuencias. Por lo tanto, es necesario calcular todos los sobrelapes (“overlaps”) posibles entre los reads alineando todos contra todos. La parte del “layout” consiste en localizar y ordenar todos los reads que presentaron un sobrelape. Finalmente, se determina la secuencia consenso (“consensus”) uniendo todos los reads alineados. Si existe información de reads pareados o “mate pair” se puede realizar el “scaffolding”.

Como se puede suponer, el calcular todos los alineamientos posibles, no es computacionalmente eficiente, por lo que se requieren de métodos heurísticos que suponen o explorar una buena cantidad de los alineamientos posibles, pero no todos. Por lo tanto, esto implica errores en el ensamblado. Además, existirán secuencias repetitivas que dificulten los pasos del “layout” y el consenso generando también errores.

**Teoría de gráficas**

La teoría de gráficas es muy conveniente para solucionar el problema del ensamblado *de novo*, debido a que simplifica la parte del “layout”. Sin embargo, su mayor utilidad es en el ensamble de datos de secuenciación masiva, debido a que debido al gran volumen de datos generados, sería imposible buscar todos los sobrelapes posibles entre los reads y aún más dado la longitud de las secuencias y la probabilidad de encontrar varios sobrelapes incorrectos. 

La teoría de gráficas surge a raiz de un problema matemático abordado por Leonhard Euler en 1736 donde trato de encontrar la manera de caminar a través de la ciudad de Königsberg en Prusia (actualmente Kaliningrado, Rusia) donde se tienen dos grandes islas que están conectadas por 7 puentes. Se requeria encontrar una ruta donde se pudiera pasar por la ciudad cruzando cada puente una solo una vez y que el punto inicial no fuera el mismo que el punto final.

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_06.png)

A pesar de que el problema en si no tiene solución, este fue el primer teorema de teoría de graficas por lo que inspiró a otros trabajos como el de Nicolaas Govert de Bruijn (pronunciado “bruaien”), el cual es utilizado para el ensamble de genomas u transcriptomas.

Un **ensamble genómico** consiste en tomar una colección de secuencias (lecturas mucho más cortas) y reconstruir con estas la secuencia del genoma del cual fueron originadas. 

Una buena señal de la calidad de nuestras secuencias y la calidad de nuestro ensamble final es el poder localizar de vuelta la mayor cantidad de las lecturas de entrada sobre el resultado del ensamble, además de ser localizados en la orientación y distancia esperada. Otra señal de la calidad de nuestro ensamble es la cantidad de fragmentos en los que quede, en la mayoría de los ensambladores obtenemos finalmente fragmentos que llamaremos `contigs` (regiones contiguas de lecturas), en otros llegaremos a nivel de scaffolds o supercontigs (conjuntos de contigs que se colocan en orden y sentido entre ellos).

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_07.png)

Programas para realizar ensambles genómicos:

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_08.png)
![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_09.png)

Consideraciones para casi todos los ensambladores:

* Asegurarse de realizar un control de calidad de las lecturas antes de ser ensambladas.
* De ser posible, verificar el tamaño de inserto de las librerías.
* Genomas con mayor cantidad y longitud de regiones con secuencias repetitivas, requieren mayor longitud de lecturas y mayor tamaño de inserto de librerías pareadas.
* Regiones repetitivas implicarán una mayor cantidad de alineamientos incorrectos en las
secuencias.
* La ploidía del organismo. Las poliploidías hacen aún más problemático los ensambles.
* Probar varios tamaños de k-meros en aquellos ensambladores basados en gráficas de de Bruijn.

**Comparando ensambles**

*In computational biology, N50 and L50 are statistics of a set of contig or scaffold lengths. The N50 is similar to a mean or median of lengths, but has greater weight given to the longer contigs. It is used widely in genome assembly, especially in reference to contig lengths within a draft assembly. L50 is the number of contigs whose summed length is N50.*

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_03/tres_10.png)

***

01. Explica:¿En qué consiste el problema de los puentes de la ciudad de Königsberg? ¿Por qué no tiene solución? Puedes consultar material libremente, para comenzar puedes ver el siguiente [video](https://www.youtube.com/watch?v=nZwSo4vfw6c).
02. Para profundizar en el tema de OLC y De Bruijin Graphs, consulta el siguiente artículo [How to apply de Bruijn graphs to genome assembly](https://www.researchgate.net/publication/51784417_How_to_apply_de_Bruijn_graphs_to_genome_assembly) y explica tres problemáticas comunes en la aplicación de las gráficas de Bruijin a genomas.    
03. Explica ¿qué son? ¿en qué consisten? y ¿para qué se usan? las estadísticas N50 y L50.
