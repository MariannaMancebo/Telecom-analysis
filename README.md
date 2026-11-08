# ConnectaTel | Análisis y segmentación de clientes

Proyecto de análisis exploratorio de clientes de telecomunicaciones en Latinoamérica, desarrollado durante la formación en análisis de datos de TripleTen.

## Objetivo

Evaluar la calidad de los registros, resumir el uso de llamadas y mensajes por usuario, detectar consumos atípicos y proponer segmentos útiles para el negocio.

## Herramientas

Python · pandas · seaborn · matplotlib · Jupyter Notebook

## Metodología

1. Exploración de tres tablas de planes, usuarios y actividad.
2. Revisión de valores faltantes, sentinels y fechas fuera del periodo de análisis.
3. Agregación de llamadas, mensajes y duración por usuario.
4. Análisis de distribuciones y valores atípicos mediante IQR.
5. Segmentación exploratoria por edad y nivel de uso; recomendaciones comerciales.

## Resultados principales

- **73.58 %** de los usuarios se clasificó como uso medio; **19.45 %** como bajo uso y **6.98 %** como alto uso.
- Se identificaron **46** valores atípicos superiores en mensajes, **30** en llamadas y **109** en minutos de llamada; se conservaron para no perder posibles patrones reales.
- La población se distribuyó entre adultos (**50.45 %**), adultos mayores (**30.55 %**) y jóvenes (**19.00 %**).

Los porcentajes y conteos proceden del análisis documentado en el notebook. Los segmentos se basan en umbrales exploratorios y no constituyen un modelo predictivo.

## Archivos

- `Analysis-Project-ConnectaTel.ipynb`: notebook con el análisis, visualizaciones y conclusiones.
- `.gitignore`: exclusión de archivos de datos locales y temporales.

## Cómo ejecutarlo

Se requieren los archivos originales `plans.csv`, `users_latam.csv` y `usage.csv`, que **no están incluidos** en este repositorio. Si tienes autorización para utilizarlos, colócalos en `data/`, instala las dependencias de `requirements.txt` y ejecuta las celdas en orden.

## Limitaciones

Los datos fuente no se distribuyen aquí; las conclusiones corresponden al conjunto de datos usado en el proyecto. La segmentación es descriptiva y los resultados no deben interpretarse como relaciones causales.
