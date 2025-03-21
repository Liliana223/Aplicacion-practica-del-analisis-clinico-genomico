# Aplicacion-practica-del-analisis-clinico-genomico

1.	Inicio del estudio. Se selecciona una enfermedad y se realiza una búsqueda de documentación e información en bases de datos genómicas y fenotípicas, como ClinVar (https://www.ncbi.nlm.nih.gov/clinvar/) o OMIM (https://www.omim.org/), con el objetivo de identificar genes relacionados con el fenotipo de interés.

Para este análisis, trabajaré con el gen TP53, relacionado con el carcinoma hepatocelular (CHC). Esta patología es causada por una mutación en varios genes, estos incluyen: TP53 MET, CTNNB1, PIK3CA, AXIN1 y APC (1).

2.	Obtención de datos. Se realizó una búsqueda en el European Nucleotide Archive (ENA) (https://www.ebi.ac.uk/ena/browser/home) para obtener datos de secuenciación del gen concreto. 

Se obtiene los datos de la siguiente página: 
https://www.ebi.ac.uk/ena/browser/view/SRX7922608

3.	Realizar un control de calidad sobre los datos en Galaxy (https://usegalaxy.org/).
   
### Basic Statistics:
En esta sección se presentan las características generales de los datos analizados, incluyendo el total de secuencias, la longitud de las secuencias, el porcentaje de contenido de GC, entre otros parámetros relevantes.

### Per base sequence quality:
Se observa una cantidad significativa de secuencias fuera del rango óptimo, las cuales 
se encuentran en las áreas roja y naranja de la gráfica. Estas secuencias 
presentan un score inferior a 28, lo que podría indicar una menor calidad.

### Per sequence quality scores
La mayoría de las secuencias presentan una calidad de 33 o inferior, mientras que
solo una pequeña proporción supera este valor.

### Per base sequence content
En esta gráfica, lo esperado sería observar líneas uniformes; sin embargo, se aprecia 
una considerable variación. Este comportamiento podría deberse a la presencia de 
adaptadores.

### Per sequence GC content
Se identifica una distribución atípica de las secuencias, caracterizada por la presencia 
de múltiples picos. Esto podría estar asociado a la existencia de secuencias repetidas 
en los datos analizados.

### Per base N content
El contenido de nucleótidos desconocidos es muy bajo

### Sequence Length Distribution
La distribución del largo de las secuencias es normal

### Sequence Duplication Levels
Se detecta una alta proporción de secuencias repetidas. Por ejemplo, se observa más 
de 1,000 secuencias que equivalen a aproximadamente el 28% de secuencias.

### Overrepresented sequences
Se observa una gran cantidad de secuencias repetidas. Por ejemplo, la primera 
secuencia de la imagen, se observa 17391 veces.

### Adapter Content
Por último, se observa la presencia de algunos adaptadores que no han sido 
eliminados.

Posteriormente realizamos una limpieza de datos con Trimmomatic.

Observamos que se corrigieron los siguientes errores:
•	Obtenemos las secuencias con mejor calidad

•	Logramos solucionar la presencia de adaptadores

•	Se eliminó una cantidad significativa de secuencias duplicadas que no cumplían con los estándares de calidad. No obstante, aún persiste una cantidad considerable de secuencias duplicadas, lo cual se evidencia en las siguientes gráficas.

Las gráficas del porcentaje de bases muestran alteraciones, posiblemente debido a la alta cantidad de secuencias repetidas.

4.	Alineamiento de secuencias. Realizar un alineamiento de secuencias para alinear las secuencias con un genoma de referencia

Procedemos a utilizar la herramienta Bowtie2. 

Observamos que las secuencias no se encuentran ordenadas y no se pueden comparar correctamente.

Posteriormente ordenamos con la herramienta Samtools sort 

Realizamos el marcado de duplicados para eliminarlos

Finalmente podemos observar las secuencias organizadas y alineadas. En este momento podemos identificar las regiones conservadas.

5.	Llamado de variantes. Identificar las variantes genéticas en las secuencias alineadas obtenidas.

Utilizamos la herramienta FreeBayes

Los archivos VCF tienen varias columnas importantes, dentro de estas se encuentran:
•	CHROM: Es el cromosoma donde se encuentra ubicada la variante.
•	POS: Es la posición donde se encuentra ubicada la variante.
•	ID: Identificador de la variante.
•	REF: Nucleótido de referencia
•	ALT: Nucleótido mutado o alternativo.
•	QUAL: Puntaje numérico que describe la calidad del llamado de la variante.
•	FILTER: Filtro aplicado a la variante
•	INFO: Información adicional de la variante (2)

6.	Análisis de variantes. Finalmente, utiliza herramientas como Ensembl VEP (https://grch37.ensembl.org/info/docs/tools/vep/index.html) para determinar la patogenicidad de las variantes encontradas, su significado biológico y más información.

Cargamos el archivo VCF que obtuvimos en Galaxy

Se procesaron un total de 121 variantes, de las cuales 55 (45.5%) correspondieron a nuevas variantes y 66 (54.5%) eran variantes previamente descritas. La mayoría de las variantes (45%) son del tipo missense, las cuales implican cambios en los aminoácidos de la proteína resultante y pueden afectar tanto su estructura como su función. A continuación, se encuentran las variantes sinónimas, que representan el 32% del total. Estas variantes implican mutaciones en las que el cambio en la secuencia del ADN no altera el aminoácido producido, manteniendo la estructura y función de la proteína.

## Referencias
1.	Entry - #114550 - HEPATOCELLULAR CARCINOMA - OMIM [Internet]. Omim.org. [citado el 10 de diciembre de 2024]. Disponible en: https://www.omim.org/entry/114550?search=cancer&highlight=%28cancer%7Ccancerous%29. .
2.	Danecek P, Auton A, Abecasis G, Albers CA, Banks E, DePristo MA, et al. The variant call format and VCFtools. Bioinformatics [Internet]. 2011;27(15):2156–8. Disponible en: http://dx.doi.org/10.1093/bioinformatics/btr330. .


