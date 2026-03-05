# 📚 Notas Conceptuales - Unidad 1: Fundamentos de Python

Este documento consolida los conceptos clave de la primera unidad del curso de Python (UNEMI), complementados con el enfoque analítico del libro *Python para todos* (Charles Severance). 

---

## 1. Introducción y Arquitectura

### ¿Qué es Python?
Es un lenguaje de programación interpretado, de alto nivel y de propósito general. Destaca por su sintaxis clara y legible, actuando como un intermediario entre las instrucciones lógicas del programador y el procesamiento de la máquina.

### Arquitectura de Hardware (El enfoque del Ingeniero)
Para escribir código eficiente, es vital entender dónde se ejecuta:
* **Unidad Central de Procesamiento (CPU):** Ejecuta las instrucciones (el código). Es extremadamente rápida pero necesita que le digamos exactamente qué hacer a continuación.
* **Memoria Principal (RAM):** Almacena los programas y datos en uso de forma temporal (variables, listas). Se borra al apagar el equipo.
* **Memoria Secundaria:** Almacenamiento persistente (discos duros, SSD). Aquí es donde viven los scripts `.py` y las bases de datos.

### Entorno de Desarrollo
* **Intérprete vs. Compilador:** Python es un intérprete. Lee y ejecuta el código línea por línea, lo que facilita la depuración interactiva.
* **Editor:** Se recomienda **Visual Studio Code (VS Code)** con la extensión de Python para mantener el código estructurado y aprovechar herramientas de autocompletado y validación (linting).

---

## 2. Variables, Tipos de Datos y Operadores

### Variables y Memoria
Una variable es un espacio en la Memoria Principal con un nombre asignado que hace referencia a un valor. 

```python
# Declaración de variables
nombre = "Ana"           # str en RAM
edad = 25                # int en RAM
altura = 1.65            # float en RAM
es_estudiante = True     # bool en RAM

# Python infiere el tipo automáticamente (tipado dinámico)
print(type(nombre))      # <class 'str'>
print(type(edad))        # <class 'int'>
```

* **Nombres Mnemónicos:** Es una buena práctica usar nombres que describan el propósito del dato (ej. `velocidad_sensor` en lugar de `v`), evitando siempre las palabras reservadas de Python (como `class`, `yield`, `def`).

```python
# ✅ Buenos nombres (mnemónicos)
temperatura_sensor = 36.5
total_estudiantes = 120
nombre_completo = "Juan Pérez"

# ❌ Malos nombres (poco descriptivos)
t = 36.5
n = 120
x = "Juan Pérez"
```

### Tipos de Datos Principales
Python infiere el tipo de dato automáticamente (tipado dinámico):
1.  **Numéricos:** Enteros (`int`), decimales (`float`), complejos (`complex`).
2.  **Cadenas de texto (`str`):** Secuencias de caracteres. Son inmutables.
3.  **Booleanos (`bool`):** Valores lógicos `True` o `False`.
4.  **Estructuras de Datos:**
    * `list` (Listas): Colecciones ordenadas y mutables.
    * `tuple` (Tuplas): Colecciones ordenadas e inmutables (más eficientes en memoria).
    * `dict` (Diccionarios): Colecciones de pares clave-valor (tablas hash).

### Operadores

* **Aritméticos:** `+`, `-`, `*`, `/` (división flotante), `//` (división entera), `%` (módulo o resto), `**` (exponenciación).

```python
# Operadores aritméticos
print(10 + 3)   # 13
print(10 - 3)   # 7
print(10 * 3)   # 30
print(10 / 3)   # 3.3333... (división flotante)
print(10 // 3)  # 3 (división entera)
print(10 % 3)   # 1 (módulo/resto)
print(10 ** 3)  # 1000 (exponenciación)
```

* **De Comparación:** `==`, `!=`, `>`, `<`, `>=`, `<=`. Evalúan condiciones y devuelven un booleano.

```python
# Operadores de comparación
edad = 18
print(edad >= 18)  # True
print(edad == 21)  # False
print(edad != 18)  # False
```

* **Lógicos:** `and`, `or`, `not`. Permiten agrupar y evaluar múltiples expresiones booleanas (Python utiliza la "evaluación en cortocircuito" para optimizar estas operaciones lógicas).

```python
# Operadores lógicos
edad = 20
tiene_licencia = True

# and: ambas condiciones deben ser True
print(edad >= 18 and tiene_licencia)  # True

# or: al menos una condición debe ser True
print(edad < 18 or tiene_licencia)    # True

# not: invierte el valor booleano
print(not tiene_licencia)              # False

# Evaluación en cortocircuito
# En 'and', si el primero es False, no evalúa el segundo
resultado = False and funcion_costosa()  # No ejecuta funcion_costosa()

# En 'or', si el primero es True, no evalúa el segundo
resultado = True or funcion_costosa()    # No ejecuta funcion_costosa()
```

---

## 3. Control de Flujo: Condicionales y Bucles

El flujo de ejecución normal es secuencial (de arriba hacia abajo), pero podemos alterarlo mediante la lógica condicional y la iteración.

### Ejecución Condicional (`if`, `elif`, `else`)
Permite ramificar la ejecución del programa basándose en expresiones booleanas.

```python
# Condicional simple
edad = 18
if edad >= 18:
    print("Eres mayor de edad")

# if-else
if edad >= 18:
    print("Eres mayor de edad")
else:
    print("Eres menor de edad")

# if-elif-else (múltiples condiciones)
nota = 85
if nota >= 90:
    print("Excelente")
elif nota >= 80:
    print("Muy bien")
elif nota >= 70:
    print("Bien")
else:
    print("Necesitas mejorar")
```

* Se pueden usar condicionales anidados, aunque por legibilidad de código se prefieren los condicionales encadenados (`elif`).

```python
# ❌ Anidado (menos legible)
if nota >= 60:
    if nota >= 80:
        print("Aprobado con honores")
    else:
        print("Aprobado")

# ✅ Encadenado (más legible)
if nota >= 80:
    print("Aprobado con honores")
elif nota >= 60:
    print("Aprobado")
else:
    print("Reprobado")
```

* **Manejo de Excepciones (`try` / `except`):** Una práctica de programación avanzada desde el día 1. En lugar de dejar que un error (como un `ValueError` al esperar un número y recibir un texto) detenga o "rompa" el programa, se "captura" el error de forma controlada.

```python
# Sin manejo de excepciones (programa se rompe)
numero = int(input("Ingresa un número: "))  # Error si usuario ingresa "abc"

# Con manejo de excepciones (programa continúa)
try:
    numero = int(input("Ingresa un número: "))
    print(f"El doble es: {numero * 2}")
except ValueError:
    print("Error: Debes ingresar un número válido")
    numero = 0  # Valor por defecto
```

### Iteraciones y Bucles (`while`, `for`)
Automatizan tareas repetitivas iterando sobre bloques de código.

* **Bucle indefinido (`while`):** Se ejecuta mientras una condición sea `True`. Requiere una variable de iteración que cambie para evitar bucles infinitos.

```python
# Bucle while
contador = 0
while contador < 5:
    print(f"Contador: {contador}")
    contador += 1  # Importante: incrementar para evitar bucle infinito

# Salida: 0, 1, 2, 3, 4
```

* **Bucle definido (`for`):** Itera sobre un conjunto de elementos conocidos (como una lista, una tupla o las líneas de un archivo).

```python
# for con lista
frutas = ["manzana", "banana", "naranja"]
for fruta in frutas:
    print(fruta)

# for con range()
for i in range(5):  # 0, 1, 2, 3, 4
    print(i)

# range con inicio y fin
for i in range(2, 8):  # 2, 3, 4, 5, 6, 7
    print(i)

# range con paso
for i in range(0, 10, 2):  # 0, 2, 4, 6, 8
    print(i)
```

* **Modificadores de comportamiento:**
    * `break`: Termina el bucle inmediatamente y sale de él.
    * `continue`: Termina la iteración actual y salta a evaluar la condición de la siguiente iteración, ignorando el resto del código debajo.

```python
# break: sale del bucle completamente
for i in range(10):
    if i == 5:
        break  # Sale cuando i es 5
    print(i)
# Salida: 0, 1, 2, 3, 4

# continue: salta a la siguiente iteración
for i in range(5):
    if i == 2:
        continue  # Salta el 2
    print(i)
# Salida: 0, 1, 3, 4

# Ejemplo práctico: buscar elemento
numeros = [10, 20, 30, 40, 50]
buscar = 30

for numero in numeros:
    if numero == buscar:
        print(f"¡Encontrado: {numero}!")
        break
else:
    # Este else se ejecuta solo si NO se usó break
    print("No se encontró el número")
```

### Errores Comunes y Soluciones

```python
# ❌ Error: Bucle infinito (falta incrementar)
contador = 0
while contador < 5:
    print(contador)
    # Falta: contador += 1

# ❌ Error: Modificar lista mientras se itera
lista = [1, 2, 3, 4, 5]
for item in lista:
    lista.remove(item)  # Comportamiento impredecible

# ✅ Solución: iterar sobre una copia
for item in lista.copy():
    lista.remove(item)

# O usar list comprehension
lista = [x for x in lista if x != valor_a_eliminar]
```

---
*Nota: Documento generado para consolidar los conocimientos teóricos de la Unidad 1. Mantener este archivo actualizado ayudará a tener una referencia rápida para conceptos de arquitectura y lógica al momento de desarrollar.*