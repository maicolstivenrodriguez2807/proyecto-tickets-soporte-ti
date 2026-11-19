# Proyecto Final - Análisis de tickets de soporte TI

Proyecto final del curso **DataXperience - Ciencia de Datos** (Grupo 1, Cuarto Ciclo Virtual 2026).

**Integrante:** Maicol Stiven Rodriguez Ortegon - Ingeniería en Sistemas

*Nota: hice el proyecto de forma individual porque por mi horario de trabajo no pude reunirme con un equipo.*

**Video de presentación:** [ver video](PEGA_AQUI_EL_ENLACE_DEL_VIDEO)

---

## De qué se trata

Escogí analizar los tickets de una mesa de ayuda de TI, que son las solicitudes que hacen los empleados de una empresa cuando tienen un problema con su computador, la red, el correo, los accesos, etc. Lo elegí porque está muy relacionado con mi carrera y es un área donde trabajan muchos ingenieros de sistemas.

La pregunta que quise responder fue: **¿qué hace que un ticket se demore más en resolverse?** y si se puede predecir cuánto se va a demorar un ticket nuevo.

## Datos

- `datos/tickets_soporte_ti_crudo.csv`: los datos originales, sin limpiar (1.498 tickets de 2025 y 11 columnas).
- `datos/tickets_soporte_ti_limpio.csv`: los datos después de la limpieza (1.388 tickets).

El dataset es simulado: lo armé con la misma estructura que tienen los sistemas de tickets reales (como GLPI o Jira) y con errores típicos (duplicados, fechas en dos formatos, comas decimales, valores imposibles y nulos) para practicar la limpieza.

Las columnas son: id del ticket, fecha de apertura, categoría, prioridad, canal, área que lo pidió, técnico, número de reasignaciones, tiempo de resolución en horas, si cumplió el SLA y la satisfacción del usuario (1 a 5).

## Etapas del proyecto

**1. Preparación de los datos.** Revisé los datos con `info()`, `isnull()` y `duplicated()`, y encontré varios problemas: duplicados, textos escritos de diferentes formas, fechas en dos formatos, tiempos con coma decimal, tiempos negativos o de 9999 y calificaciones fuera de la escala. Después de limpiar quedaron 1.388 tickets (el 92,7%).

**2. Estadística descriptiva.** Calculé la media (24,7 h), la mediana (22,5 h), la moda, el rango, la varianza y la desviación estándar (15,5 h). La distribución está sesgada a la derecha, entonces la mediana representa mejor el caso normal. También comparé por prioridad y por categoría, busqué outliers con el método IQR y revisé las correlaciones.

**3. Visualización, modelo y conclusiones.** Hice gráficos para mostrar los resultados y entrené un modelo de regresión lineal para predecir el tiempo de resolución. El modelo tiene un R² de 0,47 y un error promedio de unas 7 horas.

## Principales resultados

- Los tickets urgentes son los que **menos cumplen el SLA**: solo el 26% de los de prioridad Alta y el 23% de los Críticos.
- **Hardware** es la categoría más lenta y tiene más de la mitad de los casos extremos.
- Cada **reasignación** suma unas 6 horas.
- Entre más se demora un ticket, **peor es la satisfacción** del usuario (correlación de -0,61).

## Cómo lo aplicaría

En una mesa de ayuda se podría usar el modelo para estimar cuánto se va a demorar un ticket apenas se abre y avisar si probablemente no va a cumplir el SLA. También se puede hacer un dashboard en Power BI para hacer seguimiento y decidir cuántos técnicos se necesitan en cada área.

## Estructura del repositorio

```
proyecto-tickets-soporte-ti/
├── README.md
├── datos/           -> datasets (crudo y limpio)
├── notebook/        -> notebook de Google Colab
├── presentacion/    -> presentación en PDF
└── video/           -> enlace al video
```

## Cómo ejecutar el notebook

1. Abrir `notebook/analisis_tickets_soporte_ti.ipynb` en Google Colab (Archivo > Subir cuaderno).
2. Ir a Entorno de ejecución > Ejecutar todas.
3. Cuando lo pida, subir el archivo `datos/tickets_soporte_ti_crudo.csv`.

Librerías usadas: pandas, numpy, matplotlib, seaborn y scikit-learn.
