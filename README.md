Algoritmo ArcosGar

### Problema
El entrenamiento típico de una red neuronal implica un conocimiento inicial prácticamente aleatorio. Estructura de la red, tasa de aprendizaje, pesos iniciales... Partiendo de esto, el algoritmo funciona, pero es lento y tiene muchas cositas.

### Posible solución: evolución
¿Y si dejo que la evolución haga el trabajo?
  -	 Parte de la estructura más sencilla (inputs y outputs)
  -	 PROBLEMA: ¿alguna vez se van a crear capas nuevas? ¿Cómo va a competir una red con pesos aleatorios con redes entrenadas, aunque sean más sencillas?  

  -	 SOLUCIÓN: Cuando una mutación añada una neurona, sea en la capa que sea, todas sus conexiones serán nulas. Las conexiones del resto de las capas no se verán afectadas. Es decir, que las redes creadas tendrán capas totalmente conectadas unas con otras (la primera con la segunda, pero también con la tercera, con la cuarta, ...).


### Mutación de pesos
  -	 Prueba a mutar los pesos variando en % de su valor. Que lo más probable sean cambios pequeños (1-10%) pero que también puedan ocurrir cambios grandes. Esto se puede aplicar siempre a todos los pesos.

  -	 Muta algunos pesos con valores totalmente nuevos y aleatorios. 

  -	 ¿Una pasada de backpropagation antes de la evaluación? 


### Mutación de estructura

  -	 ¿Mucho menos probable que la mutación de pesos? Experimenta!

  -	 Empieza con la estructura más sencilla (inputs vs outputs) y ve mutando. 

  -	 Añade un nodo a cualquier capa oculta con pesos nulos. 

  -	 Elimina un nodo de cualquier capa oculta.
  -	 Pon a 0 una conexión cualquiera.

### Info que debo loguear en cada generación

  -	 Info para poder reproducir al mejor individuo de la generación.
  -	 Fitness del mejor individuo.
  -	 Fitness medio de los individuos.
  -	 Número de mutaciones de cada tipo realizadas.

# Pseudo-código

### Estructura de una red

Lista con varios elementos:
  -	 Estructura: vector con la info de las capas de la red. Ej: [5, 3, 2, 4, 1, 2] significa que la red tiene 6 capas. La de entrada tiene 5 neuronas, la primera capa oculta tiene 3 neuronas,... 

  -	 Pesos: lista de listas de matrices. Ej: el primer elemento es una lista cuyos elementos son los pesos (matrices) que conectan la capa de entrada con el resto de capas. 

  -	 Buffer de entrada: lista con un elemento por cada capa. Cada elemento es un vector numérico con un número de elementos igual al número de neuronas de esa capa. El buffer de la primera capa son las entradas a la red.  

  -	 Funciones de activación: lista de funciones con una función de activación para las neuronas de cada capa.

### Creación de una red

  -	 Estructura siempre con dos capas: entrada y salida. 

  -	 Pesos. Lista con una lista con una matriz. Inicializo los pesos en función del número de neuronas de la capa de entrada. 

  -	 Buffer de entrada a 0. 

  -	 Función de activación de entrada a 1. Función de activación de salida aleatoria entre las posibles.


### Feed forward

Para cada capa i:
> Coge las entradas del buffer
> Aplica la función de activación de la capa
> Para cada capa k desde i hasta el final:
>> Multiplica entrada i por pesos ik
>> Suma el resultado en el buffer de k


### Fitness

Error entre la salida de la red y los valores deseados, calculado con el mismo método que Kaggle :)


### Mutación de pesos 1

Elige una capa al azar.
Elige una capa de destino al azar.
Elige un elemento de esa matriz.
Súmale un valor aleatorio sacado de una distribución normal de media 0 y sd 0.5

# OLD

Prueba a hacer un algoritmo que entrene una red neuronal subiendo o bajando un poquito el valor de cada peso, recorriendo los pesos una y otra vez hasta conseguir buenos resultados. 

** Problema de este enfoque: ¿cómo elijo la estructura? **


Haz que todos los pesos partan de 0. Así la parte inicial del entrenamiento es mucho más rápida.

No sumes/restes siempre la misma cantidad si todos los pesos parten de 0 (o en general). Que sea aleatoria para evitar coincidencias.

Inicializa la red varias veces y elige la mejor como punto de partida.

Para probar varias estructuras, simplemente evalúa la que mejor se comporta después de inicializar muchas veces de forma aleatoria.

Aplica luego las técnicas aprendidas: aumento artificial de la cantidad de datos (online, añadiendo ruido), etc
