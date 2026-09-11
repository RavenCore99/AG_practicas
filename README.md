# Actividad de Aplicacion de Algoritmos Geneticos

**Aplicacion practica del problema del viajero con Algoritmos Geneticos usando PyGAD**

## Descripcion

Este proyecto desarrolla una solucion aproximada al **Problema del Viajante** (TSP - Traveling Salesman Problem) mediante un Algoritmo Genetico (AG) implementado en Python con la libreria **PyGAD**.

El objetivo es minimizar la distancia total recorrida para visitar un conjunto de ciudades, partiendo de una solucion aleatoria y evolucionandola porseleccion, cruce y mutacion hasta encontrar una ruta optimizada.

## Autor

- **Jorge Nicolas Casstro Ballesteros**
- Correo: jncastro@ucundinamarca.edu.co

## Tecnologias

![Python](assets/badges/python.svg)
![Jupyter Notebook](assets/badges/jupyter.svg)
![PyGAD](assets/badges/pygad.svg)
![NumPy](assets/badges/numpy.svg)
![Pandas](assets/badges/pandas.svg)
![Matplotlib](assets/badges/matplotlib.svg)
![License](assets/badges/license.svg)

## Requisitos del problema

El **Problema del Viajante** (TSP) es un problema clasico de optimizacion combinatoria:

- **Entrada**: Conjunto de `n` ciudades con coordenadas `(x, y)` y matriz de distancias euclidianas entre cada par
- **Salida**: Una ruta que visite todas las ciudades exactamente una vez y regrese al origen, minimizando la distancia total
- **Complejidad**: NP-duro, por lo que los AG ofrecen soluciones aproximadas de alta calidad en tiempo razonable

Para este ejercicio se usa `n=5` ciudades con coordenadas:

| Ciuda | x | y |
|-------|---|---|
| 1     | 0 | 0 |
| 2     | 2 | 3 |
| 3     | 5 | 4 |
| 4     | 7 | 1 |
| 5     | 8 | 5 |

## Diseño de la solucion

### Representacion de individuos

- Cada individuo es una **permutacion** de los indices `{0, 1, ..., n-1}` que representa el orden de visita de las ciudades
- Se usa `gene_type=int` y `allow_duplicate_genes=False` para mantener rutas validas

### Funcion de aptitud

- Calcula la distancia total de la ruta (incluyendo el regreso al punto inicial)
- Se devuelve `1 / distancia_total` para que sea maximizable (PyGAD maximiza por defecto)

### Operadores geneticos

- **Seleccion**: Torneo (`parent_selection_type="tournament"`)
- **Cruce**: Se comparan 4 metodos:
  - `single_point` (cruce de un punto)
  - `two_points` (cruce de dos puntos)
  - `uniform` (cruce uniforme)
  - `scattered` (cruce disperso)
- **Mutacion**: Aleatoria con `mutation_percent_genes=10`

### Parametros del AG

| Parametro | Valor |
|-----------|-------|
| Generaciones | 500 |
| Padres por cruce | 5 |
| Soluciones por poblacion | 10 |
| Numero de genes | 5 (cantidad de ciudades) |
| Semilla aleatoria | 42 (para reproducibilidad) |

## Archivos del proyecto

| Archivo | Descripcion |
|---------|-------------|
| `actividad_AG.ipynb` | Notebook principal con la implementacion completa |
| `S6_Libreria_PyGAD.md` | Documentacion de PyGAD (semana 6) |
| `S7_Ejercicio_TSP.md` | Enunciado del ejercicio del TSP (semana 7) |
| `README.md` | Este archivo: documentacion del proyecto |

## Ejecucion

### Instalacion de dependencias

```bash
pip install pygad numpy pandas matplotlib
```

### Ejecutar el notebook

Abrir `actividad_AG.ipynb` en Jupyter Notebook o JupyterLab e ir ejecutando celda por celda, o bien ejecutarlo completo con:

```bash
jupyter nbconvert --to notebook --execute actividad_AG.ipynb
```

### Resultados del caso base

Con semilla `42` y cruce `single_point`:

- **Mejor ruta encontrada**: `[4, 3, 0, 1, 2]`
- **Distancia total**: 21.12
- **Tiempo de ejecucion**: 0.35 s (aprox)

### Comparacion de metodos de cruce

Se ejecuta cada metodo de cruce 5 veces (con diferentes semillas) para promediar el efecto aleatorio del algoritmo.

Resultado promedio (menor distancia primero):

| Metodo de cruce | Distancia media | Desviacion estandar |
|-----------------|-----------------|---------------------|
| single_point    | ~21.51          | ~0.94               |
| two_points      | ~22.32          | ~1.47               |
| uniform         | ~25.22          | ~1.84               |
| scattered       | ~24.43          | ~1.32               |

El metodo `single_point` muestra mejor rendimiento en este conjunto pequeno de ciudades. Las diferencias se deben a la naturaleza estocastica del AG y al tamano de la poblacion.

## Estructura del notebook

El notebook `actividad_AG.ipynb` esta organizado en celdas de tipo Markdown y Codigo:

1. **Introduccion** y librerias necesarias
2. **Definicion de las ciudades** y generacion de la matriz de distancias
3. **Visualizacion de las ciudades** en un grafico de dispersion
4. **Funcion de aptitud**: calculo de la longitud total de la ruta
5. **Configuracion y ejecucion** del Algoritmo Genetico con PyGAD
6. **Visualizacion de la mejor ruta** encontrada y evolucion del fitness
7. **Comparacion de metodos de cruce** con medicion de tiempo y distancia

## Licencia

Proyecto de entrega academica - uso exclusivo para fines educativos.

---

**Generado para la materia: Algoritmos Geneticos y machine Learning en Practica**
