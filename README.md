# Entregable y Avance de Proyecto

Integrantes: María José Barrios, Julian Marciales, Juan David Cordobá

## Índice de Contenidos
1. [Objetivo](#objetivo)
2. [Presentación del Problema](#presentación-del-problema)
3. [¿Cómo se abordó el problema?](#cómo-se-abordó-el-problema)
4. [Anexos](#anexos)

## Objetivo

El objetivo principal es crear un juego de sopa de letras (en python) que permita a los usuarios interactuar con una matriz de letras generada aleatoriamente. en esta entrega de avance se busca definir el diseño inicial del juego y poder mostrar el progreso en la implementación de las funciones que hemos creado hasta ahora

Importante:

1. Definir el diseño inicial del juego de sopa de letras, explicando cómo se generará la sopa, cómo se verificaran las palabras y cómo se presentará la interfaz al usuario.
2. Mostrar el progreso en la implementación de las funciones principales del juego como por ejemplo: la creación de la matriz, la inserción de letras y el formato de la sopa de letras.

## Presentación del Problema

El reto consiste en la creación de un programa que genere una sopa de letras con la que el usuario pueda interactuar desde la consola. El juego debe cumplir con los siguientes requisitos:

### Requerimientos:
1. **Generación Aleatoria:** Las palabras deben insertarse de forma aleatoria en la matriz, evitando superposiciones.
2. **Personalización:** El usuario podrá definir el tamaño de la matriz, la dificultad (basada en la densidad de palabras y la longitud de las mismas) y la lista de palabras a incluir (opcional).
3. **Verificación:** El sistema permitirá al usuario ingresar las coordenadas de las palabras que encuentre y verificar si son correctas.
4. **Interfaz:** Se requerirá una interfaz de usuario (al menos en modo consola) que permita al usuario interactuar con la sopa de letras.

### Restricciones:
1. **Sin uso de librerías externas.**
2. **Límites de tamaño:** La matriz tendrá un tamaño mínimo de 10x10 y un máximo de 30x30.
3. **Orientaciones:** Las palabras pueden ser insertadas en sentido horizontal, vertical o diagonal.

## ¿Cómo se abordó el problema?

La solución al problema se abordó de manera estructurada, comenzando por organizar la lógica del código a través de diagramas de flujo o pseudocódigo (en los anexos) luego se implementaron las funciones básicas que permiten generar y rellenar la sopa de letras, utilizando las herramientas que se dieron en clase, como matrices, arreglos, ciclos y listas.

### Creación de la matriz
El primer paso fue crear la función `crear_matriz`, que recibe como parámetro el tamaño deseado para la sopa de letras. Este tamaño se encuentra dentro de un rango permitido de 10 a 30, lo que garantiza que la matriz sea adecuada para cualquier nivel de dificultad. La matriz se construye como una lista de listas, en la que cada sublista representa una fila y se inicializa con espacios en blanco. Esta estructura vacía sirve como base para la colocación de las palabras más adelante.

```python
def crear_matriz(tamanio):   
    if not (10 <= tamanio <= 30):   
        print("Error: El tamaño debe estar entre 10 y 30")
        return None
    matriz = []  # Inicializamos la matriz vacía
    
    # Primer bucle para crear filas
    for i in range(tamanio):
        fila = []  # Creamos una fila vacía
        # Segundo bucle para crear columnas en cada fila
        for j in range(tamanio):
            fila.append(' ')  # Añadimos un espacio en blanco
        matriz.append(fila)  # Añadimos la fila a la matriz
    
    return matriz  # Retornamos la matriz completa

# Solicitamos el tamaño de la sopa de letras
tamanio = int(input("Ingresa tamaño deseado de la sopa (entre 10 y 30): "))
matriz = crear_matriz(tamanio)  
#esto se va a modificar para que el tamaño corresponda a la dificultad elegida
```

### Relleno de la matriz
Una vez que la matriz está creada, se utiliza la función `rellenar_matriz` para completar los espacios vacíos con letras aleatorias. Este proceso se realiza mediante un bucle doble: el primer bucle recorre las filas y el segundo recorre las columnas. En cada posición de la matriz, se asigna una letra aleatoria utilizando la función `random.choice` del módulo `string`, asegurando que la sopa de letras tenga una distribución aleatoria de letras.

```python
def rellenar_matriz(matriz):    # Función para rellenar la matriz con letras
    if matriz is None:    # Verificamos que la matriz exista
        return None
    
    tamanio = len(matriz)    
# Utilizamos len para obtener eltamaño de la matriz la cual vamos a rellenar 
    for i in range(tamanio):    # i recorre las filas
        for j in range(tamanio):    # j recorre las columnas
            matriz[i][j] = random.choice(string.ascii_uppercase)
    
    return matriz    # Retornamos la matriz rellenada
```

### Función de instrucciones
Para mejorar la experiencia del usuario se incluyó una función de instrucciones que proporciona una introducción clara sobre cómo jugar a la sopa de letras. Se explicaran las dinámicas de las tres dificultades disponibles: baja, media y alta y se describira brevemente las reglas del juego. Aunque el código aún está en desarrollo y no tiene la funcionalidad completa para la colocación y búsqueda de palabras consideramos que la estructura está bien definida, obvio teniendo en cuenta los comentarios en el código que indican las modificaciones pendientes

```python
def instrucciones():
    print("Bienvenid@ a la sopa de letras de Darth Pyths")
    print("Instrucciones:")
    print("1. La sopa de letras tiene 3 dificultades:")
    print("   - Baja: 10x10")
    print("   - Media: 20x20")
    print("   - Alta: 30x30")
    print("2. Escoge una categoría de palabras: Categoría 1, Categoría 2, Categoría 3...")
#aqui tal vez podriamos poner una categoria con palabras definidas por nosotros y otra que se un diccionario de palabras definidas por ellos
    print("3. Las palabras pueden ser ubicadas en direcciones horizontales, verticales o diagonales.")
    print("4. El objetivo es encontrar todas las palabras en la matriz, dando su coordenada inicial y final.") 
    print("vamos a empezar...")
```

## Anexos
### Codigo Cmpleto
```python
import random    
import string    
# Estas dos primeras lineas importan dos modulos:
# el primero permite generar numeros y secciones al al azar
#  mientras que el segundo permite importar constantes de letras para la sopa 
def instrucciones():
    print("Bienvenid@ a la sopa de letras de Darth Pyths")
    print("Instrucciones:")
    print("1. La sopa de letras tiene 3 dificultades:")
    print("   - Baja: 10x10")
    print("   - Media: 20x20")
    print("   - Alta: 30x30")
    print("2. Escoge una categoría de palabras: Categoría 1, Categoría 2, Categoría 3...")
    print("3. Las palabras pueden ser ubicadas en direcciones horizontales, verticales o diagonales.")
    print("4. El objetivo es encontrar todas las palabras en la matriz, dando su coordenada inicial y final.") 
    print("\nVamos a empezar...\n")

def crear_matriz(tamanio):   
    if not (10 <= tamanio <= 30):   
        print("Error: El tamaño debe estar entre 10 y 30")
        return None
    matriz = []  # Inicializamos la matriz vacía
    
    # Primer bucle para crear filas
    for i in range(tamanio):
        fila = []  # Creamos una fila vacía
        # Segundo bucle para crear columnas en cada fila
        for j in range(tamanio):
            fila.append(' ')  # Añadimos un espacio en blanco
        matriz.append(fila)  # Añadimos la fila a la matriz
    
    return matriz  # Retornamos la matriz completa

# Solicitamos el tamaño de la sopa de letras
tamanio = int(input("Ingresa tamaño deseado de la sopa (entre 10 y 30): "))
matriz = crear_matriz(tamanio)  
#esto se va a modificar para que el tamaño corresponda a la dificultad elegida


#aqui va una funcion para ordenar aleatoriamente las palabras en la matriz antes de rellenar

def rellenar_matriz(matriz):    # Función para rellenar la matriz con letras
    if matriz is None:    # Verificamos que la matriz exista
        return None
    
    tamanio = len(matriz)    
# Utilizamos len para obtener eltamaño de la matriz la cual vamos a rellenar 
    for i in range(tamanio):    # i recorre las filas
        for j in range(tamanio):    # j recorre las columnas
            matriz[i][j] = random.choice(string.ascii_uppercase)
    
    return matriz    # Retornamos la matriz rellenada

def main():
    #aqui ya estaran las funciones ordenadas :)

 main()
```

## Diagrama de flujo
https://lucid.app/lucidchart/395987fe-f5f7-4083-933d-46fa406f7909/edit?view_items=RNJMd7JfcoLR&invitationId=inv_5560ae65-536e-43fe-87f8-2fdfd5b6e565

![Diagrama Proyecto final](https://github.com/user-attachments/assets/f1937c14-44fe-4ed8-bf6c-1255839694d4)


## Pseudocodigo
```python
inicio #la verdad no sabia si poner el main abajo o arriba
  Llamar a la función instrucciones para mostrar las instrucciones del juego
  
  Escribir "Ingresa tamaño deseado de la sopa (entre 10 y 30):"
  Leer tamanio
  
  Llamar a la función crear_matriz(tamanio) para crear la matriz con el tamaño especificado
  Si matriz es None entonces
    Escribir "Error: El tamaño debe estar entre 10 y 30"
    Terminar programa
  Fin si
  
  Llamar a la función rellenar_matriz(matriz) para llenar la matriz con letras aleatorias
  
  Llamar a la función principal para continuar con el flujo del juego
  
Fin

[función instrucciones]
inicio
  Escribir "Bienvenid@ a la sopa de letras de Darth Pyths"
  Escribir "Instrucciones:"
  Escribir "1. La sopa de letras tiene 3 dificultades:"
  Escribir "   - Baja: 10x10"
  Escribir "   - Media: 20x20"
  Escribir "   - Alta: 30x30"
  Escribir "2. Escoge una categoría de palabras: Categoría 1, Categoría 2, Categoría 3..."
  Escribir "3. Las palabras pueden ser ubicadas en direcciones horizontales, verticales o diagonales."
  Escribir "4. El objetivo es encontrar todas las palabras en la matriz, dando su coordenada inicial y final."
  Escribir "Vamos a empezar..."
Fin

[función crear_matriz]
entrada: tamanio
salida: matriz de caracteres
inicio
  Si tamanio no está entre 10 y 30 entonces
    Escribir "Error: El tamaño debe estar entre 10 y 30"
    Retornar None
  Fin si
  
  Inicializar matriz como una lista vacía
  Para i desde 0 hasta tamanio - 1 hacer
    Crear fila vacía
    Para j desde 0 hasta tamanio - 1 hacer
      Añadir un espacio vacío a la fila
    Fin para
    Añadir la fila a la matriz
  Fin para
  
  Retornar matriz
Fin

[función rellenar_matriz]
entrada: matriz
salida: matriz de caracteres
inicio
  Si matriz es None entonces
    Retornar None
  Fin si
  
  Obtener el tamaño de la matriz como tamanio
  Para i desde 0 hasta tamanio - 1 hacer
    Para j desde 0 hasta tamanio - 1 hacer
      Asignar una letra aleatoria a matriz[i][j]
    Fin para
  Fin para
  
  Retornar matriz
Fin
```






