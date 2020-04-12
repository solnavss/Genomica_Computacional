# Genómica Computacional: Grupo 7075, Semestre 2020-2
## Práctica 02 - Análisis de datos de Secuenciación Masiva (Entrega: 20.04.20/23:59)

**Indicaciones:** La práctica esta compuesta de cinco partes con ejercicios para repasar algunos comandos de bash, teoría sobre el manejo de secuencias, algunos formatos particulares (`.fna`/`.fasta`, `.gff3`, `.faa` y `.fastqc`) e instalación de software específico. Deberán resolver **en equipos máximo de 3 personas** los ejercicios conforme se indique y anotar los comandos que se piden en un archivo tipo [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) `.md`. Es responsabilidad de los alumnos subir el directorio correspondiente a su cuenta de [git](https://github.com/) y corroborar que se encuentre toda la información que se les pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a su cuenta de `git` antes de que cierre la asignación **(20.04.20/23:59)**. **Nota:** Si existen dudas al respecto de la práctica, favor de escribir a mi correo. **Estaré respondiendo dudas a más tardar el lunes 20.04.20 a las 11:59.**

***

## Parte I. __ / 20

**Objetivo:** En esta práctica, se espera que los alumnos revisen los flujos de datos posibles desde la salida del secuenciador, hasta una aplicación final. Los distintos formatos con los que tradicionalmente se manejan los datos y cómo se realiza el análisis primario.

01. ^En su directorio `genomica_2020-2` un integrante del equipo deberá crear uno nuevo de la siguiente manera (minúsculas): `nombredelequipo+_p02`. **Ejemplo:** Equipo: dinamita -> `dinamita_p02`. 
02. ^Cada que se indique **(Ej. 1. ^)** deberán anotar los comandos que utilizaron para realizar el ejercicio en un archivo denominado `comandos_p02.md` utilizando cualquier editor de texto plano (`emacs`, `sublime text`, `atom`, `vi`, `vim`, `nano`, `bloc de notas`, `notepad++`, etc). Este archivo deberán crearlo dentro del directorio de su equipo.  
03. En el nuevo directorio, tendrán que colaborar todos los integrantes del equipo con un flujo de trabajo de git. Es decir, el integrante que creo el directorio deberá subirlo a git y los demás deberán clonar el repositorio solicitando permiso de colaboración. 
04. En el nuevo directorio deberán crear los directorios correspondientes: `data/`, `filtered/`, `/raw_data`, `meta/`, `scripts/`, `figures/` y `archive/`. 

Los comandos de los ejercicios marcados **(Ej. 1. ^)** en el archivo `comandos_p02.md` deberán seguir el siguiente formato : 

```
# Comandos de la Práctica 02
## Nombre del equipo
## Integrante 1: Nombre(s) Apellido(s)
## Integrante 2: Nombre(s) Apellido(s)
## Integrante 3:Nombre(s) Apellido(s)

## Parte I. 
01. [comando] [opciones] [argumentos]
02. [comando] [opciones] [argumentos]

# Parte II.
...
```
## Parte II. __ / 20

**Flujo de datos de Secuenciación Masiva**

Las plataformas de `Illumina` generan por default archivos en formato `.fastq`. Sin embargo, plataformas como `454` y `Ion Torrent` generan archivos en formato `.sff` de manera nativa, aunque es posible convertir este formato a `.fastq`. El análisis de calidad de las secuencias generadas en la corrida, se lleva a cabo sobre archivos en formato `.fastq`.

Cuando los archivos `.fastq` son alineados contra un *genoma de referencia*, este último debe estar en formato `.fasta`. Si en cambio lo que se realiza es un ensamblado de novo, el resultado del ensamble también se presenta en formato `.fasta`.

El resultado de llevar a cabo un proceso de alineamiento contra un genoma de referencia usando alineadores como `Bowtie2`, `Smalt` o `BWA`, será un archivo en formato `.sam`, que se puede convertir a un archivo en formato `.bam` (binario, mucho más compacto) o si se quiere mayor compresión, el `.bam` se puede convertir en un archivo con formato `.cram`.

A partir de los archivos mencionados anteriormente es posible corroborar la localización de "features" o anotaciones típicamente usando archivos en formato `.gff3` o `.bed` en conjunto con los archivos `.bam`. También desde el archivo `.bam` se puede realizar una búsqueda de variantes y obtener un archivo en formato `.vcf` por sus iniciales "Variant Call Format".

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_01.png)

***

01. Vean el siguiente video sobre tecnologías de [secuanciación masiva](https://www.youtube.com/watch?v=jFCD8Q6qSTM&list=PLTt9kKfqE_0Gem8hIcJEn7YcesuuKdt_n&index=2&t=441s) (NGS) y elaboren una tabla comparativa de las características de *algunas* de las [tecnologías](https://en.wikipedia.org/wiki/DNA_sequencing) por [generación](https://www.intechopen.com/books/next-generation-sequencing-advances-applications-and-challenges/next-generation-sequencing-an-overview-of-the-history-tools-and-omic-applications). Anoten las referencias que hayan utilizado. 

| Plataforma/compañía          | Longitud de reads (pb)  | # reads x run  | Tiempo   | Costo x 10^6 bases  | Error (%)   | Química                    |
| ------------------------------------ |:-------------------------------:| ------------------:| -----------:| ----------------------------:| --------------:| ---------------------------:|
| Primera generación             |                                       |                       |               |                                    |                   |                                  |
| Sanger/Life Technologies    | 800                                | 1                    | 2 hrs      | 2400                           | 0.3             | Dideoxy terminator   |
| Segunda generación           |                                       |                       |               |                                    |                   |                                   |   
| Tercera generación              |                                       |                       |               |                                    |                   |                                   |

## Parte III. __ / 20

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

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_02.png)

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

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_03.png)

Las calidades de un archivo `fastq` de *Illumina* pueden representarse con la codificación `Phred 33`, que está constituida por el conjunto de valores de la tabla de códigos [ASCII](https://www.ascii-code.com/) desde el valor 33 hasta el 73. 

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_04.png)

Esto es, desde el símbolo "!" hasta el símbolo "I" ya que el valor decimal para dichos símbolos va de 33 a 73. La codificación implica que a cada símbolo se le reste el valor 33, por lo que "!" representa un valor de 0 de calidad mientras que el símbolo "I" Representa un valor de 40 de calidad.

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_05.png)

**Formatos de alineamiento: SAM / BAM y CRAM**

Cuando un archivo `fastq` ha sido alineado contra un genoma de referencia, es posible obtener el resultado de este alineamiento en un archivo con formato `sam`.

SAM significa "Sequence Alignment / Map". Se trata de un formato del texto delimitado por tabuladores que consiste en una sección de cabecera, que es opcional, y una sección de alineamientos. La cabecera, si está presente, antecede a la información de los alineamientos. Las líneas de la cabecera empiezan con "@", mientras que las líneas de los alineamientos no. Cada línea de los alineamientos tiene [11 campos](https://galaxyproject.org/tutorials/ngs/) obligatorios con la información esencial de alineación como la posición de mapeo y número variable de campos opcionales para obtener información específica flexibles o del alineador.

`<QNAME>  <FLAG> <RNAME> <POS> <MAPQ> <CIGAR> <MRNM> <MPOS> <ISIZE> <SEQ> <QUAL>`

Con este formato, logramos tener en una sola línea la información tanto de la secuencia como de su posición en una referencia.

`ERR458493 .552967 16 chrI 140 255 12 M61232N37M2S * 0 0 CCACTCGTTCACCAGGGCCGGCGGGCTGATCACTTTATCGTGCATCTTGGC BB?HHJJIGHHJIGIIJJIJGIJIJJIIIGHBJJJJJJHHHHFFDDDA1+B NH:i:1 HI:i:1 AS:i:41 nM:i:2`

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_06.png)

Un archivo BAM, contiene la misma información que un archivo SAM pero está comprimido en el formato BGZF. Los archivos BGZF permiten accesos aleatorios a través del índice del archivo BAM.

El formato [CRAM](https://samtools.github.io/hts-specs/CRAMv3.pdf) fue diseñado por el EBI (European Bioinformatic Institute) para reducir el espacio necesario y almacenar todas las secuencias que requieren ser archivadas. Son los archivos con mayor capacidad de compresión actualmente.

**Formato de anotación: GFF**

Un archivo `gff` (“General Feature Format”), es útil para contextualizar en las secuencias nucleotídicas, información genómica como puede ser la ubicación de un gen en dicha secuencia. GFF es un formato propuesto como un protocolo para transferir fácilmente información de los genes de un organismo.

*Características:*

* Archivo de texto: los campos están en una sola línea y separados por tabuladores 

` <seqname> <source> <feature> <start> <end> <score> <strand> <frame>`

```
<seqname>: Nombre de la secuencia
<source>: La fuente de la secuencia
<feature>: Tipo de secuencia (gen, CDS, etc.)
<start>: Posición de inicio de la secuencia
<end>: Posición final de la secuencian
<score>: Calificación de la secuencia
<strand>: Dirección de la secuencia
<frame>: Marco de referencia de la secuencia
[attributes]: Otros atributos definidos por el usuario
[comments]: Cualquier comentario acerca de la secuencia
```

**Formato de llamado de variantes: VCF**

Un archivo `vcf` (Variant Call Format) tiene un formato que almacena de una manera comprimida información sobre variantes en las secuencias de genes. Contiene líneas de metainformación en las líneas de la cabecera, y luego cada línea de datos contiene información acerca de una posición en el genoma. El formato también tiene la capacidad de contener información sobre el [genotipo](https://samtools.github.io/hts-specs/VCFv4.2.pdf) de las muestras para cada posición. 

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_07.png)

***

01. ^Creen una *liga simbólica suave* del archivo `sra_data.fastq.gz`, dentro del directorio del equipo ej.  `genomica_2020-2/dinamita_p02/data/filtered`. Descomprimanlo utilizando el comando `gunzip -c sra_data.fastq.gz` para conservar el archivo original comprimido. Usando awk conviertan este archivo de `fastq` a `fasta`.
02. ^Filtren únicamente el dato de la longitud de las lecturas del archivo `fasta` usando los comandos correspondientes y creen un nuevo archivo de texto con todas las longitudes separadas por coma. Posteriormente obtén el promedio de las secuencias. 
03. Un string de CIGAR de 36M significa que 36 posiciones de la secuencia hacen "match" con el genoma de referencia. Suponiendo que el genoma de referencia tiene un fragmento con la secuencia que se muestra a continuación ¿Cómo se vería el alineamiento? y ¿Cuál sería su CIGAR string?

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_08.png)

Secuencia de referencia:
`AGCATGTTAGATTAGATAGCTGTGCTA...`

Secuencia a comparar:
`TTAGATAAAGGATACTG`
    
04. ^Creen una *liga simbólica suave* del archivo `sequence.gff3`, dentro del directorio del equipo ej.  `genomica_2020-2/dinamita_p02/data/filtered`. Utilizando los comandos correspondientes, reporten para la columna tres cuántos reportes hay para cada una de las categorías.

## Parte IV. __ / 20

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
![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_09.png)

Hmmmm....Ok.
![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_02/dos_09.png)

