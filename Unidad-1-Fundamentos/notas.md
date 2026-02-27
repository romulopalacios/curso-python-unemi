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
* **Nombres Mnemónicos:** Es una buena práctica usar nombres que describan el propósito del dato (ej. `velocidad_sensor` en lugar de `v`), evitando siempre las palabras reservadas de Python (como `class`, `yield`, `def`).

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
* **De Comparación:** `==`, `!=`, `>`, `<`, `>=`, `<=`. Evalúan condiciones y devuelven un booleano.
* **Lógicos:** `and`, `or`, `not`. Permiten agrupar y evaluar múltiples expresiones booleanas (Python utiliza la "evaluación en cortocircuito" para optimizar estas operaciones lógicas).

---

## 3. Control de Flujo: Condicionales y Bucles

El flujo de ejecución normal es secuencial (de arriba hacia abajo), pero podemos alterarlo mediante la lógica condicional y la iteración.

### Ejecución Condicional (`if`, `elif`, `else`)
Permite ramificar la ejecución del programa basándose en expresiones booleanas.
* Se pueden usar condicionales anidados, aunque por legibilidad de código se prefieren los condicionales encadenados (`elif`).
* **Manejo de Excepciones (`try` / `except`):** Una práctica de programación avanzada desde el día 1. En lugar de dejar que un error (como un `ValueError` al esperar un número y recibir un texto) detenga o "rompa" el programa, se "captura" el error de forma controlada.

### Iteraciones y Bucles (`while`, `for`)
Automatizan tareas repetitivas iterando sobre bloques de código.
* **Bucle indefinido (`while`):** Se ejecuta mientras una condición sea `True`. Requiere una variable de iteración que cambie para evitar bucles infinitos.
* **Bucle definido (`for`):** Itera sobre un conjunto de elementos conocidos (como una lista, una tupla o las líneas de un archivo).
* **Modificadores de comportamiento:**
    * `break`: Termina el bucle inmediatamente y sale de él.
    * `continue`: Termina la iteración actual y salta a evaluar la condición de la siguiente iteración, ignorando el resto del código debajo.

---
*Nota: Documento generado para consolidar los conocimientos teóricos de la Unidad 1. Mantener este archivo actualizado ayudará a tener una referencia rápida para conceptos de arquitectura y lógica al momento de desarrollar.*