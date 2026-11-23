# U5--SIMULACION-DE-UN-SISTEMA-A-LA-REALIDAD
U5- SIMULACION DE UN SISTEMA A LA REALIDAD

1. Definición y recolección de datos
1.1. Descripción del fenómeno real
El fenómeno físico que se desea representar y simular es la caída libre y el salto vertical bajo los efectos de la gravedad. En la realidad, cuando un objeto (en este caso, un astronauta) es lanzado hacia arriba con una velocidad inicial, la gravedad del planeta actúa como una fuerza de atracción que lo frena hasta detenerlo en su punto más alto (altura máxima) y luego lo hace descender hasta volver al suelo.

En el juego, este fenómeno se representa mediante un personaje que salta al presionar una tecla. La gravedad del entorno se puede modificar (Tierra, Marte, Luna), permitiendo al jugador observar cómo un mismo impulso de salto (misma velocidad inicial) produce alturas drásticamente diferentes dependiendo de la fuerza gravitatoria del planeta seleccionado. Este fenómeno se rige por el Movimiento Rectilíneo Uniformemente Acelerado (MRUA).

1.2. Identificación de las variables del sistema
Para construir el modelo matemático que gobierna el juego, se han identificado las siguientes variables:

Variables Independientes (Las que el jugador controla o cambia):

g
g (Gravedad): La aceleración ejercida por el planeta. En el juego se puede alternar entre:

Tierra: 
9.8
 
m
/
s
2
9.8m/s 
2
 

Marte: 
3.7
 
m
/
s
2
3.7m/s 
2
 

Luna: 
1.6
 
m
/
s
2
1.6m/s 
2
 

v
0
v 
0
​
  (Velocidad inicial de salto): El impulso vertical que se le da al personaje al saltar (ajustable mediante las flechas arriba/abajo en el juego, por defecto inicia en 
6.0
 
m
/
s
6.0m/s).

t
t (Tiempo): El tiempo transcurrido durante el salto (se actualiza frame por frame en el juego).

Variables Dependientes (Las que el modelo matemático calcula):

y
y (Posición vertical / Altura): La altura del personaje en un instante 
t
t. Se calcula respecto a la posición inicial (
y
0
y 
0
​
 ).

v
y
v 
y
​
  (Velocidad vertical): La velocidad del personaje en un instante 
t
t. Disminuye mientras sube y aumenta (en dirección negativa) mientras cae.

h
m
a
x
h 
max
​
  (Altura máxima): El punto más alto que alcanza el personaje.

Variables Constantes (Para el juego):

y
0
y 
0
​
  (Posición inicial): La altura del suelo.

d
t
dt (Delta de tiempo): El tiempo que pasa entre un frame y otro (aprox. 
0.016
0.016 segundos).

1.3. Recolección de datos y comportamiento esperado
Para validar que nuestro juego funciona correctamente, necesitamos datos de referencia. El comportamiento esperado está dictado por las leyes de la cinemática (específicamente las ecuaciones del MRUA).

Para un tiro vertical, la fórmula que predice la altura máxima que alcanzará un objeto es:

h
m
a
x
=
v
0
2
2
g
h 
max
​
 = 
2g
v 
0
2
​
 
​
 
Datos de referencia (Cálculo Teórico):
Si establecemos una velocidad inicial constante de 
v
0
=
6.0
 
m
/
s
v 
0
​
 =6.0m/s (el salto del astronauta), podemos calcular la altura máxima esperada en cada planeta utilizando la fórmula:

En la Tierra (
g
=
9.8
g=9.8):
h
m
a
x
=
6.0
2
2
⋅
9.8
=
36
19.6
≈
1.84
 
m
e
t
r
o
s
h 
max
​
 = 
2⋅9.8
6.0 
2
 
​
 = 
19.6
36
​
 ≈1.84metros

En Marte (
g
=
3.7
g=3.7):
h
m
a
x
=
6.0
2
2
⋅
3.7
=
36
7.4
≈
4.86
 
m
e
t
r
o
s
h 
max
​
 = 
2⋅3.7
6.0 
2
 
​
 = 
7.4
36
​
 ≈4.86metros

En la Luna (
g
=
1.6
g=1.6):
h
m
a
x
=
6.0
2
2
⋅
1.6
=
36
3.2
=
11.25
 
m
e
t
r
o
s
h 
max
​
 = 
2⋅1.6
6.0 
2
 
​
 = 
3.2
36
​
 =11.25metros

Nota: En el juego se añadió una línea roja que muestra exactamente estos valores calculados. El objetivo del jugador es ver cómo el personaje llega (o no) a esa línea roja.

Tiempo de vuelo esperado (
t
v
u
e
l
o
t 
vuelo
​
 ):
El tiempo total que tarda en subir y bajar se puede calcular con 
t
=
2
v
0
g
t= 
g
2v 
0
​
 
​
 .

En la Tierra: 
t
=
12
9.8
≈
1.22
 
s
t= 
9.8
12
​
 ≈1.22s.

En la Luna: 
t
=
12
1.6
=
7.5
 
s
t= 
1.6
12
​
 =7.5s (el salto dura muchísimo más, lo cual es comprobable en el juego al ver que el personaje "flota").

1.4. Supuestos del modelo
Para que el modelo matemático sea funcional en el juego y sea fácil de programar, se asumen las siguientes condiciones ideales:

No hay resistencia del aire (fricción): En el juego, el personaje no se frena por el viento, solo por la gravedad.

Gravedad constante: Se asume que la altura del salto es tan pequeña en comparación con el planeta que la gravedad no cambia mientras el personaje está en el aire.

Movimiento unidimensional: Para la mecánica de salto, solo nos importa el eje Y (vertical), ignorando el desplazamiento horizontal para simplificar el modelo.
