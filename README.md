# U5--SIMULACION-DE-UN-SISTEMA-A-LA-REALIDAD
# 🚀 Simulador de Gravedad - Proyecto de Modelado Matemático

Este proyecto es un videojuego interactivo desarrollado en **Python** (utilizando la librería **Pygame**) que simula el fenómeno físico del **salto vertical y la caída libre** bajo diferentes gravedades planetarias, aplicando el modelo matemático del **Movimiento Rectilíneo Uniformemente Acelerado (MRUA)**.

---

## 📌 1. Definición y recolección de datos

### 1.1. Descripción del fenómeno real
El fenómeno físico representado es la **caída libre y el salto vertical**. En la realidad, cuando un objeto es lanzado hacia arriba con una velocidad inicial, la gravedad del planeta actúa como una fuerza de atracción que lo frena hasta detenerlo en su punto más alto (altura máxima) y luego lo hace descender hasta volver al suelo.

En el juego, este fenómeno se simula mediante un astronauta que salta al presionar una tecla. El jugador puede modificar la gravedad del entorno (Tierra, Marte, Luna) en tiempo real, permitiendo observar cómo un mismo impulso de salto (misma velocidad inicial) produce alturas drásticamente diferentes dependiendo de la fuerza gravitatoria del planeta seleccionado.

### 1.2. Identificación de las variables del sistema
Para construir el modelo matemático que gobierna el juego, se han identificado las siguientes variables:

**Variables Independientes (Controladas por el jugador o el entorno):**
*   **`g` (Gravedad):** La aceleración ejercida por el planeta. En el juego se puede alternar entre:
    *   Tierra: `9.8 m/s²`
    *   Marte: `3.7 m/s²`
    *   Luna: `1.6 m/s²`
*   **`v0` (Velocidad inicial):** El impulso vertical que se le da al personaje al saltar (ajustable entre 1.0 y 10.0 m/s).
*   **`t` (Tiempo):** El tiempo transcurrido durante el salto (se actualiza frame por frame en el juego).

**Variables Dependientes (Calculadas por el modelo matemático):**
*   **`y` (Posición vertical / Altura):** La altura del personaje en un instante `t`. Se calcula respecto a la posición inicial.
*   **`vy` (Velocidad vertical):** La velocidad del personaje en un instante `t`. Disminuye mientras sube y aumenta (en dirección negativa) mientras cae.
*   **`h_max` (Altura máxima):** El punto más alto que alcanza el personaje.

### 1.3. Recolección de datos y comportamiento esperado
Para validar que el juego funciona correctamente, necesitamos datos de referencia. El comportamiento esperado está dictado por las leyes de la cinemática (ecuaciones del MRUA).

Para un tiro vertical, la fórmula que predice la **altura máxima** es:

$$h_{max} = \frac{v_0^2}{2g}$$

Si establecemos una velocidad inicial constante de **`v0 = 6.0 m/s`** (el salto base del astronauta), podemos calcular la altura máxima esperada en cada planeta para nuestra tabla de validación:

| Planeta | Gravedad (`g`) | Altura Teórica (`h_max`) | Tiempo de vuelo (`t = 2v0/g`) |
| :--- | :--- | :--- | :--- |
| **Tierra** | 9.8 m/s² | **1.84 metros** | ~ 1.22 segundos |
| **Marte** | 3.7 m/s² | **4.86 metros** | ~ 3.24 segundos |
| **Luna** | 1.6 m/s² | **11.25 metros**| 7.50 segundos |

> *Nota de desarrollo: En la interfaz del juego se dibuja una **línea roja horizontal** que representa exactamente esta altura teórica calculada. El jugador puede comprobar visualmente cómo el personaje alcanza dicha línea al saltar.*

### 1.4. Supuestos del modelo
Para que el modelo matemático sea funcional en el código y fácil de programar, se asumen las siguientes condiciones ideales:
1.  **No hay resistencia del aire (fricción):** El personaje no se frena por el viento, solo por la gravedad.
2.  **Gravedad constante:** Se asume que la altura del salto es tan pequeña que la gravedad no varía durante el vuelo.
3.  **Movimiento unidimensional:** Para la mecánica de salto evaluada, solo nos importa el eje Y (vertical).

---

## ⚙️ 2. Construcción y programación del modelo

Para llevar el modelo físico a la pantalla, no podemos usar el cálculo continuo perfecto, sino que debemos simularlo mediante **métodos numéricos** (integración paso a paso) dentro del bucle del juego (Game Loop).

### 2.1. Ecuaciones del modelo matemático
El movimiento del astronauta se rige por las ecuaciones del Movimiento Rectilíneo Uniformemente Acelerado (MRUA). Para el eje vertical (Y), donde actúa la gravedad, tenemos:

1. **Velocidad en función del tiempo:**

$$v_y(t) = v_{y0} - g \cdot t$$

2. **Posición (altura) en función del tiempo:**

$$y(t) = y_0 + v_{y0} \cdot t - \frac{1}{2} g \cdot t^2$$

### 2.2. Integración numérica (El corazón del código)
En lugar de calcular la posición exacta usando la fórmula cuadrática en cada frame, el juego utiliza un método de integración llamado **Método de Euler**. En cada iteración del bucle (que corre a 60 FPS), actualizamos la velocidad y la posición basándonos en el tiempo transcurrido entre frames (`dt` o *delta time*).

El código implementa el modelo así:

```python
# dt = tiempo entre frames (aprox 0.016 segundos a 60 FPS)
dt = clock.tick(60) / 1000.0

# Integración de Euler
vy += g * dt          # Actualiza la velocidad: v = v0 + g*t
y  += vy * dt         # Actualiza la posición: y = y0 + v*t
