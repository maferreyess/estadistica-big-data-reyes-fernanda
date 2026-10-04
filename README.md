# Actividad 4.1 — Modelado estadístico para Big Data

## Pregunta de análisis

¿Qué estructuras de agrupación pueden identificarse a partir de las
características cartográficas y qué tan confiables y útiles resultan
los grupos obtenidos?

## Fuente de datos

Covertype, UCI Machine Learning Repository.

https://archive.ics.uci.edu/dataset/31/covertype

## Unidad de análisis

Cada observación representa una celda territorial de 30 × 30 metros.

## Metodología

1. Separación de `Cover_Type` antes de cualquier transformación.
2. Diagnóstico de observaciones, variables, tipos de datos,
   duplicados, valores faltantes y uso de memoria.
3. Estandarización de las 10 variables cuantitativas mediante
   `StandardScaler`.
4. Conservación de las 44 variables binarias en formato 0/1.
5. Construcción de una configuración de referencia sin reducción
   de dimensionalidad.
6. Aplicación de Incremental PCA.
7. Comparación de umbrales de 90%, 95% y 99% de varianza explicada.
8. Selección de 10 componentes, que conservan
   92.24% de la varianza.
9. Aplicación de MiniBatch K-Means con valores
   k = [2, 3, 4, 5, 6] y semillas [42, 123, 2026].
10. Evaluación mediante inercia, Silhouette, Davies-Bouldin,
    Calinski-Harabasz y estabilidad entre semillas.
11. Selección final de k = 3.
12. Comparación del modelo reducido contra la referencia sin PCA.
13. Validación externa posterior utilizando `Cover_Type`.
14. Caracterización de los grupos mediante las variables originales.

## Configuración final

- PCA: 10 componentes.
- Varianza conservada:
  92.24%.
- Número de grupos: k = 3.
- Algoritmo de agrupamiento: MiniBatch K-Means.

## Resultados principales

- Silhouette:
  0.1871

- Davies-Bouldin:
  1.8281

- Calinski-Harabasz:
  894.74

- Estabilidad ARI media:
  0.4772

- ARI externo con Cover_Type:
  0.0023

- NMI externo con Cover_Type:
  0.0147

## Comparación con la referencia

La configuración sin PCA utilizó 54 variables y aproximadamente
119.68 MB de memoria.

La configuración final con PCA utilizó 10 componentes y
aproximadamente 22.16 MB.

El tiempo de ajuste de MiniBatch K-Means fue de aproximadamente:

- Sin PCA:
  0.2528 segundos.

- Con PCA:
  0.1487 segundos.

La reducción de dimensionalidad permitió disminuir el uso de memoria
y el tiempo de procesamiento, además de mejorar las métricas internas
de agrupamiento.

## Caracterización de los grupos

El modelo final identificó tres perfiles cartográficos principales:

- Cluster 0:
  orientación este y mayor iluminación matutina.

- Cluster 1:
  orientación oeste y mayor iluminación vespertina.

- Cluster 2:
  mayor elevación y mayor alejamiento de fuentes de agua.

Estas denominaciones describen los patrones observados y no implican
que los grupos correspondan a categorías naturales o tipos de
cobertura forestal.

## Evaluación crítica del modelo

La configuración final utiliza 10 componentes principales,
que conservan 92.24% de la varianza,
junto con MiniBatch K-Means con k = 3.

La reducción de dimensionalidad mejoró la eficiencia computacional y
las métricas internas de agrupamiento. Sin embargo, el coeficiente de
silueta de 0.1871 indica que la
separación entre los grupos es moderada y existe superposición entre
ellos.

La estabilidad ARI media de
0.4772 muestra que la
solución presenta estabilidad moderada frente a cambios en la semilla
de inicialización.

La concordancia con las clases conocidas de `Cover_Type` fue muy baja,
con un ARI de 0.0023 y un NMI de 0.0147.
Por lo tanto, los grupos no deben interpretarse como una reproducción
de los tipos conocidos de cobertura forestal.

El modelo puede utilizarse para describir patrones cartográficos
relacionados con orientación, iluminación, elevación e hidrología,
pero no debe utilizarse como clasificación definitiva ni como
sustituto de `Cover_Type`.

Entre las principales limitaciones se encuentran la sensibilidad de
K-Means a la inicialización, la superposición entre algunos grupos,
la pérdida parcial de interpretabilidad causada por PCA y la
preferencia del algoritmo por grupos aproximadamente compactos.

Como procedimiento adicional de validación, sería conveniente
comparar los resultados con otro algoritmo de agrupamiento o repetir
el análisis sobre diferentes submuestras.

## Reproducción

1. Abrir `notebooks/actividad_4_1_modelado.ipynb`.
2. Instalar las dependencias indicadas en `requirements.txt`.
3. Ejecutar todas las celdas en orden.
4. Las figuras se generan automáticamente en la carpeta `figures/`.

## Referencia del conjunto de datos

Blackard, J. (1998). *Covertype* [Dataset].
UCI Machine Learning Repository.
https://doi.org/10.24432/C50K5N