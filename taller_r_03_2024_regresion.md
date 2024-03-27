Taller 03 (version 2024)
================
dacarras
Wed Mar 27, 2024

------------------------------------------------------------------------

# Instrucciones

- Los siguientes ejercicios implican generar los resultados de un
  instrumento compuesto por varias preguntas, hacer un análisis de un
  modelo de regresión simple, graficar los resultados y finalmente,
  comparar los resultados con un modelo de regresión con variables
  estandarizadas.

- Al igual que en la tarea 2, vamos a una copia de los datos del estudio
  de Poli victimizacion de Jovenes, realizada en Chile en Octubre de
  2017.

- Los datos que vamos a emplear son una versión recortada de los datos y
  con nombres adaptados, que se espera sean más amigables para generar
  los resultados programando en R.

- El archivo que contiene los datos que vamos a emplear se llama:

<!-- -->


    datos_poli_2017.csv

- El libro de codigos de la base de datos que vamos a emplear, se llama:

<!-- -->


    datos_poli_2017_codebook.xlsx

- **Advertencia**: Los datos originales provienen de una muestra
  probabilística. Este tipo de datos, permite realizar inferencias a la
  población, si la información del diseño es empleada para producir
  estimaciones. En este ejercicio con fines ilustrativos, vamos a
  ignorar este aspecto, y solo vamos a producir resultados descriptivos.

# Referencias

Alvarez, E., Guajardo, H., & Messen, R. (1986). Estudio exploratorio
sobre una escala de autoevaluación para la depresión en niños y
adolescentes. Revista Chilena de Pediatria, 57(1), 21–25.
<https://doi.org/10.4067/s0370-41061986000100003>

Birleson, P., Hudson, I., Buchanan, D. G., & Wolff, S. (1987). Clinical
Evaluation of a Self‐Rating Scale for Depressive Disorder in Childhood
(Depression Self‐Rating Scale). Journal of Child Psychology and
Psychiatry, 28(1), 43–60.
<https://doi.org/10.1111/j.1469-7610.1987.tb00651.x>

Consejo Nacional de la Infancia. (2018). Análisis Multivariable de
Estudio de Polivictimización en Niños, Niñas y Adolescentes realizado
por la Pontificia Universidad Católica de Chile.
<http://biblioteca.digital.gob.cl/handle/123456789/3535>

Denda, K., Kako, Y., Kitagawa, N., & Koyama, T. (2006). Assessment of
depressive symptoms in Japanese school children and adolescents using
the birleson depression self-rating scale. International Journal of
Psychiatry in Medicine, 36(2), 231–241.
<https://doi.org/10.2190/3YCX-H0MT-49DK-C61Q>

MINSAL. (2013). Guía Clínica para el tratamiento de adolescentes de 10 a
14 años con Depresión.
<https://www.guiadisc.com/wp-content/pdfs/guia-clinica-tratamiento-depresion-adolescentes.pdf>

Subsecretaria Prevención del Delito. (2018). Primera Encuesta Nacional
de Polivictimización en Niñas, Niños y Adolescentes: Presentación de
Resultados.

------------------------------------------------------------------------

# Ejercicios

## Ejercicio 1. Abrir los datos.

- Abra los datos `datos_poli_2017.csv`, empleando la función
  `read.csv()`. Emplee un objeto llamado `data_poli_full` para alojar a
  los datos abiertos.

``` r
# Instrucciones: Pegue o escriba los códigos utilizados en las siguientes 
#                líneas [no coloque el signo gato antes de su respuesta]
#                Una vez terminado su código, borre estos comentarios.

url_file <- url('https://raw.githubusercontent.com/dacarras/psi2301_2023_taller_03/main/datos_poli_2017.csv')

data_poli_full <- read.csv(url_file)
```

## Ejercicio 2. Vista previa de a los datos.

- **¿Cuántas variables, y cuántos casos posee la base de datos
  original?**
- Indique su respuesta bajo el código.

``` r
# Instrucciones: Escriba aqui un comando para obtener la 
#                cantidad de variables, y de casos observados
#                de la base de datos empleada.


# opcion 1
dplyr::glimpse(data_poli_full)
```

    ## Rows: 19,684
    ## Columns: 46
    ## $ id_i  <int> 47601, 47602, 47603, 47604, 47605, 47606, 47607, 47608, 47609, 4…
    ## $ curso <int> 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 3, 3, 4…
    ## $ sexo  <int> 1, 1, 2, 1, 1, 2, 1, 1, 2, 1, 1, 1, 2, 2, 1, 1, 1, 1, 1, 1, 1, 2…
    ## $ edad  <int> 1, 1, 1, 2, 1, 1, 2, 2, 2, 3, 3, 2, 3, 2, 3, 3, 3, 3, 4, 3, 3, 4…
    ## $ v01   <int> 2, 2, 2, 1, 2, 2, 1, 1, 2, 1, 2, 1, 1, 2, 2, 1, 2, 2, 2, 2, 2, 1…
    ## $ v02   <int> 2, 2, 2, NA, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, NA, 2, 2, 2,…
    ## $ v03   <int> 1, 1, 1, 2, 2, 2, 1, 2, 1, 2, 2, 1, 1, 1, 1, 2, 2, 2, 2, 1, 1, 1…
    ## $ v04   <int> 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, NA, 2, 2, 2, …
    ## $ v05   <int> 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ v06   <int> 2, 2, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 2, 1, 2, 2, 2, 1, 1, 1, 1, 1…
    ## $ v07   <int> 1, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ au1   <int> 5, 5, 4, 3, 4, 4, 5, 5, 5, 5, 3, 4, 4, 4, 5, 5, 5, 5, 5, 4, 3, 5…
    ## $ au2   <int> 5, 5, 5, 2, 4, 4, 5, 5, 5, 5, 3, 4, 4, 4, 5, 4, 5, 5, 5, 4, 4, 5…
    ## $ au3   <int> 1, 1, 1, 3, 1, 2, 2, 2, 3, 2, 3, 4, 2, 2, 3, 3, 1, 3, 1, 2, 4, 1…
    ## $ au4   <int> 5, 5, 5, 2, 5, 3, 4, 5, 5, 4, 3, 3, 4, 3, 4, 4, 5, 5, 5, 5, 4, 5…
    ## $ au5   <int> 1, 2, 1, 2, 2, 4, 1, 1, 1, 1, 3, 3, 2, 1, 5, 4, 1, 1, 1, 2, 5, 1…
    ## $ au6   <int> 5, 4, 5, 2, 5, 4, 5, 5, 5, 5, 3, 3, 4, 3, 3, 3, 4, 5, 4, 4, 2, 5…
    ## $ au7   <int> 5, 4, 5, 1, 4, 3, 5, 5, 5, 5, 3, 4, 3, 5, 2, 4, 5, 5, 5, 3, 2, 5…
    ## $ au8   <int> 1, 2, 2, 5, 4, 3, 5, 2, 1, 4, 3, 5, 3, 2, 5, 4, 1, 1, 2, 3, 2, 1…
    ## $ au9   <int> 1, 2, 1, 4, 2, 2, 2, 2, 1, 4, 3, 5, 2, 4, 4, 3, 3, 3, 2, 2, 4, 1…
    ## $ au10  <int> 1, 1, 1, 4, 1, 3, 2, 3, 1, 4, 4, 2, 2, 2, 5, 4, 2, 2, 2, 1, 2, 1…
    ## $ d01   <int> 3, 2, 2, 2, 2, 3, 3, 1, 3, 2, 2, 2, 3, 2, 3, 2, 2, 3, 3, 2, 1, 2…
    ## $ d02   <int> 2, 2, 2, 2, 2, 1, 2, 2, 3, 2, 3, 3, 1, 2, 2, 1, 2, 2, 2, 3, 2, 1…
    ## $ d03   <int> 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 3, 3, 1, 1, 3, 1, 1, 1, 1, 2, 1, 1…
    ## $ d04   <int> 1, 2, 2, 1, 1, 1, 1, 1, 2, 1, 2, 2, 2, 1, 2, 2, 2, 1, 1, 2, 2, 1…
    ## $ d05   <int> 2, 2, 2, 1, 3, 2, 3, 3, 2, 1, 2, 2, 2, 1, 1, 1, 1, 2, 2, 1, 1, 2…
    ## $ d06   <int> 3, 1, 3, 2, 2, 2, 3, 3, 1, 2, 2, 1, 1, 3, 2, 2, 3, 3, 2, 2, 2, 3…
    ## $ d07   <int> 2, 2, 3, 1, 2, 2, 2, 3, 3, 3, 2, 2, 3, 2, 3, 2, 2, 3, 2, 2, 1, 3…
    ## $ d08   <int> 3, 3, 3, 3, 3, 3, 3, 3, 2, 3, 3, 2, 2, 3, 3, 3, 3, 3, 3, 3, 2, 3…
    ## $ d09   <int> 2, 3, 3, 1, 2, 3, 1, 3, 3, 2, 2, 3, 2, 3, 2, 3, 3, 2, 3, 2, 2, 3…
    ## $ d10   <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 1, 1, 1, 1, 2, 1…
    ## $ d11   <int> 3, 2, 3, 2, 2, 2, 2, 3, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 2, 3…
    ## $ d12   <int> 3, 3, 3, 2, 2, 2, 2, 3, 1, 3, 2, 2, 2, 3, 2, 3, 3, 3, 3, 2, 1, 3…
    ## $ d13   <int> 2, 3, 3, 2, 3, 2, 3, 3, 1, 3, 1, 2, 2, 3, 3, 3, 3, 3, 3, 2, 1, 3…
    ## $ d14   <int> 1, 1, 2, 1, 2, 1, 1, 1, 2, 2, 2, 3, 1, 1, 1, 2, 1, 1, 1, 1, 1, 1…
    ## $ d15   <int> 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 2, 3, 1, 1, 2, 2, 1, 2, 1, 3, NA, …
    ## $ d16   <int> 2, 3, 3, 2, 2, 3, 3, 3, 3, 3, 2, 2, 2, 2, 3, 2, 2, 3, 3, 2, 1, 3…
    ## $ d17   <int> 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 3, 1, 1, 2, 1, 1, 1, 1, 3, 2, 1…
    ## $ d18   <int> 2, 2, 2, 3, 2, 2, 1, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 1, 2, 3, 3, 1…
    ## $ self  <int> 50, 45, 48, 22, 42, 34, 42, 45, 48, 39, 29, 29, 38, 38, 27, 32, …
    ## $ dep   <int> 7, 9, 6, 18, 10, 7, 6, 4, 17, 12, 19, 22, 10, 8, 14, 11, 8, 4, 5…
    ## $ adm   <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ zona  <int> 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4…
    ## $ prio  <dbl> 0.1644, 0.1644, 0.1644, 0.1644, 0.1644, 0.1644, 0.1644, 0.1644, …
    ## $ comu  <int> 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115,…
    ## $ poli  <int> 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…

``` r
# opcion 2
dim(data_poli_full) # filas y columnas
```

    ## [1] 19684    46

- Respuesta
  - Casos: \[escribir aqui la cantidad de casos, y borrar los
    corchetes\]
  - Variables: \[escribir aqui la cantidad de variables, y borrar los
    corchetes\]

## Ejercicio 3. Generar muestra aleatoria

- Al igual que en la tarea 1, queremos que se produzcan resultados que
  sean únicos para cada uno de ustedes. De esta forma, les solicitamos
  que generen una muestra de datos que sea única a su rut. En esta
  sección solo tendra que reemplazar el valor de `set.seed()`, de modo
  que se genere una muestra de datos que fuera única. Recuerde que
  **todos los ejericicios** siguentes, **requieren** que **se emplen los
  datos generados**.

``` r
# Instrucciones: borre a "#" al lado de "set.seed()", e incluya su RUT
#                como argumento para fijar al seed.
#                Genere la muestra aleatoria solicitada.
#                Esta muestra contiene el 50% de los datos originales.

set.seed(123456789)     # solo reemplazar el set.seed, y conservar el resto del código.
library(dplyr)
data_poli <- dplyr::slice_sample(data_poli_full, prop = .5, by = comu)
```

## Ejercicio 4. Crear una variable con los puntajes de autoestima de Rosenberg

- Inserte los códigos utilizados para crear la variable “autoestima” a
  partir de los ítems au1 a au10. (Recuerde revisar si hay ítems
  inversos e invertirlos si corresponde).

**Notas**

La escala de autoestima de Rosenberg contiene 5 afirmaciones positivas,
y 5 afirmaciones en negativo.

- Para que los puntajes totales varíen de 10 a 50 puntos, pero siempre
  representen que, mayor puntaje indique mayor autoestima, se invierte
  el valor digitado de los items invertidos. Una vez realizado el paso
  anterior, se suman las respuestas originales, y las recodificadas, y
  se produce un puntaje que varía de 10 a 50 puntos.

- A continuación, se indican los items positivos y negativos (au3, au5,
  au8, au9, au10).

<!-- -->

    variable  invertido texto_item
    au1       no        Siento que soy una persona valiosa, al menos igual que los demás
    au2       no        Siento que tengo cualidades positivas
    au3       sí        En general, tiendo a sentir que soy un fracaso
    au4       no        Soy capaz de hacer las cosas tan bien como la mayoría de las otras personas
    au5       sí        Siento que no tengo mucho de lo que sentirme orgulloso
    au6       no        Tengo una actitud positiva hacia mí mismo
    au7       no        Considerando todas las cosas, estoy satisfecho conmigo mismo
    au8       sí        Me gustaría tener más respeto conmigo mismo
    au9       sí        Me siento inútil a veces
    au10      sí        Algunas veces pienso que no soy bueno en absoluto

- En este ejericicio setiene que crear el puntaje de la escala de
  autoestima de Rosenberg. Se recomienda realizar esto en pasos. Los
  pasos son:

  - Recodificar los items negativos, en variables que se llamen `au*r`.
    Por ejemplo, `au3`, se recodifica como `au3r`.
  - Luego de recodificar los items respectivos, sume las respuestas de
    los items positivos, y los valores de las recodificaciones de los
    items negativos.
  - La suma, es por fila. Para estos fines emplee la función
    `rowSums(cbind(), na.rm = TRUE)`, u otra equivalente.
  - Guarde los resultados en una variable llamada `auto`.
  - Revise los resultados generados. Genere un plot que compare los
    puntajes de `auto`, y los de `sef`. Debiera encontrar una línea
    recta. Los puntajes deben ser iguales.

``` r
# Instrucciones: los códigos utilizados en la siguiente línea [no coloque el signo gato antes de su respuesta]

# invertir items, y crear puntaje total
data_model <- data_poli %>%
              mutate(au3r = 5 + 1 - au3) %>%
              mutate(au5r = 5 + 1 - au5) %>%
              mutate(au8r = 5 + 1 - au8) %>%
              mutate(au9r = 5 + 1 - au9) %>%
              mutate(au10r = 5 + 1 - au10) %>%
              mutate(auto = rowSums(cbind(
                au1, au2,   au3r,
                au4, au5r,  au6,
                au7, au8r,  au9r, au10r
                ), na.rm = TRUE)) %>%
              dplyr::glimpse()
```

    ## Rows: 9,789
    ## Columns: 52
    ## $ id_i  <int> 57504, 64711, 57223, 47616, 48719, 48720, 57204, 47201, 47612, 4…
    ## $ curso <int> 3, 2, 3, 3, 1, 1, 5, 1, 2, 5, 2, 1, 2, 4, 3, 3, 2, 2, 2, 2, 2, 2…
    ## $ sexo  <int> 2, 1, 2, 1, 2, 1, 2, 2, 1, 2, 2, 1, 1, 1, 1, 1, 2, 2, 1, 1, 1, 2…
    ## $ edad  <int> 4, 2, 5, 3, 3, 1, 6, 3, 2, 5, 2, 2, 3, 4, 3, 4, 4, 3, 3, 3, 2, 3…
    ## $ v01   <int> 2, 1, 2, 1, 2, 2, 1, 2, 1, 2, 2, 1, 1, 1, 2, 1, 2, 1, 2, 2, NA, …
    ## $ v02   <int> 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, NA, …
    ## $ v03   <int> 1, 1, 2, 2, 2, 1, 2, 1, 1, 2, 1, 1, 2, 1, 1, 2, 2, 2, 1, 2, 1, 1…
    ## $ v04   <int> 2, 1, 1, 2, 2, 1, 2, 1, 1, 2, 1, 1, 2, 2, 2, 2, 1, 1, 2, 2, 1, 2…
    ## $ v05   <int> 2, 2, 2, 2, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 1, 2…
    ## $ v06   <int> 1, 1, 1, 2, 2, 1, 2, 1, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 1, 1, 1, 2…
    ## $ v07   <int> 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 1, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2…
    ## $ au1   <int> 5, 3, 1, 5, 4, 4, 5, 4, 4, 5, 5, 3, 5, 2, 3, 4, 4, 5, 5, 3, 5, 4…
    ## $ au2   <int> 4, 3, 4, 4, 4, 2, 5, 3, 4, 5, 5, 4, 5, 2, 4, 3, 5, 5, 4, 3, 5, 4…
    ## $ au3   <int> 2, 3, 4, 3, 3, 4, 1, 3, 4, 1, 3, 3, 2, 4, 4, 3, 2, 1, 4, 3, 3, 2…
    ## $ au4   <int> 4, 4, 4, 4, 4, 4, 5, 3, 3, 5, 5, 3, 4, 2, 4, 4, 5, 4, 4, 3, 5, 4…
    ## $ au5   <int> 2, 4, 4, 4, 3, 2, 1, 3, 3, 1, 1, 3, 1, 4, 5, 4, 3, 2, 4, 2, 1, 2…
    ## $ au6   <int> 4, 3, 4, 3, 4, 2, 5, 2, 3, 5, 5, 4, 5, 1, 2, 5, 4, 5, 3, 3, 4, 4…
    ## $ au7   <int> 4, 2, 4, 4, 4, 3, 5, 3, 4, 5, 5, 5, 5, 1, 2, 4, 4, 5, 3, 4, 4, 3…
    ## $ au8   <int> 4, 4, 4, 4, 3, 2, 2, 5, 5, 5, 1, 4, 4, 5, 2, 5, 3, 5, 4, 4, 5, 3…
    ## $ au9   <int> 3, 5, 4, 3, 4, 4, 1, 2, 5, 1, 1, 4, 4, 5, 4, 2, NA, 1, 5, 4, 2, …
    ## $ au10  <int> 2, 3, 4, 4, 3, 2, 1, 3, 2, 1, 1, 4, 4, 5, 2, 1, 3, 2, 5, 4, 1, 2…
    ## $ d01   <int> 2, 2, 3, 2, 2, 2, 3, 2, 2, 2, 3, 2, 2, 2, 1, 2, 3, 3, 1, 2, 3, 3…
    ## $ d02   <int> 1, 3, 1, 1, 2, 2, 2, 2, 3, 1, 3, 3, 2, 3, 2, 1, 1, 1, 2, 3, 2, 1…
    ## $ d03   <int> 1, 3, 1, 1, 1, 1, 1, 1, 3, 1, 2, 2, 2, 3, 1, 1, 2, 1, 2, 2, 1, 1…
    ## $ d04   <int> 2, 3, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 3, 2, 2, 2, 2, 2, 3, 2, 2…
    ## $ d05   <int> 2, 2, 2, 1, 2, 2, 2, 1, 2, 3, 2, 3, 1, 1, 1, 3, 2, 1, 1, 2, 3, 2…
    ## $ d06   <int> 3, 2, 3, 2, 2, 2, 3, 2, 1, 2, 1, 3, 2, 2, 2, 3, 3, 3, 2, 3, 3, 1…
    ## $ d07   <int> 2, 2, 3, 2, 2, 2, 3, 3, 2, 3, 3, 2, 3, 1, 1, 3, 3, 2, 2, 1, 2, 3…
    ## $ d08   <int> 3, 2, 3, 3, 2, 2, 3, 3, 2, 3, 2, 3, 3, 2, 2, 2, 3, 3, 2, 3, 3, 2…
    ## $ d09   <int> 3, 2, 3, 3, 3, 3, 2, 2, 3, 3, 3, 2, 2, 3, 2, 2, 3, 3, 3, 3, 3, 2…
    ## $ d10   <int> 1, 2, 1, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 2, 2, 1, 1, 1, 3, 2, 1, 1…
    ## $ d11   <int> 2, 2, 2, 2, 2, 2, 3, 2, 2, 3, 2, 2, 2, 1, 2, 2, 2, 3, 2, 2, 2, 2…
    ## $ d12   <int> 2, 2, 2, 3, 2, 3, 3, 2, 2, 3, 1, 2, 3, 1, 1, 3, 3, 3, 2, 3, 2, 2…
    ## $ d13   <int> 3, 3, 3, 3, 3, 3, 2, 2, 2, 3, 1, 3, 3, 1, 1, 2, 2, 3, 2, 3, 3, 2…
    ## $ d14   <int> 1, 2, 1, 2, 1, 2, 2, 1, 3, 1, 2, 2, 2, 2, 1, 1, 2, 2, 1, 3, 1, 1…
    ## $ d15   <int> 1, 2, 1, 2, 2, 2, 2, 1, 3, 1, 2, 2, 2, 3, NA, 1, 3, 1, 2, 3, 1, …
    ## $ d16   <int> 3, 1, 3, 2, 2, 2, 3, 3, 2, 3, 3, 2, 3, 1, 1, 2, 1, 3, 1, 3, 2, 2…
    ## $ d17   <int> 1, 3, 1, 1, 2, 1, 3, 1, 3, 1, 2, 3, 2, 2, 2, 1, NA, 1, 2, 2, 1, …
    ## $ d18   <int> 2, 3, 1, 2, 2, 2, 1, 1, 2, 1, 2, 2, 2, 3, 3, 2, 2, 1, 3, 2, 1, 1…
    ## $ self  <int> 38, 26, 27, 32, 34, 31, 49, 29, 29, 46, 48, 31, 39, 15, 28, 35, …
    ## $ dep   <int> 7, 23, 4, 11, 13, 12, 9, 11, 22, 2, 17, 16, 12, 28, NA, 8, NA, 5…
    ## $ adm   <int> 1, 2, 2, 1, 1, 1, 2, 2, 1, 1, 1, 2, 1, 1, 1, 1, 1, 2, 1, 2, 2, 1…
    ## $ zona  <int> 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4…
    ## $ prio  <dbl> 0.3722, 0.5130, 0.5092, 0.1644, 0.2933, 0.2933, 0.5092, 0.1128, …
    ## $ comu  <int> 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115,…
    ## $ poli  <int> 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 1, 2…
    ## $ au3r  <dbl> 4, 3, 2, 3, 3, 2, 5, 3, 2, 5, 3, 3, 4, 2, 2, 3, 4, 5, 2, 3, 3, 4…
    ## $ au5r  <dbl> 4, 2, 2, 2, 3, 4, 5, 3, 3, 5, 5, 3, 5, 2, 1, 2, 3, 4, 2, 4, 5, 4…
    ## $ au8r  <dbl> 2, 2, 2, 2, 3, 4, 4, 1, 1, 1, 5, 2, 2, 1, 4, 1, 3, 1, 2, 2, 1, 3…
    ## $ au9r  <dbl> 3, 1, 2, 3, 2, 2, 5, 4, 1, 5, 5, 2, 2, 1, 2, 4, NA, 5, 1, 2, 4, …
    ## $ au10r <dbl> 4, 3, 2, 2, 3, 4, 5, 3, 4, 5, 5, 2, 2, 1, 4, 5, 3, 4, 1, 2, 5, 4…
    ## $ auto  <dbl> 38, 26, 27, 32, 34, 31, 49, 29, 29, 46, 48, 31, 39, 15, 28, 35, …

``` r
# plot de puntajes originales y generados
plot(y = data_model$self, x = data_model$auto)
```

![](taller_r_03_2024_regresion_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

## Ejercicio 5. Diagrama de dispersión entre la variable autoestima (`auto`) y la variable depresion (`dep`).

- Inserte los códigos utilizados para generar un gráfico de dispersión
  de las dos variables indicadas. La variable autoestima debe estar en
  el eje horizontal y depresión en el eje vertical. Recuerde
  personalizar el título para ambos ejes.

- Calcule la media de la variable de respuesta y en el mismo gráfico
  incluya una línea que muestre esa media.

``` r
# Instrucciones: los códigos utilizados en la siguiente línea [no coloque el signo gato antes de su respuesta]

# Recomendaciones: para agregar una linea al gráfico puede  
#                  utilizar el comando "abline()".

# plot de puntajes originales y generados
plot(
  y = data_model$dep, 
  x = data_model$auto,
  ylab = 'Depresion (Birleson)',
  xlab = 'Autoestima (Rosenberg)'
  )
abline(h = mean(data_model$dep, na.rm = TRUE), col = "red", lty = 1)
```

![](taller_r_03_2024_regresion_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

## Ejercicio 6. Regresión lineal simple prediciendo la variable depresión (dep) en base al predictor autoestima (auto)

- Inserte los códigos utilizados para realizar una regresión lineal
  utilizando la variable depresión (dep) como variable de respuesta y la
  variable autoestima como variable predictora. Genere el resumen de
  resultados del modelo de regresión.

``` r
# Instrucciones: los códigos utilizados en la siguiente línea [no coloque el signo gato antes de su respuesta]

lm(dep ~ 1 + auto, data = data_model) %>%
summary()
```

    ## 
    ## Call:
    ## lm(formula = dep ~ 1 + auto, data = data_model)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -23.49  -2.92  -0.29   2.77  23.94 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 30.48572    0.21922   139.1   <2e-16 ***
    ## auto        -0.54271    0.00619   -87.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 4.54 on 9041 degrees of freedom
    ##   (746 observations deleted due to missingness)
    ## Multiple R-squared:  0.459,  Adjusted R-squared:  0.459 
    ## F-statistic: 7.68e+03 on 1 and 9041 DF,  p-value: <2e-16

## Ejercicio 7. Reporte los resultados de la regresión.

- Indique los valores de los siguientes resultados en el modelo de
  regresión:

- **Respuesta**

  - El coeficiente del intercepto es:
    - b0 = 30,49 (SE = 0.22, t = 139.06, p \< .001)
  - El coeficiente de la pendiente es
    - b1 = -0.54 (SE = 0.01, t = -87.63, p \< .001)
  - La desviación estándar de los residuos (i.e., **residual standard
    error**)
    - RSE = 4.54 (df = 9041)
  - El coeficiente de determinación (r cuadrado) es
    - R^2 = .46

## Ejercicio 8. Graficar la recta de regresión

- Genere un nuevo diagrama de dispersión entre la variable depresión
  (dep) y la variable autoestima.

- En el mismo gráfico use los coeficientes de intercepto y pendiente
  para mostrar la recta de regresión que estimo en el ejercicio
  anterior.

``` r
# Instrucciones: los códigos utilizados en la siguiente línea [no coloque el signo gato antes de su respuesta]


# Recomendaciones: para agregar una linea al gráfico puede  
#                  utilizar el comando "abline()".


plot(y = data_model$dep, x = data_model$auto)
abline(lm(dep ~ 1 + auto, data = data_model), col = "red", lty = 1)
```

![](taller_r_03_2024_regresion_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

## Ejercicio 9. Interprete la desviación estándar de los residuos y el coeficiente de determinación

- **Respuesta**

  - La desviación estándar de los residuos me indica qué:
    - La desviación estandar de los residuos del modelo ajustado,
      indican que la dispersion típica de los residuos es de 4.54
      puntos.
  - El coeficiente de determinación (r cuadrado) me indica qué:
    - El coeficiente de determinación indica que la inclusión del
      predictor redujo el total de los residuos del modelo base en un
      45%.

## Ejercicio 10a. Repetir la regresión usando variables estandarizadas.

- Cree un nuevo objeto llamado data_z que tenga solo las variables dep y
  autoestima de data_poli

- Mantenga solo los casos que tengan todos los datos (eliminando casos
  con algun dato perdido)

- Inserte los códigos para convertir a puntaje Z la variable autoestima
  y guárdela en la variable autoestima_z en data_z

- Convierta a puntaje Z la variable depresión (dep) y guardela en la
  variable dep_z en data_z

- Inserte los códigos utilizados para realizar una regresión lineal
  utilizando la variable autoestima_z como variable de respuesta y la
  variable dep_z como variable predictora.

- Obtenga el resumen de resultados de la nueva regresión.

> Nota: cuando se estandarizan variables, estas *centran* las variables
> a la media de la lista de valores disponibles en cada variable. Para
> asegurar que el centro entre ambas variables sea el mismo se requiere
> se comparta la misma lista de casos. Por lo anterior, en este caso
> primero creamos una base de datos que contiene solo a las variables de
> interés, y luego creamos las transformaciones de variables.

``` r
# Pegue los códigos utilizados en la siguiente línea [no coloque el signo gato antes de su respuesta]

data_z <- data_model %>%
          dplyr::select(dep, auto) %>%
          na.omit() %>%
          mutate(dep_z = as.numeric(scale(dep, scale = TRUE))) %>%
          mutate(auto_z = as.numeric(scale(auto, scale = TRUE))) %>%
          dplyr::glimpse()
```

    ## Rows: 9,043
    ## Columns: 4
    ## $ dep    <int> 7, 23, 4, 11, 13, 12, 9, 11, 22, 2, 17, 16, 12, 28, 8, 5, 21, 1…
    ## $ auto   <dbl> 38, 26, 27, 32, 34, 31, 49, 29, 29, 46, 48, 31, 39, 15, 35, 43,…
    ## $ dep_z  <dbl> -0.76656, 1.82285, -1.25207, -0.11921, 0.20447, 0.04263, -0.442…
    ## $ auto_z <dbl> 0.44744, -1.10774, -0.97814, -0.33015, -0.07095, -0.45975, 1.87…

``` r
# ajustamos como se despliegan los numeros en consola
options(scipen = 5)
options(digits = 4)

# salida tradicional de lm()
lm(dep_z ~ 1 + auto_z, data = data_z) %>%
summary()
```

    ## 
    ## Call:
    ## lm(formula = dep_z ~ 1 + auto_z, data = data_z)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -3.801 -0.472 -0.047  0.448  3.874 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  1.54e-16   7.73e-03     0.0        1    
    ## auto_z      -6.78e-01   7.73e-03   -87.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.735 on 9041 degrees of freedom
    ## Multiple R-squared:  0.459,  Adjusted R-squared:  0.459 
    ## F-statistic: 7.68e+03 on 1 and 9041 DF,  p-value: <2e-16

``` r
# salida lm, mediante broom::tidy()
lm(dep_z ~ 1 + auto_z, data = data_z) %>%
broom::tidy() %>%
knitr::kable(., digits = 2)
```

| term        | estimate | std.error | statistic | p.value |
|:------------|---------:|----------:|----------:|--------:|
| (Intercept) |     0.00 |      0.01 |      0.00 |       1 |
| auto_z      |    -0.68 |      0.01 |    -87.63 |       0 |

``` r
# correlación entre ambas variables
with(data_z, cor.test(dep_z, auto_z))
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  dep_z and auto_z
    ## t = -88, df = 9041, p-value <2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.6887 -0.6664
    ## sample estimates:
    ##     cor 
    ## -0.6777

``` r
# Nota: (actualización 2024).
#        Para garantizar que el intercepto quede en cero
#        removemos los casos perdidos de la variable de respuesta (y)
#        y de la covariable (x). De esta forma, podemos asegurar
#        que el cero de ambas variables ocupa la misma posición.
```

## Ejercicio 10b. Interprete los coeficientes de la regresión con variables estandarizadas.

- **Respuesta**

- El coeficiente del intercepto es:

  - Como esta es una regresión con puntajes estandarizados, el
    intercepto es necesariamente cero. Este representa a la media de la
    covariable del modelo.

- El coeficiente de la pendiente es:

  - La pendiente indica el aumento o disminución esperada de la variable
    de respuesta, condicional a los valores de la covariable de
    autoestima. Por cada 1 desviación estandar de auestima, esperamos
    una disminución en los puntajes de depresión de .68 desviación
    estándar de los puntajes de depresión. Este coeficiente, es
    equivalente al coeficiente de correlación entre ambas variables.
