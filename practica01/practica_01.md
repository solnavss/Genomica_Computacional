# Genómica Computacional, 
## Práctica 01 - Manejo de datos de secuenciación masiva (Bash)

**Indicaciones:** La práctica esta compuesta de cuatro partes con ejercicios para repasar los comandos de Bash que se vieron en clase, también el manejo de secuencias y algunos formatos particulares (`.fna`/`.fasta`, `.faa`,`.gff3` y `.fastq`). Deberán resolver de manera **individual** los ejercicios y anotar los comandos, líneas de código y/o outputs que se piden en un archivo llamado `comandos_p01.txt` utilizando cualquier editor de texto plano (`emacs`, `sublime text`, `atom`, `vi`, `vim`, `nano`, `bloc de notas`, `notepad++`, etc).

**Nota:** Es responsabilidad del alumno subir el directorio correspondiente a su cuenta de [GitHub](https://github.com/) y corroborar que se encuentre toda la información que se le pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a su cuenta de `GitHub` antes de que cierre la asignación.  

## Parte I. __ / 20

Inicia la terminal y colócate en el directorio `computadora@usuario:~/home/` o `computadora@usuario:~/Desktop/`. Crea un directorio llamado `GenomicaComputacional` (sin tilde) y dentro de él crea un nuevo directorio como se indica a continuación (minúsculas): `inicialdelnombre+apellido_p01`. **Ejemplo:** Marisol Navarro -> `mnavarro_p01`. 

Crea el archivo `comandos_p01.md` dentro del directorio con tu inicial y apellido. Recuerda que debe contener los comandos, líneas de código y/o outputs que se piden para resolver cada ejercicio en [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). El archivo deberá seguir el siguiente formato: 

```
# Comandos de la Práctica 01
## Nombre(s) Apellido(s)

# Parte I. 

**Respuesta 1:**

/bin/bash 

**Respuesta 2:**

[comando] [opciones] [argumentos]

**Respuesta 3:**

[comando] [opciones] [argumentos]

**Respuesta 4:**

La organización...

# Parte II.
...
```

01. Indica qué tipo de shell tiene tu computadora. Si no recuerdas el comando, recuerda que posiblemente alguien ya preguntó eso alguna vez. Puedes visitar el siguiente sitio: [AskUbuntu](https://askubuntu.com/questions/590899/how-do-i-check-which-shell-i-am-using01).
02. Un proyecto bioinformático que se quiere publicar debe estar bien organizado y documentado para que éste se vuelva reproducible. Colócate dentro del directorio que creaste con tu inicial y apellido. Ahora crea en una sola linea los siguientes directorios para la organización de tu proyecto bioinformático: `data/`, `filtered/`, `raw_data/`, `meta/`, `scripts/`, `figures/` y `archive/`. 
03. Mueve los archivos necesarios para obtener la siguiente esctructura: `data/filtered` y `data/raw_data`.
04. Visita el siguiente repositorio y contesta ¿A qué se debe el nombre y la organización de los directorios que acabamos de crear? [BioinfinvRepo](https://github.com/u-genoma/BioinfinvRepro/blob/master/Unidad2/Unidad2_Organizacion_proyecto_bioinf.md)

## Parte II. __ / 20

Entra al directorio `scripts/`, crea un archivo de texto `delay.sh` y abrelo con un editor de texto desde la terminal para escribir las siguientes líneas de código: **Nota:** Antes de continuar, verifica que tu ruta de bash es la misma que en el cuadro de código usando `which bash`, si obtuviste `/bin/bash` continúa. De lo contrario, modifica la primer línea con lo que se imprimió `#!<ubicación_bash>`. Como notaste, los caracteres `#!` antes de la ubicación del programa bash, son indispensables, a estos se les conoce como [shebang](https://es.wikipedia.org/wiki/Shebang).

```
#!/bin/bash
echo "Después de la Parte I. necesito un descanso de exactamente 30 segundos."
```

01. Deseas ejecutar el script, por lo que tienes que darle (al menos) al usuario permisos de ejecución.
02. Verifica los permismos de `delay.sh`. Una vez que te aseguraste de que tiene permiso de ejecución, ahora puedes ejecutarlo de alguna de las dos formas que vimos en clase.
03. Quieres que después de la segunda línea, haya una pausa de 30 segundos. Ya conoces el comando que permite *dormir* un proceso, si no recuerdas la unidad de tiempo que maneja, visita su manual `man <comando>`. Edita el archivo tomando como guía el siguiente cuadro de código. No olvides reportar el comando que agregaste. 

```
#!/bin/bash
echo "Después de la Parte I. necesito un descanso de exactamente 30 segundos."
# < AQUÍ VA EL COMANDO QUE PERMITE DORMIR POR 30 SEGUNDOS >
echo "Ya puedo continuar!"
```

04. Imagina que en lugar de poner 30, escribiste 300. Hazlo y ejecutalo en *background*. Como no queremos esperar 5 minutos, *cancela* el proceso utilizando su PID.

## Parte III. __ / 20

En esta parte, trabajarás con secuencias genómicas del virus SARS-CoV-2 que provoca la enfermedad Covid-19. Si necesitas un contexto general de los datos, también puedes consultar el siguiente [video sobre Covid-19](https://www.youtube.com/watch?v=BtN-goy9VOY&feature=youtu.be). También aprenderás a obtener datos de secuencias biológicas. 

01. Elabora un resumen de 120 palabras sobre la siguiente conferencia respecto a la [estructura molecular del SARS-Cov-2](https://www.youtube.com/watch?v=I0AbpnFP1g8). También puedes apoyarte en el siguiente [texto](https://www.nytimes.com/interactive/2020/04/03/science/coronavirus-genome-bad-news-wrapped-in-protein.html) publicado por The New York Times. El resumen deberá estar escrito en un archivo `SarsCov-2.txt` dentro del directorio creado para la práctica Ej. `~/home/GenomicaComputacional/mnavarro_p01/meta`

02. Indicaciones para descargar archivos:

Entra al vínuclo del [National Center for Biotechnology Information](https://www.ncbi.nlm.nih.gov/) (NCBI). Sigue los pasos para obtener los archivos:`sequence.fasta` y `sequence.gff3`. Renombrar los archivos usando el comando adecuado `sequence.fasta` -> `sarscov2_genome.fasta` y `sequence.gff3` ->  `sarscov2_genome.gff3`.

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica01/ncbi_01.png)

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica01/ncbi_02.png)

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica01/ncbi_03.png)

Vuelve a entrar al vínuclo del [National Center for Biotechnology Information](https://www.ncbi.nlm.nih.gov/) (NCBI). Sigue los pasos para obtener uno por uno los archivos en formato FASTA correspondientes a Chain C, SARS-CoV-2 spike glycoprotein, Chain B, SARS-CoV-2 spike glycoprotein y Chain A, SARS-CoV-2 spike glycoprotein: `sequence.fasta`, `sequence (1).fasta` y `sequence (2).fasta`. Renombrar los archivos usando el comando adecuado `sequence.fasta` -> `splike_c.faa`, `sequence (1).fasta` -> `splike_b.faa` y `sequence (2).fasta` -> `splike_a.faa`. 

Además para esta parte, es necesario que crees en tu directorio `/meta` un archivo `SarsCov-2_Spike.txt` donde describas a grandes rasgos cuál es la función de la [SARS-CoV-2 spike ectodomain structure](https://www.annualreviews.org/doi/abs/10.1146/annurev-virology-110615-042301).

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica01/ncbi_04.png)

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica01/ncbi_05.png)

![alt text](https://github.com/solouli/Genomica_Computacional/blob/master/practica01/ncbi_06.png)

***

Una vez obtenidos los archivos anteriores, también descarga los archivos `SRR10971381_R1.fastq.gz`, `SRR10971381_R2.fastq.gz` y `sarscov2_assembly.fasta.gz` disponibles en `GitHub`. 

Finalmente mueve los **ocho** archivos `sarscov2_genome.fasta`, `sarscov2_genome.gff3`, `splike_c.faa`, `splike_b.faa`, `splike_a.faa`, `SRR10971381_R1.fastq.gz`, `SRR10971381_R2.fastq.gz` y `sarscov2_assembly.fasta.gz` a tu directorio `data\raw_data`.

## Parte IV. __ / 20

01. Realiza tres ligas simbólicas suaves de los archivos `splike_c.faa`, `splike_b.faa` y `splike_a.faa` en el directorio `data/filtered`.
02. Dentro de `data/filtered` crea un nuevo archivo llamado `glycoproteins.faa`. 
03. Obten la primera línea de los tres archivos y repórtalas (en `comandos_p01.md`). 
04. Usando el comando adecuado, redirecciona el contenido de los tres archivos `splike_*.faa` a `glycoproteins.faa` de tal forma que obtengas el orden siguiente.

```
>pdb|6VYB|A Chain A, spike glycoprotein
MGILPSPGMPALLSLVSLLSVLLMGCVAETGTQCVNLTTRTQLPPAYTNSFTRGVYYPDKVFRSSVLHST
QDLFLPFFSNVTWFHAIHVSGTNGTKRFDNPVLPFNDGVYFASTEKSNIIRGWIFGTTLDSKTQSLLIVN
...(resto de la proteína)
>pdb|6VYB|B Chain B, spike glycoprotein
MGILPSPGMPALLSLVSLLSVLLMGCVAETGTQCVNLTTRTQLPPAYTNSFTRGVYYPDKVFRSSVLHST
QDLFLPFFSNVTWFHAIHVSGTNGTKRFDNPVLPFNDGVYFASTEKSNIIRGWIFGTTLDSKTQSLLIVN
... (resto de la proteína)
>pdb|6VYB|C Chain C, spike glycoprotein
MGILPSPGMPALLSLVSLLSVLLMGCVAETGTQCVNLTTRTQLPPAYTNSFTRGVYYPDKVFRSSVLHST
QDLFLPFFSNVTWFHAIHVSGTNGTKRFDNPVLPFNDGVYFASTEKSNIIRGWIFGTTLDSKTQSLLIVN
... (resto de la proteína)

```

05. Mueve lo archivos `data/raw_data/splike_*.faa` al directorio `archive/`. ¿Qué pasó con las ligas simbólicas suaves?. 
**Nota:** Como te habrás dado cuenta algunos de los archivos que descargaste tienen una extensión `.gz` lo que quiere decir que estan comprimidos. Si abres el archivo con los comandos `less`, `more` o `cat` te darás cuenta que estan en binario. Inténtalo. Para poder acceder a ellos sin necesidad de descomprimirlos, puedes usar el siguiente ejemplo `zless archivo.gz | <comando> | <comando>`. 
06. Dentro del directorio `data/raw_data`, explora los archivos `sarscov2_genome.fasta` y `sarscov2_assembly.fasta.gz`. Ya que los exploraste. usa el comando adecuado para ver en la terminal las primeras 3 líneas de los archivos. Repórtalas. ¿Cómo explicas la diferencia entre el número de lecturas de los archivos `.fasta`?
07. Pudiste notar en los archivos que el nombre/header de las secuencias esta delimitado por el caracter '>'. Cuenta cuántos headers tienen ambos y reporta el número (recuerda usar pipes). 
08. De igual manera abre el archivo [.fastq](https://en.wikipedia.org/wiki/FASTQ_format) `SRR10971381_R2.fastq.gz` y obten las primeras 12 líneas. Repórtalas. Observa el patrón e identifica qué caracter te podría ayudar a obtener un conteo de las secuencias. Utiliza el patrón que elegiste para contar la cantidad de secuencias que hay. Repórtalo.
09. Explica la diferencia entre los formatos `.faa`, `.fastqc` y `fasta`: ¿Las secuencias hacen referencia a nucleótidos o aminoácidos? ¿A qué corresponde la información de las líneas en el formato `fastqc`?.  
10. Abre el archivo [.gff3](https://www.ensembl.org/info/website/upload/gff3.html) de las siguientes formas `less sequence.gff3` y `less -S sarscov2_genome.gff3`. Observa las diferencias. Repórtalas en un enunciado. 
11. Filtra el tercer campo del archivo `sarscov2_genome.gff3` por la categoría `gene` y reporta la cantidad de genes que tiene el archivo. ¿A qué corresponde el campo tres? ¿Cuál es la diferencia entre `gene` y `CDS` de acuerdo a la información proporcionada por la documentación del campo 3? 

**12. En tu cuenta de GitHub sube tu directorio GenomicaComputacional como un nuevo repositorio. Asegúrate de que contenga toda la información de tu práctica.**

## Ejercicio extra

01. Cambia al directorio `figures/` y crea una liga simbólica suave del archivo `sarscov2_genome.gff3`
02. Identifica cuántas categorías distintas existen en el campo 3 y cuántas veces aparecen. Redirecciona la salida a un archivo que se llame `barplot_data.txt`
03. Limpia tu archivo `barplot_data.txt` de tal forma que sólo te queden las categorías que corresponden al campo 3.
04. Crea un script de python `gff_barplot.py` con los datos que obtuviste. Asegúrate de que el shebang corresponda a la ubicación de python en tu computadora. 
05. Guarda la figura que obtuviste en `figures/`

```
#!/Users/solouli/opt/anaconda3/bin/python

import numpy as np
import matplotlib.pyplot as plt
from textwrap import wrap

# Crea el dataset con << tus datos obtenidos en barplot_data.txt >>
frecuencias = [3, 12, 5, 18, 45]
categorias = ['Categoría A', 'Categoría B', 'Categoría C', 'Categoría D', 'Categoría E']
categorias = [ '\n'.join(wrap(l, 11)) for l in categorias]

y_pos = np.arange(len(categorias))

# Gráfico de barras
plt.bar(y_pos, frecuencias)

# Nombres en el eje-x
plt.xticks(y_pos, categorias)

# Mostrar la gráfica
plt.show()
```
## Fin de la práctica :)
