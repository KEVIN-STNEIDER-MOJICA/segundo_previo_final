SEGUNDO PREVIO DISEÑO EXPERIMENTOS
================

## Nombre: KEVIN MOJICA

## Codigo: 1950115

## Introduccion

La base de datos Theoph, tiene 132 filas y 5 columnas de datos de un
experimento sobre la farmacocinética de la teofilina. Boeckmann, Sheiner
y Beal (1994) informan datos de un estudio del Dr. Robert Upton sobre la
cinética del fármaco antiasmático teofilina. Doce sujetos recibieron
dosis orales de teofilina y luego se midieron las concentraciones
séricas en 11 puntos de tiempo durante las siguientes 25 horas. Y las
variables están representadas en la data de la siguiente manera: -
Subject: un factor ordenado con niveles 1, …, a 12 e identifica al
sujeto sobre el que se realizó la observación. El orden se da según como
va aumentando la concentración máxima de teofilina observada. - Wt: peso
del sujeto (kg). - Dose: dosis de teofilina administrada por vía oral al
sujeto (mg / kg). - Time: tiempo desde la administración del fármaco
cuando se extrajo la muestra (horas). - conc: concentración de teofilina
en la muestra (mg / L). \#\# Primer punto:

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.3     v purrr   0.3.4
    ## v tibble  3.1.0     v dplyr   1.0.6
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   1.4.0     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(dplyr)
```

## Base de datos de teofilina

Agrupada por sujetos de estudio

``` r
library(dplyr)
theoph1 <- group_by(Theoph,Subject)
Tiempo <- summarise(theoph1, tiempo_promedio=mean(Time))

Tiempo
```

    ## # A tibble: 12 x 2
    ##    Subject tiempo_promedio
    ##    <ord>             <dbl>
    ##  1 6                  5.89
    ##  2 7                  5.87
    ##  3 8                  5.89
    ##  4 11                 5.87
    ##  5 3                  5.91
    ##  6 2                  5.87
    ##  7 4                  5.94
    ##  8 9                  5.87
    ##  9 12                 5.88
    ## 10 10                 5.92
    ## 11 1                  5.95
    ## 12 5                  5.89

Podemos evidenciar en la tabla de tiempo promedio en donde el mayor
promedio de tiempo es el sujeto 1 con un promedio de 5,95 y tambien
evidenciamos el menor promedio de tiempo en el sujeto 7 con 5.865455.

## Tiempo de Toma de muestra vs Concentracion (Teofilina)

``` r
library(tidyverse)
DF1 <- mutate(Theoph, Razon_Time_conc=Time/conc)
Conglomerado_tiempo <- DF1 %>%dplyr::filter(Time>=0.25 & Time<=1)
library(dplyr)
DF2 <- DF1 %>% select(Time, Dose) %>% summarize_all(sd)
```

Podemos observar la desviacion estandar entre los sujetos durante ese
periodo de tiempo, con un tiempo de: 6.925 y una dosis de: 0.718.

## 
