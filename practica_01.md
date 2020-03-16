# Genómica Computacional: Grupo 7075, Semestre 2020-2
## Práctica 01 - Herramientas bioinformáticas I (Entrega: 23.03.20/23:59)

**Indicaciones:** La práctica esta compuesta de cinco partes con ejercicios para repasar los comandos de bash que se vieron en clase, también el manejo de secuencias y algunos formatos particulares (`.faa`, `.fna` y `.fastqc`). Deberán resolver **individualmente** los ejercicios conforme se indique y anotar los comandos que se piden en un archivo `.txt`. Es responsabilidad del alumno subir el directorio correspondiente a su cuenta de [git](https://git-scm.com/) **(Parte IV)** y corroborar que se encuentre toda la información que se le pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a su cuenta de `git` antes de que cierre la asignación **(23.03.20/23:59)**. **Nota:** Si existen dudas al respecto de la práctica, favor de escribir a mi correo. Estaré respondiendo dudas a más tardar el lunes 23.03.20 a las 11:59.
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
 
## Parte IV. __ / 20

## Parte V. __ / 20

