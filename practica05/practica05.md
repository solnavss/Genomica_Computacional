# Práctica 5. Análisis de Datos Genómicos, Parte III: Evolución e Inferencia Filogenética
## Licenciatura en Ciencias de la Computación, Facultad de Ciencias - UNAM

**Indicaciones:** La práctica esta compuesta de cuatro partes con ejercicios para repasar los temas vistos en clase. La práctica se deberán resolver de manera **individual**. Es responsabilidad del alumno subir el directorio correspondiente a la práctica a su cuenta de [git](https://github.com/) y corroborar que se encuentre toda la información que se le pidió. Así mismo, tendrán que enviar vía [Google Classroom](https://classroom.google.com/) la liga a su cuenta de `git` antes de que cierre la asignación.

***

## Parte I. __ / 20

1. *Comparación de secuencias e identificación de mutaciones.*

Un estudiante de la Facultad de Ciencias está estudiando neurodesarrollo. A partir de sus estudios encontró una región en el genoma de su organismo de estudio que parece estar involucrada en este fenómeno. Dicho estudiante ha aislado cuatro mutantes de las cuales una muestra un nulo efecto en el fenotipo, otra muestra un leve efecto y las dos muestran un efecto letal en el fenotipo. Utilizando las secuencias del archivo `pregunta1.fasta` ayuda al estudiante con las siguientes preguntas. **Nota:** En el archivo WT indica la secuencia de referencia (silvestre) y el resto de las secuencias, identificadas como MUTX son las secuencias mutantes.

1.	¿Cuál es el organismo que analiza el estudiante hipotético? 
2.	Revisando fuentes adicionales, ¿existe evidencia previa de que ésta región del genoma esté involucrada en el neurodesarrollo? 
3.	¿Cuántas mutaciones existen entre cada una de las secuencias mutantes respecto a la secuencia silvestre?
4.	Para cada una de las mutaciones identificadas en las secuencias mutantes, clasificarlas como (i) sustitución, (ii) deleción o (iii) adición. 
5.	Para cada una de las secuencias, reporta cada una de las mutaciones de la forma: **i.**	En el caso de sustituciones: XYZ, donde X es el nucleótido original, Y es la posición de la mutación y Z el nucleótido producto de la mutación. Por ejemplo: C21T indica que la citosina en la posición 21 fue reemplazada a una timina. **ii.**	En el caso de deleciones: ΔXY donde X es el nucleótido original y Y es la posición de la mutación. Por ejemplo ΔC21 indica que se eliminó la citosina en la posición 21. 
6.	¿Hay evidencia de que WT sea una secuencia codificante? Justifica tu respuesta. Si es así, ¿a qué gen corresponde? 
7.	Si la respuesta a la pregunta 6 es positiva, clasifica las mutaciones identificadas en cada secuencia en (i) sinónimas, (ii) no sinónimas, (iii) corrimiento del marco de lectura y (iv) sin sentido. 
8.	Si la respuesta a la pregunta 6 es positiva, reporta cada una de las mutaciones no sinónimas de la forma: XYZ donde X es el aminoácido original, Y la posición del aminoácido en la proteína y Z el aminoácido producto de la mutación. Ejemplo: A53Y indica que el aminoácido alanina en la posición 53 fue reemplazado por el aminoácido tirosina. 
8.	Si la respuesta a la pregunta 6 es positiva y basado en el tipo de mutación (sinónima, no sinónima, corrimiento del marco de lectura o sin sentido), ¿cuál considerarías que es el efecto de cada una de las secuencias mutantes en el fenotipo (un nulo, un leve y dos letales)?

## Parte II. __ / 20

2. *Inferencia filogenética y relaciones de parentesco.*

El archivo `pregunta2.fasta` contiene las secuencias de la proteína citocromo b obtenida de las mitocondrias para 32 primates y además una de ratón, este último como grupo externo. 

1.	Describe brevemente ¿qué es? y ¿cuál es la función de la proteína citocromo b?. 
2.	A partir de consultar fuentes de información adicionales y utilizando los nombres que se encuentren en los encabezados de cada una de las secuencias, clasifica a los organismos para los cuales se proporcionan secuencias en: lemuriformes, tarsiiformes, monos del nuevo mundo, monos del viejo mundo y hominoides. 
3.	A partir de consultar fuentes de información adicionales, ¿cuáles es el rasgo característico de los hominoides? 
4.	Utilizando [IQ-TREE](http://iqtree.cibiv.univie.ac.at/), infiere el árbol filogenético de máxima verosimilitud y visualiza el resultado en [iTOL](https://itol.embl.de/) o el paquete [ape](http://www.phytools.org/Cordoba2017/ex/2/Intro-to-phylogenies.html) de R utilizando a *Mus musculus* para enraizar el árbol. 
5.	Según el reporte generado por IQ-TREE, ¿cuál es el modelo utilizado para inferir la filogenia? 
6.	Según la filogenia obtenida, los organismos incluídos en este análisis se agrupan de acuerdo a la clasificación de la pregunta 2. 
7.	¿Cuál es el organismo o los organismos más cercanamente relacionado al humano? ¿Cuál es el nombre común de este o estos organismos? 
8.	¿Cuál dirías que es el linaje más basal dentro del grupo de los primates? 

## Parte III. __ / 20

3. *Integración de filogenias moleculares y rasgos fenotípicos.* 

Previo a la inferencia filogenética utilizando secuencias moleculares, los caracteres morfológicos eran utilizados para estimar las relaciones de parentesco entre organismos. Aunque los resultados obtenidos a partir de ambos enfoques pueden discernir, considerar ambos es importante para vislumbrar las historias evolutivas. En los archivos `pregunta3_nt.fasta` y `pregunta3_aa.fasta` se encuentran las secuencias de nucleótidos y aminoácidos, respectivamente (las secuencias de aminoácidos corresponden a las secuencias traducidas de las secuencias de nucleótidos), obtenidas de miembros de la familia Volvocaceae. Dentro de esta familia se encuentra el género *Volvox*, el cual es contiene organismos considerados como multicelulares. Tomando en cuenta los caracteres morfológicos, se ha considerado clásicamente que todos los miembros del género *Volvox* componen un grupo filogenético dentro de la familia Volvocaceae y que por lo tanto la multicelularidad en esta familia ha emergido una única vez. Utilizando las secuencias de estos archivos responde: 

1.	Utilizando únicamente una de las secuencias, ¿a qué gen corresponde las secuencias utilizadas en este ejercicio? Describe brevemente ¿qué es? y ¿cuál es la función de este gen?. 
2.	A partir de alinear las secuencias, ¿podrías decir que la secuencia se encuentra conservada a través de los miembros de la familia Volvocaceae? 
3.	Dada la respuesta del inciso anterior, ¿qué tipo de secuencia (nucleótidos o aminoácidos) consideras que es más apropiada para inferir una filogenia de este grupo? 
4.	Utilizando IQ-TREE y el alineamiento siguiendo la consideración del inciso anterior, infiere el árbol filogenético de máxima verosimilitud y visualiza el resultado en iTOL o el paquete ape de R. 
5.	Según el reporte generado por IQ-TREE, ¿cuál es el modelo utilizado para inferir la filogenia? 
6.	Considerando la filogenia, ¿se apoya la hipótesis de que la multicelularidad ha emergido en una ocasión dentro de la familia Volvocaceae o de manera se podría proponer de manera alternativa que ha emergido múltiples veces? 

## Parte IV. __ / 20

5. *Hipótesis de selección con base en secuencias de nucleótidos.* 

Utilizando el alineamiento de las secuencias de nucleótidos de la `pregunta_3nt.fasta`, así como la función kaks del paquete seqinr en R. ¿Se podría decir que el gen considerado se encuentra sujeto a selección positiva, selección purificadora o evolución neutral?
