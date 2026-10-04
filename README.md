# Actividad 4.1 — Modelado estadístico para Big Data

## Pregunta de análisis
¿Qué estructuras de agrupación pueden identificarse a partir de las características cartográficas y qué tan confiables y útiles resultan los grupos obtenidos?

## Fuente de datos
Covertype, UCI Machine Learning Repository.  
https://archive.ics.uci.edu/dataset/31/covertype

## Unidad de análisis
Cada observación representa una celda territorial de 30 × 30 metros.

## Metodología
1. Separación de `Cover_Type`.
2. Diagnóstico de datos.
3. Estandarización de 10 variables cuantitativas y conservación de 44 binarias en 0/1.
4. Referencia sin reducción.
5. Incremental PCA con umbral principal de 90%.
6. Sensibilidad con 90%, 95% y 99%.
7. MiniBatch K-Means con k = [2, 3, 4, 5, 6] y semillas [42, 123, 2026].
8. Evaluación con inercia, Silhouette, Davies-Bouldin, Calinski-Harabasz y estabilidad.
9. Comparación con la referencia.
10. Validación externa posterior con `Cover_Type`.
11. Caracterización de clusters con variables originales.

## Configuración final
- PCA: 10 componentes.
- Varianza conservada: 92.24%.
- k = 3.
- Algoritmo: MiniBatch K-Means.

## Resultados principales
- Silhouette: 0.1871
- Davies-Bouldin: 1.8281
- Calinski-Harabasz: 894.74
- Estabilidad ARI media: 0.4772
- ARI externo: 0.0023
- NMI externo: 0.0147

## Comparación con referencia
- Memoria sin PCA: 119.68 MB
- Memoria con PCA: 22.16 MB
- Tiempo K-Means sin PCA: 0.3337 s
- Tiempo K-Means con PCA: 0.1375 s

## Caracterización
- Cluster 0: Orientación este y mayor iluminación matutina.
- Cluster 1: Orientación oeste y mayor iluminación vespertina.
- Cluster 2: Mayor elevación y alejamiento de hidrología.

Los nombres describen perfiles cartográficos y no representan categorías naturales ni tipos definitivos de cobertura forestal.

## Evaluación crítica
La solución presenta estructura interna, pero separación y estabilidad moderadas. La concordancia con `Cover_Type` es muy baja, por lo que no debe usarse como clasificación o sustituto de la variable conocida.

## Reproducción
1. Abrir `notebooks/actividad_4_1_modelado.ipynb`.
2. Instalar `requirements.txt`.
3. Ejecutar las celdas en orden.
4. Las figuras se generan en `figures/`.

## Referencia
Blackard, J. (1998). *Covertype* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C50K5N