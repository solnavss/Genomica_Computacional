# Genómica Computacional
## Práctica 03 - Análisis de datos genómicos, Parte I: Calidad

**Indicaciones:** La práctica esta compuesta de cuatro partes. Deberán resolver **en equipos** los ejercicios y anotar los comandos, líneas de código y/o outputs que se piden en un archivo llamado `comandos_p02.txt` utilizando cualquier editor de texto plano (`emacs`, `sublime text`, `atom`, `vi`, `vim`, `nano`, `bloc de notas`, `notepad++`, etc).

**Nota:** Es responsabilidad de los alumnos subir el directorio correspondiente a su cuenta de [GitHub](https://github.com/) y corroborar que se encuentre toda la información que se le pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a su cuenta de `GitHub` antes de que cierre la asignación. 

## Parte I. __ / 20

Un integrante del equipo deberá iniciar la terminal y colocarse en su directorio `computadora@usuario:~/home/` o `computadora@usuario:~/Desktop/`. Entra a su repositorio creado anteriormente `GenomicaComputacional` y dentro de él crear un nuevo directorio como se indica a continuación (minúsculas): `nombre_del_equipo_p02`. **Ejemplo:** Equipo01 -> `Equipo01_p02`. 

También deberá crear el archivo `comandos_p02.md` en el cual colaborarán **todos los integrantes del equipo** usando el flujo de trabajo de git. Es decir, el integrante que creo el directorio deberá subirlo a git y los demás deberán clonar el repositorio solicitando permiso de colaboración. Recuerden que el archivo debe contener los comandos, imágenes, líneas de código y/o outputs que se piden para resolver cada ejercicio en [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) (también pueden consultar este enlace de [markdown avanzado](https://github.com/DavidWells/advanced-markdown/blob/master/README.md)). El archivo deberá seguir el siguiente formato: 

```
# Comandos de la Práctica 02
## Nombre del equipo
### Integrante 1: Nombre(s) Apellido(s)
### Integrante 2: Nombre(s) Apellido(s)
### Integrante 3: Nombre(s) Apellido(s)
...

# Parte I. 

**Respuesta 1:**

Tabla

# Parte II.
...
```

**Objetivo:** En esta práctica se espera que los alumnos conozcan los flujos de datos posibles desde la salida del secuenciador y el análisis primario.

**Flujo de datos de Secuenciación Masiva**

Las plataformas de `Illumina` generan por default archivos en formato `.fastq`. Plataformas como `454` y `Ion Torrent` generan archivos en formato `.sff` aunque es posible convertir este formato a `.fastq`. El análisis de calidad de las secuencias generadas en la corrida, se lleva a cabo sobre archivos en formato `.fastq`.

Cuando los archivos `.fastq` son alineados contra un *genoma de referencia*, este último debe estar en formato `.fasta`. Si en cambio lo que se realiza es un ensamblado *de novo*, el resultado del ensamble también se presenta en formato `.fasta`.

El resultado de llevar a cabo un proceso de alineamiento contra un genoma de referencia usando alineadores como `Bowtie2`, `Smalt` o `BWA`, será un archivo en formato `.sam`, que se puede convertir a un archivo en formato `.bam` (binario, mucho más compacto) o si se quiere mayor compresión, el `.bam` se puede convertir en un archivo con formato `.cram`.

A partir de los archivos mencionados anteriormente es posible corroborar la localización de anotaciones típicamente usando archivos en formato `.gff3` o `.bed` en conjunto con los archivos `.bam`. También desde el archivo `.bam` se puede realizar una búsqueda de variantes y obtener un archivo en formato `.vcf` por sus iniciales "Variant Call Format".

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_01.png)

01. Vean el siguiente video sobre tecnologías de [secuanciación masiva](https://www.youtube.com/watch?v=jFCD8Q6qSTM&list=PLTt9kKfqE_0Gem8hIcJEn7YcesuuKdt_n&index=2&t=441s) (NGS) y elaboren una tabla comparativa de las características de *algunas* de las [tecnologías](https://en.wikipedia.org/wiki/DNA_sequencing) por [generación](https://www.intechopen.com/books/next-generation-sequencing-advances-applications-and-challenges/next-generation-sequencing-an-overview-of-the-history-tools-and-omic-applications). Anoten las referencias que hayan utilizado. 

Plataforma/compañía | Longitud de reads (pb) | # reads x run | Tiempo | Costo x 10^6 bases | Error (%) | Química
--- | --- | --- | --- | --- | --- | --- |
Primera generación | | | | | | |
Sanger/Life Technologies | 800 | 1 | 2 hrs | 2400 | 0.3 | Dideoxy terminator
Segunda generación | | | | | | |
Tercera generación | | | | | | |

## Parte II. __ / 20

**Formatos de archivos más comunes: [fasta](https://en.wikipedia.org/wiki/FASTA_format)**

Este formato fue definido por el programa `FastA`, pero actualmente es usado por una gran variedad de programas (por ejemplo, `BLAST`, `gibbs`, alineadores, etc.) y se ha convertido en un estándar de formato de secuencias tanto de nucleótidos como de aminoácidos.

```
>SRR11241254.156.1 156 length=185
ACTCAGTTTGCCTGTTTTACAGGTTCGCGACGTGCTCGTACGTGGCTTTGGAGACTCCGTGGAGGAGGTCTTATCAGAGGCACGTCAACATCTTAAAGATGGCACTTGTGGCTTAGTAGAAGTTGAAAAAGGCGTTTTGCCTCAACTTGAACAGCCCTATGTGTTCATCAAACGTTCGGATGCTC
>SRR11241254.157.1 157 length=185
ACTCAGTTTGCCTGTTTTACAGGTTCGCGACGTGCTCGTACGTGGCTTTGGAGACTCCGTGGAGGAGGTCTTATCAGAGGCACGTCAACATCTTAAAGATGGCACTTGTGGCTTAGTAGAAGTTGAAAAAGGCGTTTTGCCTCAACTTGAACAGCCCTATGTGTTCATCAAACGTTCGGATGCTC
>SRR11241254.158.1 158 length=185
ACTCAGTTTGCCTGTTTTACAGGTTCGCGACGTGCTCGTACGTGGCTTTGGAGACTCCGTGGAGGAGGTCTTATCAGAGGCACGTCAACATCTTAAAGATGGCACTTGTGGCTTAGTAGAAGTTGAAAAAGGCGTTTTGCCTCAACTTGAACAGCCCTATGTGTTCATCAAACGTTCGGATGCTC
```

**Características:**

* Cada secuencia inicia con el símbolo ">" seguido del identificador de la secuencia y todos los comentarios que se quiera sobre esa misma línea. A esta línea se le llama encabezado ("header") y tiene el formato "origen | id" 
* La siguiente línea describe propiamente la secuencia, a la que se le pueden insertar saltos de línea. Los caracteres empleados requeridos corresponden al código utilizado para las secuencias de ADN o aminoácidos.
* Dentro de un solo archivo puede haber una o varias secuencias.

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_02.png)

**Formatos de archivos más comunes: [fastq](https://en.wikipedia.org/wiki/FASTQ_format)**

Fastq es un formato basado en texto para que se ajuste tanto una secuencia biológica (de nucleótidos por lo general) y sus registros de calidad correspondientes en formato phred.

Con este formato se evita tener las calidades numéricas para cada base en un archivo diferente, con lo que se condensa la información. Cada secuencia es descrita en término de 4 Renglones. El primero de los cuales es conocido como identificador de la secuencia e inicia con una arroba (@). El segundo es propiamente la secuencia, por lo tanto, esta conformado solo de ATGC, el tercero repite el nombre de la secuencia, pero inicia con un símbolo +. El último renglón es la calidad en formato Phred.

```
@SRR11241254.156.1 156 length=185
ACTCAGTTTGCCTGTTTTACAGGTTCGCGACGTGCTCGTACGTGGCTTTGGAGACTCCGTGGAGGAGGTCTTATCAGAGGCACGTCAACATCTTAAAGATGGCACTTGTGGCTTAGTAGAAGTTGAAAAAGGCGTTTTCCTCAACTTGAACAGCCCTATGTGTTCATCAAACGTTCGGATGCTC
+SRR11241254.156.1 156 length=185
CCCCCGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGCGGGGGCFGGGGGGGGGGGEGGGGDGFGGGGGGGGGGGGGGGGGGGFFGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGCE7FGGGGGFGGGGGGGGGGGGFFCFFEGFGGGGGGGGFGFGGGGGGGGCGGGFGC
@SRR11241254.157.1 157 length=185
ACTCAGTTTGCCTGTTTTACAGGTTCGCGACGTGCTCGTACGTGGCTTTGGAGACTCCGTGGAGGAGGTCTTATCAGAGGCACGTCAACATCTTAAAGATGGCACTTGTGGCTTAGTAGAAGTTGAAAAAGGCGTTTTGCCTCAACTTGAACAGCCCTATGTGTTCATCAAACGTTCGGATGCTC
+SRR11241254.157.1 157 length=185
CCCCCGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGFGGGGGGGGGGGGGGGGGGGFGGGGGGGGGGGGGGGGGGGGGGFGGGGGGGGGGGGGGGGG
```
**Calidad Phred, código ASCII**

Las referencias [phred](https://en.wikipedia.org/wiki/Phred_quality_score) están asociadas a la confiabilidad de cada carácter de la secuencia, a partir de un valor Q = -10log P . El valor de calidad Q es un número entero de mapeo de P (la probabilidad de que la base en la secuencia sea incorrecta). La ecuación es el estándar de Sanger para evaluar la confianza de una base, también conocida como puntuación de calidad Phred. 

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_03.png)

Las calidades de un archivo `fastq` de *Illumina* pueden representarse con la codificación `Phred 33`, que está constituida por el conjunto de valores de la tabla de códigos [ASCII](https://www.ascii-code.com/) desde el valor 33 hasta el 73. 

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_04.png)

Esto es, desde el símbolo "!" hasta el símbolo "I" ya que el valor decimal para dichos símbolos va de 33 a 73. La codificación implica que a cada símbolo se le reste el valor 33, por lo que "!" representa un valor de 0 de calidad mientras que el símbolo "I" Representa un valor de 40 de calidad.

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_05.png)

01. Trabajarán con secuencias crudas del genoma de [Mycoplasma genitalium](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5745988/). Deberán obtenerlas identificando en el artículo, dónde están depositadas. Después deberán descargar un par de ellas y descomprimirlas de ser necesario. Finalmente usando awk o python, conviertan este archivo de `fastq` a `fasta`. **Reporten únicamente los comandos que utilizaron y suban el script al directorio de esta práctica.**
02. ¿Ambos archivos `fasta` tienen la misma cantidad de secuencias? **Reporten los comandos utilizados y ambos valores.**
03. Obtengan el promedio de la longitud de las secuencias para cada archivo creando una función de python qué haga la tarea. **Reporten únicamente los comandos que utilizaron y suban el script al directorio de esta práctica.**

## Parte III. __ / 20

**Análisis de Calidad de Secuencias**

Como ya se observó, cada tecnología presenta ciertos sesgos y fuentes de error. En resumen, dentro de las principales fuentes de error que se pueden llegar a observar en el análisis de calidad de las secuencias podemos mencionar los siguientes:

* Variación en la preparación biológica
* Contaminación
* Duplicados por PCR
* Recombinación
* Amplificación selectiva
* Secuenciación
* Error por sustitución de bases
* Inserciones y deleciones
* Calidad/confiabilidad de los datos generados

**FastQC**

`FastQC` es un software que tiene como objetivo proporcionar una manera simple de hacer algunas comprobaciones de control de calidad de datos de secuencias procedentes de metodologías de secuenciación de alto rendimiento. Proporciona un conjunto modular de análisis que se pueden utilizar para dar una impresión rápida de si sus datos tienen algún problema de calidad que deba ser tomado en cuenta antes de realizar cualquier análisis posterior.

Las principales funciones de FastQC son:

* Proporcionar una visión general y rápida que identifique en qué áreas puede haber problemas.
* Gráficos y tablas para evaluar rápidamente los datos.
* Exportación de los resultados a un archivo HTML.
* Operación fuera de línea para permitir la generación automática de informes sin ejecutar la aplicación de forma interactiva.

Excellent quality
![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_06.png)

Hmmmm....Ok.
![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_07.png)

**Revisando el [reporte](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)**

* Basic Statistics
* Per base sequence quality
* Per tile sequence quality
* Per sequence quality scores
* Per base sequence content
* Per sequence GC content
* Per base N content
* Sequence Length Distribution
* Sequence Duplication Levels
* Overrepresented sequences
* Adapter Content

*** 

01. Descargar [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/download.html) para linea de comandos y descomprimirlo con los comandos adecuados. Asignar permisos de ejecución al archivo fastqc y *volverlo ejecutable* en cualquier lugar de su computadora.
02. Crear un script de bash `fastqc_run.sh` como se indica a continuación -con los nombres de las secuencias pertenecientes a *Mycoplasma genitalium*- y correrlo.

```
#!/bin/bash

fastqc file_1.fastq file_2.fastq
``` 

03. Abrir el archivo `.html` en cualquier buscador. Realicen una breve descripción de la calidad de ambas lecturas. Describan si las lecturas ¿Son buenas o malas? ¿Por qué? ¿Cómo es el comportamiento de las calidades?
04. Calculen y reporten la cobertura del genoma tomando en cuenta que:

`covertura = (cantidad de lecturas*longitud de lecturas) / total del tamaño del genoma (bp)`

*La cantidad de lecturas es la suma de los archivos pareados*
*La longitud de lecturas es aquella obtenida en la PII.03*
*El tamaño del genoma (bp) debe ser el reportado para la especie*

## Parte IV. __ / 20

**Herramientas de limpieza**

Después de analizar los datos, es posible concluir que es necesario llevar a cabo una “limpieza de adaptadores”, eliminar secuencias sobrerrepresentadas o hacer cortes para el mejoramiento de las calidades. Existen múltiples herramientas para llevar a cabo esta limpieza de un archivo en formato fastq:

* Usando el script Clean_Adapter.pl (UUSMB)
* CutAdapt ( https://cutadapt.readthedocs.org/en/stable/ )
* Condetri ( https://github.com/linneas/condetri )
* ERNE-filter ( http://erne.sourceforge.net )
* FASTX-tools ( http://hannonlab.cshl.edu/fastx_toolkit/download.html )
* PRINTSEQ ( http://prinseq.sourceforge.net )
* Trimmomatic ( http://www.usadellab.org/cms/?page=trimmomatic )
* Trimgalore ( https://www.bioinformatics.babraham.ac.uk/projects/trim_galore/ )

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica03/tres_08.png)

**Remover organelos, sólo si se trata de información genómica**

Esto se puede realizar con un mapeador e información de un genoma mitocondrial o de cloroplasto de una especie filogenéticamente cercana. 

01. Descarguen las secuencias crudas de algún organismo modelo de su preferencia que tenga un genoma pequeño. **No suban los datos a GitHub, únicamente hagan una breve descripción de las características del organismo que eligieron**
02. Describan qué tecnología de secuenciación fue utilizada y de ser posible la referencia del artículo donde lo reportan. 
03. Calculen la cobertura de su genoma y el desglose que utilizaron para obtenerla.
04. Corran FastQC y suban a GitHub los archivos `.html` y discutan sobre las calidades de los archivos. 
05. ¿Cuál es el valor de phred que utilizan sus datos?
06. Planteen la estrategia adecuada para mejorar las calidades de sus secuencias de ser necesario. Ej. Cortar hasta cierta longitud de bases o phred, remover adaptadores, quitar secuencias sobrerrepresentadas, etc. Incluye el software que utilizarías para hacer esto. 

## Ejercicio extra

01. Realicen la limpieza de sus secuencias utilizando Trimmomatic. Para correrlo, creen un script para esa tarea ej. `trimmomatic_run.sh`. **Suban el script con los parámetros que utilizaron**
02. Vuelvan a correr FastQC y hagan la comparación de las lecturas antes y después de hacer los cortes. **Suban los nuevos archivos `html` a GitHub**. Discutan si mejoraron las calidades de sus secuencias.
