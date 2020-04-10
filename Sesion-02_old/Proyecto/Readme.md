[`Estadística con R`](../Readme.md) > `Sesión 02: Análisis Exploratorio de Datos - Análisis Multivariado`
	
## Proyecto de la sesión

### OBJETIVO 

- Aplicar los conceptos adquiridos durante la sesión.

#### REQUISITOS 

1. Completar el work de la Sesión 01
2. R versión 3.6.2 o mayor
3. R Studio versión 1.2.5033 o mayor 

#### CONTEXTO

A finales del 2019 se desató una pandemia, el COVID-19. Queremos analizar la situaciones de los distintos paises en algunos días de interés. En el repositorio https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data/csse_covid_19_daily_reports, podemos encontrar información que nos ayudará a realizar nuestros datos.

#### DESARROLLO

**En este pequeño proyecto aplicarás los conceptos adquiridos durante la sesión:**

- Matriz de correlación
- Crear visualizaciones con `ggplot2`

Para continuar con el análisis, deberás abrir el archivo que trabajaste la sesión pasada en la parte de **Proyecto**.
1. Abre tu archivo `Proyecto.R`.
2. Ejecuta todo lo que ya tenías en este archivo.
3. Crea una columna que se llame `DeathRate` donde veas la tasa de mortalidad (Num Muertes entre Num Casos).
4. Crea una columna que se llame `RecoveryRate` donde veas la tasa de recuperación (Num Recuperados entre Num Casos).
5. Crea una matriz de correlación con las variables numéricas de tu dataframe y responde: ¿cuáles son las variables con mayor correlación?
6. Para la tabla de frecuencia que realizaste la sesión pasada, crea una gráfica de barras para visualizar esta información.
7. Para las columnas numéricas que creaste `DeathRate` y `RecoveryRate`, ordena de mayor a menor y quedate con el top 20.  
8. Crea histogramas para visualizar estas dos columnas filtradas.
9. Guarda tu trabajo en el mismo script `Proyecto.R`.
