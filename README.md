# Proyecto 6 — Análisis de una empresa de telecomunicaciones

## Descripción general

Este proyecto analiza el comportamiento de los clientes de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en México y Colombia.

El propósito principal es comprender cómo los usuarios utilizan los servicios móviles, especialmente llamadas y mensajes, detectar comportamientos atípicos y reconocer segmentos de clientes con necesidades diferentes.

El análisis busca generar hallazgos útiles para mejorar la oferta comercial, diseñar planes más adecuados y fortalecer la experiencia del cliente.

---

## Objetivo del proyecto

Construir un perfil estadístico del comportamiento de los clientes durante el periodo disponible hasta 2024, integrando información de usuarios, planes y uso real del servicio.

Las principales preguntas de negocio son:

- ¿Qué segmentos presentan mayor o menor uso de llamadas y mensajes?
- ¿Qué usuarios muestran valores atípicos o comportamientos inusuales?
- ¿Cómo varía el uso según la edad y el plan contratado?
- ¿Qué oportunidades existen para mejorar o crear nuevos planes?

---

## Datasets utilizados

El análisis se desarrolló con tres archivos CSV proporcionados dentro del entorno educativo de TripleTen:

### `plans.csv`

Contiene la información de los planes disponibles:

- nombre del plan;
- mensajes incluidos;
- GB incluidos al mes;
- minutos incluidos;
- pago mensual;
- costo por GB adicional;
- costo por mensaje adicional;
- costo por minuto adicional.

### `users_latam.csv`

Contiene la información de los clientes:

- identificador del usuario;
- nombre y apellido;
- edad;
- ciudad;
- fecha de registro;
- plan contratado;
- fecha de cancelación.

### `usage.csv`

Contiene el detalle del uso de los servicios:

- identificador de la actividad;
- identificador del usuario;
- tipo de actividad: llamada o mensaje;
- fecha de la actividad;
- duración de las llamadas;
- longitud de los mensajes.

> **Nota:** Los archivos CSV no se incluyen en este repositorio. El proyecto fue publicado únicamente con el notebook y este README, de acuerdo con las instrucciones de entrega. Para reproducir el análisis es necesario contar con los datasets originales proporcionados por TripleTen.

---

## Etapas del análisis

### 1. Carga y exploración inicial

- Importación de las librerías necesarias.
- Carga de los tres datasets.
- Revisión de las primeras filas.
- Inspección de dimensiones, columnas y tipos de datos con `.shape` y `.info()`.

### 2. Identificación de problemas de calidad

- Conteo y proporción de valores nulos.
- Revisión de valores inválidos y sentinels.
- Exploración estadística de columnas numéricas.
- Revisión de valores únicos en columnas categóricas.
- Detección de fechas fuera del periodo válido.

### 3. Limpieza básica

- Sustitución del sentinel `-999` en la edad por la mediana.
- Reemplazo del valor `?` en ciudad por valores nulos.
- Conversión de columnas de fecha con `pd.to_datetime()`.
- Marcado de fechas futuras como nulas.
- Conservación de nulos estructurales en `duration` y `length`, ya que dependen del tipo de actividad.

### 4. Construcción del perfil de uso por usuario

Se creó una tabla agregada por `user_id` con:

- cantidad total de mensajes;
- cantidad total de llamadas;
- minutos totales de llamada.

Esta información se combinó con el dataset de usuarios para construir el DataFrame final `user_profile`.

### 5. Análisis estadístico y visual

- Resumen estadístico de edad, mensajes, llamadas y minutos.
- Distribución porcentual de los planes.
- Histogramas separados por tipo de plan.
- Boxplots para identificar valores extremos.
- Detección de outliers mediante el método del rango intercuartílico, IQR.

### 6. Segmentación de clientes

Se crearon dos segmentaciones:

#### Segmentación por uso

- **Bajo uso:** menos de 5 llamadas y menos de 5 mensajes.
- **Uso medio:** menos de 10 llamadas y menos de 10 mensajes.
- **Alto uso:** resto de los casos.

#### Segmentación por edad

- **Joven:** menor de 30 años.
- **Adulto:** de 30 a 59 años.
- **Adulto Mayor:** 60 años o más.

### 7. Conclusiones ejecutivas

Se documentaron:

- problemas de calidad encontrados;
- distribución de los segmentos;
- comportamiento por edad y nivel de uso;
- patrones extremos;
- oportunidades comerciales;
- recomendaciones para mejorar la oferta de planes.

---

## Principales hallazgos

- El segmento de **Uso medio** representa la mayor parte de los clientes.
- Los **Adultos** constituyen el grupo de edad más numeroso.
- Los minutos de llamada presentan la mayor cantidad de valores atípicos.
- Los outliers se conservaron porque pueden representar clientes reales de alto consumo.
- Existen oportunidades para diseñar planes diferenciados para usuarios de bajo, medio y alto uso.

---

## Herramientas utilizadas

- Python
- pandas
- seaborn
- matplotlib
- Jupyter Notebook

---

## Cómo ejecutar el notebook

### En el entorno de TripleTen

El notebook fue desarrollado usando las rutas de datos disponibles dentro de la plataforma:

```python
plans = pd.read_csv('/datasets/plans.csv')
users = pd.read_csv('/datasets/users_latam.csv')
usage = pd.read_csv('/datasets/usage.csv')
```

Para ejecutarlo:

1. Abre el notebook dentro del entorno de TripleTen.
2. Verifica que los archivos estén disponibles en la carpeta `/datasets/`.
3. Ejecuta las celdas en orden.
4. Usa **Run All** para confirmar que el notebook es reproducible de principio a fin.

### En Google Colab o Jupyter Notebook

Como los datasets no están incluidos en este repositorio, primero debes obtener los tres archivos originales desde la fuente autorizada.

Después:

1. Abre el notebook en Google Colab o Jupyter Notebook.
2. Carga los archivos `plans.csv`, `users_latam.csv` y `usage.csv`.
3. Ajusta las rutas según la ubicación de los archivos.

Ejemplo para Google Colab:

```python
plans = pd.read_csv('/content/plans.csv')
users = pd.read_csv('/content/users_latam.csv')
usage = pd.read_csv('/content/usage.csv')
```

Ejemplo si los archivos están en la misma carpeta que el notebook:

```python
plans = pd.read_csv('plans.csv')
users = pd.read_csv('users_latam.csv')
usage = pd.read_csv('usage.csv')
```

4. Ejecuta las celdas desde el inicio y en el orden original.

---

## Guía breve de reproducción

1. Obtén los datasets originales desde TripleTen o desde una fuente autorizada.
2. Coloca los tres archivos en el entorno donde ejecutarás el notebook.
3. Instala las dependencias necesarias:

```bash
pip install pandas seaborn matplotlib jupyter
```

4. Abre el notebook.
5. Ajusta las rutas de carga de los CSV.
6. Ejecuta las celdas de importación, exploración, limpieza, agregación, visualización y segmentación.
7. Ejecuta **Run All** para verificar que no existan dependencias ocultas entre celdas.

---

## Contenido del repositorio

```text
proyecto-connectatel/
│
├── analisis_connectatel.ipynb
└── README.md
```

Los datasets no forman parte del repositorio.

---

## Autor

Proyecto desarrollado como parte del programa de análisis de datos de TripleTen.
