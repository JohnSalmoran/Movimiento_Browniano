# Simulación de Movimiento Browniano y Proceso Geométrico

Proyecto de simulación estocástica para aproximar trayectorias de Movimiento Browniano mediante caminatas aleatorias reescaladas y su aplicación en modelos financieros.

## Descripción

Este proyecto implementa simulaciones de:

- **Caminatas aleatorias** discretas con reescalamiento
- **Movimiento Browniano** estándar $W_t$ en el intervalo $[0, 1]$
- **Proceso Geométrico Browniano** para modelar precios de activos
- **Valoración de opciones europeas** mediante Monte Carlo y Black-Scholes

## Contenido

### 1. Simulación de Caminatas Aleatorias

Se generan trayectorias discretas $S_k$ y su versión centrada $Z_k$ para diferentes valores de pasos $N$ (100, 500, 1000, 5000), demostrando:

- La convergencia al Movimiento Browniano (Teorema de Donsker)
- Propiedades de martingala en el proceso centrado
- Efecto del número de pasos en la suavidad de las trayectorias

### 2. Proceso Geométrico Browniano

Modelo de evolución de precios de activos:

$$S_t = S_0 \cdot e^{-\alpha t + W_t}$$

donde:
- $S_0 = 110$ (precio inicial)
- $\alpha = 0.042$ (tasa libre de riesgo)
- $W_t$ es un Movimiento Browniano estándar

### 3. Valoración de Opciones Call Europeas

Comparación de dos métodos para valorar una opción call:

- **Simulación Monte Carlo** (100,000 iteraciones)
- **Fórmula de Black-Scholes** (solución analítica)

#### Parámetros de la opción:
- Precio inicial: $S_0 = 110$
- Strike: $K = 113$
- Tasa libre de riesgo: $r = 0.04$
- Tiempo a vencimiento: $T = 1$ año
- Volatilidad: $\sigma = \sqrt{2 \times 0.04}$

## Requisitos

### Librerías de R

```r
library(ggplot2)
library(dplyr)
library(tidyr)
library(knitr)
```

### Instalación

```r
install.packages(c("ggplot2", "dplyr", "tidyr", "knitr"))
```

## Uso

1. Abrir el archivo `Proyecto Movimiento Browniano.Rmd` en RStudio
2. Ejecutar todos los chunks o renderizar el documento completo:

```r
rmarkdown::render("Proyecto Movimiento Browniano.Rmd")
```

3. El output HTML mostrará:
   - Gráficos de las trayectorias simuladas
   - Tablas resumen de resultados
   - Análisis estadístico de convergencia
   - Comparación de métodos de valoración

## Resultados Esperados

### Convergencia del Browniano

A medida que $N$ y $r$ aumentan, las trayectorias discretas convergen a procesos continuos suaves, validando el Teorema de Donsker.

### Valoración de Opciones

La simulación Monte Carlo proporciona resultados con error relativo típicamente < 1% respecto a la fórmula de Black-Scholes, con intervalos de confianza del 95% bien definidos.

## Estructura del Código

```
├── Parámetros iniciales (semilla, tasas, valores de N y r)
├── Cálculo de probabilidad p* para la caminata aleatoria
├── Simulaciones principales:
│   ├── Generación de trayectorias S_k y Z_k
│   ├── Movimientos Brownianos con diferentes resoluciones
│   └── Proceso Geométrico para modelar precios
├── Monte Carlo para opciones:
│   ├── Simulación de payoffs
│   ├── Estimación del valor esperado
│   └── Cálculo de intervalos de confianza
└── Black-Scholes:
    ├── Cálculo de d1 y d2
    └── Fórmula cerrada para call europeo
```

## Fundamentos Teóricos

### Teorema de Donsker

Las caminatas aleatorias reescaladas convergen en distribución al Movimiento Browniano cuando el número de pasos tiende a infinito.

### Modelo de Black-Scholes

Asume que los precios de los activos siguen un proceso geométrico browniano con drift y volatilidad constantes, permitiendo valoración analítica de opciones europeas.

### Método de Monte Carlo

Estima el valor esperado del payoff descontado mediante simulación:

$$C_0 = e^{-rT} \mathbb{E}[\max(S_T - K, 0)]$$

## Autor

Jonathan Ivan Salmoran Acuña

## Notas

- La semilla `set.seed(42)` garantiza reproducibilidad de resultados
- Los gráficos utilizan principalmente funciones de base R para eficiencia
- El error relativo típico entre Monte Carlo y Black-Scholes es < 1% con N=100,000

## Referencias

- Teorema de Donsker (Principio de Invarianza de Donsker)
- Black, F. & Scholes, M. (1973). "The Pricing of Options and Corporate Liabilities"
- Modelo de Black-Scholes-Merton para derivados financieros
