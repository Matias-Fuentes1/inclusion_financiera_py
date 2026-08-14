# Dataset — Global Findex Microdata (Brasil)

Este proyecto usa los **microdatos individuales** de la encuesta Global Findex del Banco Mundial, filtrados para Brasil. El archivo no está incluido en este repositorio por su tamaño — seguí estos pasos para descargarlo.

## Cómo descargarlo

1. Entrá a la **World Bank Microdata Library**: https://microdata.worldbank.org/
2. Buscá **"Global Findex"** en el buscador de datasets.
3. Seleccioná la edición correspondiente (2025) y accedé a la página del dataset.
4. Descargá el archivo de microdatos individuales en formato `.csv` (versión "labelled", con las etiquetas de las variables ya decodificadas).
5. Puede requerir registro gratuito en la plataforma del Banco Mundial para habilitar la descarga.

## Dónde ubicarlo

Una vez descargado, colocá el archivo dentro de esta carpeta (`data/`) con el siguiente nombre, que es el que espera el notebook: data/findex_microdata_2025_labelled_update112425.csv

Si tu archivo se llama distinto, renombralo o ajustá la variable `file_path` en la primera celda de carga de datos del notebook.

## Variables relevantes usadas en el análisis

| Variable | Descripción |
|---|---|
| `economy` | País de la persona encuestada (se filtra por "Brazil") |
| `age` | Edad del encuestado |
| `saved` | Si ahorró en el último año (1 = Sí, 2 = No) |
| `female` | Género (1 = Mujer, 2 = Hombre) |
| `inc_q` | Quintil de ingreso del hogar (1 = más pobre, 5 = más rico) |
| `account_mob` | Posesión de cuenta de dinero móvil / billetera digital (0 = No, 1 = Sí) |
| `wgt` | Factor de expansión poblacional (obligatorio para cualquier cálculo de tasas representativas) |

## Nota

No subas el CSV completo al repositorio. El archivo de microdatos pesa varios MB y no aporta valor versionarlo — cualquiera puede reproducir el análisis descargándolo desde la fuente oficial siguiendo los pasos de arriba.
