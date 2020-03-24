# Genómica Computacional: Grupo 7075, Semestre 2020-2
## Práctica 01 - Herramientas bioinformáticas I (Entrega: 23.03.20/23:59)

**Indicaciones:** La práctica esta compuesta de cinco partes con ejercicios para repasar los comandos de bash que se vieron en clase, también el manejo de secuencias y algunos formatos particulares (`.fna`/`.fasta`, `.gff3`, `.faa` y `.fastqc`). Deberán resolver de manera **individual** los ejercicios conforme se indique y anotar los comandos que se piden en un archivo `.txt`. Es responsabilidad del alumno subir el directorio correspondiente a su cuenta de [git](https://github.com/) **(Parte IV)** y corroborar que se encuentre toda la información que se le pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a su cuenta de `git` antes de que cierre la asignación **(23.03.20/23:59)**. **Nota:** Si existen dudas al respecto de la práctica, favor de escribir a mi correo. Estaré respondiendo dudas a más tardar el lunes 23.03.20 a las 11:59.

***

## Parte I. __ / 20

Inicia la terminal y colócate en el directorio `computadora@usuario:~/home/` o `computadora@usuario:~/Desktop/`. Crea un directorio llamado `genomica_2020-2` y dentro de él crea un nuevo directorio de la siguiente manera (minúsculas): `inicialdelnombre+apellido_p01`. **Ejemplo:** Marisol Navarro -> `mnavarro_p01`. Cada que se te indiqué deberás anotar los comandos que utilizaste para realizar el ejercicio en un archivo denominado `comandos.txt` utilizando cualquier editor de texto plano (`emacs`, `sublime text`, `atom`, `vi`, `vim`, `nano`, `bloc de notas`, `notepad++`, etc). Este archivo deberás crearlo dentro del directorio con tu inicial y apellido.  

A partir de ahora, anotarás los comandos de los ejercicios marcados **(Ej. 2. ^)** en el archivo `comandos.txt` de la siguiente manera: 
```
# Comandos de la Práctica 01
# Nombre(s) Apellido(s)

# Parte I. 
[comando] [opciones] [argunmentos]
[comando] [opciones] [argunmentos]
[comando] [opciones] [argunmentos]
Respuesta 4: La organización...

# Parte II.
...
```
01. ^Indica qué tipo de shell tiene tu computadora. Si no recuerdas el comando, visita el siguiente sitio: [AskUbuntu](https://askubuntu.com/questions/590899/how-do-i-check-which-shell-i-am-using01).
02. ^Dentro del directorio que creaste con tu inicial y apellido, crea en una sola linea los siguientes directorios para la organización de tu proyecto bioinformático: `data/`, `filtered/`, `/raw_data`, `meta/`, `scripts/`, `figures/` y `archive/`. 
03. ^Mueve los archivos necesarios para obtener la siguiente esctructura: `data/filtered` y `data/raw_data`
04. ^Visita el siguiente repositorio y contesta ¿A qué se debe el nombre y la organización de los directorios que acabamos de crear? [BioinfinvRepo](https://github.com/u-genoma/BioinfinvRepro/blob/master/Unidad2/Unidad2_Organizacion_proyecto_bioinf.md)

## Parte II. __ / 20

Entra al directorio `scripts/`, crea un archivo de texto `delay.sh` y abrelo con un editor en la terminal para escribir las siguientes líneas de código: **Nota:** Antes de continuar, escribe lo siguiente `which bash`, si obtuviste `/bin/bash` continúa. De lo contrario, modifica la primer línea con lo que se imprimió `#!<ubicación_bash>`. Como notaste, los caracteres `#!` antes de la ubicación del programa bash, son indispensables, a estos se les conoce como [shebang](https://es.wikipedia.org/wiki/Shebang).

```
#!/bin/bash
echo "Después de la Parte I. necesito 1/2 minuto de descanso, que son exactamente 30 segundos."

echo "Ahora sí, con todo!"
```
01. ^Deseas ejecutar el script, por lo que tienes que darle al menos al usuario permisos de ejecución.
02. ^Verifica los permismos de `delay.sh`. Una vez que te aseguraste de que tiene permiso de ejecución, escribe lo siguiente `./delay.sh`.
03. ^Quieres que después de la segunda línea, haya una pausa de 30 segundos. Ya conoces el comando que permite *dormir* un proceso, si no recuerdas la unidad de tiempo que maneja, visita su manual `man <comando>`. Edita el archivo nuevamente insertanto el comando como se indica abajo. Observa lo que sucede y repórtalo junto con los comandos que usaste.

```
#!/bin/bash
echo "Después de la Parte I. necesito 1/2 minuto de descanso, que son exactamente 30 segundos."
< AQUÍ VA EL COMANDO QUE PERMITE DORMIR POR 30 SEGUNDOS >
echo "Ahora sí, con todo!"
```
04. ^Imagina que en lugar de poner 30, escribiste 300. Hazlo y ejecutalo en *background*. Como no queremos esperar 5 minutos, *mata* el proceso utilizando su PID.   

## Parte III. __ / 20

01. ^En esta parte, trabajarán con secuencias genómicas del Covid-19 ([coronavirus](https://www.youtube.com/watch?v=BtN-goy9VOY&feature=youtu.be)), el cuál actualmente (17.03.20) es considerado [pandemia](https://nextstrain.org/ncov). Para tener contexto de los datos, a continuación les anexo un video sobre la [estructura molecular del Covid-19](https://www.youtube.com/watch?v=I0AbpnFP1g8). Deberán elaborar un resumen de máximo 120 palabras y anexar al archivo `comandos.txt`. 

02. ^Seguir las siguientes indicaciones:
***
*Entrar a este vínculo de [NCBI](https://www.ncbi.nlm.nih.gov/genbank/sars-cov-2-seqs/) (National Institute of Health) sobre el Covid-19. Seguir los pasos para obtener los archivos:`sequence.fasta` y `sequence.gff3`.*

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_01.jpg)

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_02.jpg)
***
*Estando en el vínculo de RefSeq, sigue los pasos para obtener los archivos:`sequence_1.faa`,`sequence_2.faa` y `sequence_3.faa`. **Nota:** Es sumamente importante descargar los 3 archivos **por separado**. Si los archivos se van a las `Descargas/`, seguramente se les asignará un nombre como `sequence (1).fasta`, el cual para efectos prácticos deberás cambiar a `sequence_1.faa` **para cada archivo**. Además para esta parte, es necesario que describas -en `comandos.txt`- a grandes rasgos cuál es la función de la [SARS-CoV-2 spike ectodomain structure](https://www.annualreviews.org/doi/abs/10.1146/annurev-virology-110615-042301).*

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_03.jpg)

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_04.jpg)

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_05.jpg)

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_06.jpg)
***
*Una vez obtenidos los archivos anteriores, deberas regresar al vínculo de NCBI inicial y seguir los pasos para obtener los archivos:`sra_data.fasta.gz` y `sra_data.fastq.gz`.*

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_07.jpg)

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_08.jpg)

![alt text](https://github.com/solouli/genomica_2020-2/blob/master/practica/practica_01/ncbi_09.jpg)
***
03. ^Finalmente, deberás mover los siete archivos `sequence.fasta`, `sequence.gff3`, `sequence_1.faa`, `sequence_2.faa`, `sequence_3.faa`,  `sra_data.fasta.gz` y `sra_data.fastq.gz` al directorio `raw_data/` **(Ej. ~/Desktop/genomica_2020-2/mnavarro_p01/data/raw_data/)**

## Parte IV. __ / 20

01. ^Realiza las siete ligas simbólica suaves de todos los archivos que acaban de descargar al directorio `data/filtered`.
02. ^Mueve las ligas simbólicas suaves `sequence_1.faa`, `sequence_2.faa` y `sequence_3.faa` a un nuevo directorio llamado `proteins`.
03. ^Colócate dentro del directorio `proteins` y crea un nuevo archivo de texto llamado `glycoproteins.faa`. Obten las primeras dos líneas de los tres archivos y repórtalas -en `comandos.txt`-. 
04. ^Sin copiar y pegar (Crtl+c, Ctrl+p) en un editor, redirecciona el contenido de las tres secuencias al archivo `glycoproteins.faa` de tal forma que obtengas el orden siguiente.
```
>pdb|6VYB|A Chain A, spike glycoprotein
MGILPSPGMPALLSLVSLLSVLLMGCVAETGTQCVNLTTRTQLPPAYTNSFTRGVYYPDKVFRSSVLHST
QDLFLPFFSNVTWFHAIHVSGTNGTKRFDNPVLPFNDGVYFASTEKSNIIRGWIFGTTLDSKTQSLLIVN
...
>pdb|6VYB|B Chain B, spike glycoprotein
MGILPSPGMPALLSLVSLLSVLLMGCVAETGTQCVNLTTRTQLPPAYTNSFTRGVYYPDKVFRSSVLHST
QDLFLPFFSNVTWFHAIHVSGTNGTKRFDNPVLPFNDGVYFASTEKSNIIRGWIFGTTLDSKTQSLLIVN
...
>pdb|6VYB|C Chain C, spike glycoprotein
MGILPSPGMPALLSLVSLLSVLLMGCVAETGTQCVNLTTRTQLPPAYTNSFTRGVYYPDKVFRSSVLHST
QDLFLPFFSNVTWFHAIHVSGTNGTKRFDNPVLPFNDGVYFASTEKSNIIRGWIFGTTLDSKTQSLLIVN
...
```
05. ^Regresa al directorio anterior. Usa el comando adecuado para ver en la terminal las primeras 5 líneas de los archivos `sequence.fasta` y `sra_data.fasta.gz`. Repórtalas -en `comandos.txt`-.
06. ^Ya que reportasete las primeras 5 líneas de los archivos, puedes notar que el nombre/header de las secuencias esta delimitado por el caracter '>'. Cuenta cuántos headers tienes y reporta el número -en `comandos.txt`- recuerda usar pipes |. **Nota:** Como te habrás dado cuenta uno de los archivos tiene una extensión `.gz` o `gunzip` lo que quiere decir que está comprimido. Si abres el archivo con los comandos `less`, `more` o `cat` te darás cuenta que está en binario. Hazlo. Para poder acceder a él sin necesidad de descomprimirlo, puedes usar el siguiente ejemplo `zless sra_data.fasta.gz | <comando> ...`. 
07. ^De igual manera abre el archivo [.fastq](https://en.wikipedia.org/wiki/FASTQ_format) `sra_data.fastq.gz` y obten las primeras 12 líneas. Repórtalas -en `comandos.txt`-. Observa el patrón e identifica qué caracter te podría ayudar a obtener un conteo de las secuencias. Utiliza el patrón que elegiste para contar la cantidad de secuencias que hay y escríbelo.
08. ^Explica la diferencia entre los formatos `.faa`, `.fastqc` y `fasta`. ¿Las secuencias son de nucleótidos (ATCG) o de aminoácidos? ¿Cómo explicas la diferencia entre el número de lecturas de los archivos `.fasta`? ¿Qué es el formato `.fastqc` y ¿A qué corresponde la información de las líneas en el formato `fastqc`?.  
09. ^Abre el archivo [.gff3](https://www.ensembl.org/info/website/upload/gff3.html) de las siguientes formas `less sequence.gff3` y `less -S sequence.gff3`. Observa las diferencias. Repórtalas en un enunciado. 
10. ^Filtra la tercera columna por la categoría `gene` y reporta la cantidad de genes que tiene el archivo.   

## Parte V. __ / 20

Nuevamente visita la Unidad 2 del siguiente repositorio [BioinfinvRepo](https://github.com/u-genoma/BioinfinvRepro/blob/master/Unidad2/Unidad2_Organizacion_proyecto_bioinf.md) y realiza únicamente los ejercicios que se indican en este documento de `.md`. Leer las siguientes secciones del repo:

* Markdown
* git
* Github

01. Una vez que leyeron las secciones anteriores, ceen un respaldo de los ejercicios que hicieron con anterioridad y ahora sí, suban la carpeta genomica_2020-2 (que contiene todos sus ejercicios resueltos) a su repositorio. Corroboren que todos sus archivos estén disponibles desde su git. Consideren que aquellos directorios que se encuentran vacíos, no apareceran. 
02. En la próxima sesión de laboratorio vamos a ocupar comandos de git, así que lean con detenimiento y si lo necesitan repasen con los ejercicios que ahí se sugieren.

## Fin de la práctica :)
