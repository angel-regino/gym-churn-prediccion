# Predicción de cancelación de clientes en un gimnasio

**Proyecto de análisis de datos · TripleTen · 2026**

Autor: Angel Regino

---

## 1. El problema

Una cadena de gimnasios pierde clientes cada mes. El área de **retención de clientes** necesita saber:

1. **¿Qué características tienen los clientes que se van?**
2. **¿Se puede predecir quién va a cancelar?** Así el gimnasio puede actuar antes de que pase.
3. **¿Qué perfiles de clientes existen?** Así se pueden diseñar estrategias para cada grupo.

## 2. Los datos

`gym_churn_us.csv`: **4 000 clientes** sin valores nulos, con 13 características y la columna objetivo `Churn` (1 = canceló).

| Tipo | Variables |
|---|---|
| Datos del cliente | Género, edad, si vive cerca, si viene por una empresa asociada o por un amigo, si dejó teléfono |
| Contrato | Duración del contrato (1, 6 o 12 meses) y meses que le faltan |
| Comportamiento | Antigüedad (`Lifetime`), frecuencia de visitas (total y del último mes), clases grupales y gasto en servicios extra |

## 3. Lo que hice

### Análisis exploratorio (EDA)
- Comparé a los clientes que se van con los que se quedan, con gráficos de barras (variables de sí/no) e histogramas (variables numéricas).
- Hice una matriz de correlación para ver qué variables se relacionan con la cancelación y cuáles están duplicadas.

### Modelo de predicción
- Separé los datos en entrenamiento (80%) y prueba (20%) y estandaricé las variables.
- Entrené y comparé dos modelos de clasificación: **regresión logística** y **bosque aleatorio** (*random forest*).
- Los evalué con **exactitud** (*accuracy*), **precisión** y **recall**.

### Segmentación de clientes
- Usé un **dendrograma** (agrupamiento jerárquico), que sugirió entre 4 y 6 grupos.
- Agrupé a los clientes con **K-means** (5 clústeres) y comparé la tasa de cancelación de cada grupo.

**Herramientas:** Python (pandas, Matplotlib, seaborn, scikit-learn, SciPy) en Jupyter Notebook

## 4. Lo que descubrí

- **La cancelación no es aleatoria.** Se concentra en clientes nuevos, con contrato corto y poca asistencia reciente. Las variables más ligadas a quedarse son la antigüedad (-0.44), la asistencia del último mes (-0.41), la duración del contrato (-0.39) y los meses que faltan para que termine (-0.38). El género y el teléfono no influyen.
- **El modelo predice bien.** Ambos modelos aciertan con el 92% de los clientes (predecir que nadie cancela daría 73%). La **regresión logística** fue un poco mejor, con **precisión de 0.85 y recall de 0.83**: detecta a más de 8 de cada 10 clientes que se van. Además, es más simple de interpretar.
- **Hay perfiles muy distintos.** La tasa de cancelación va del **2.8%** (clúster 0, contratos largos, convenios con empresas y amigos) al **51.4%** (clúster 3, clientes nuevos con contrato de 1 mes y baja asistencia). El clúster 2, con 44% de cancelación, agrupa a quienes viven lejos del gimnasio.

### Recomendaciones para el gimnasio
1. **Fomentar la asistencia constante:** retos semanales con premios y mensajes automáticos a quien baje su frecuencia.
2. **Reforzar los primeros meses:** orientación gratuita, rutina guiada y seguimiento en el primer y segundo mes.
3. **Impulsar contratos más largos:** descuentos para pasar de 1 mes a 6 o 12 meses.
4. **Aprovechar lo social:** reforzar "trae a un amigo", los convenios con empresas y las clases grupales, sobre todo para quienes viven lejos.
5. **Usar el modelo cada mes** para identificar a los clientes en riesgo y dirigirles primero estas acciones.
