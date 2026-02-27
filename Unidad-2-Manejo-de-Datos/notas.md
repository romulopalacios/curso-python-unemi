# 📚 Notas Conceptuales - Unidad 2: Manejo de Datos Intermedio

Este documento sintetiza los conceptos de la Unidad 2 del curso de la UNEMI, enfocándose en la manipulación avanzada de datos, la encapsulación de lógica y la interacción con el sistema de archivos.

---

## Tema 1: Estructuras de Datos Complejas

Python ofrece colecciones nativas altamente optimizadas para manejar múltiples valores. Elegir la correcta es vital para el rendimiento y la memoria.

1. **Listas (`list`):**
   * **Características:** Ordenadas, mutables y permiten duplicados.
   * **Uso ideal:** Colecciones de elementos secuenciales.
   * *Técnica avanzada:* **List Comprehensions** `[e for e in lista if e > 0]`. Permite filtrar y transformar listas en una sola línea de código optimizada a nivel de C.
2. **Tuplas (`tuple`):**
   * **Características:** Ordenadas, **inmutables** y permiten duplicados.
   * **Uso ideal:** Datos que no deben cambiar durante la ejecución (ej. coordenadas, configuraciones fijas). Son más rápidas y ocupan menos memoria que las listas.
3. **Conjuntos (`set`):**
   * **Características:** No ordenadas, mutables, **sin elementos duplicados**. Sus elementos internos deben ser inmutables.
   * **Uso ideal:** Operaciones matemáticas de conjuntos (uniones, intersecciones) o para eliminar rápidamente duplicados de una lista.
4. **Diccionarios (`dict`):**
   * **Características:** Colecciones desordenadas (hasta Python 3.6) de pares **clave-valor**. 
   * **Uso ideal:** Estructurar datos complejos. Su lógica subyacente es una *tabla hash*, lo que hace que buscar un valor por su clave sea extremadamente rápido, sin importar el tamaño del diccionario. Es el formato base para manipular JSONs en APIs.

---

## Tema 2: Funciones y Programación Modular

La programación modular consiste en dividir un sistema grande en partes más pequeñas, independientes y reutilizables.

* **Definición de Funciones (`def`):** Encapsulan una lógica específica. Reciben entradas (parámetros) y devuelven una salida (`return`).
* **Tipos de Parámetros:**
  * *Posicionales:* Los valores se asignan en el orden en que se definen.
  * *Por defecto:* Se asigna un valor base desde la definición (ej. `def potencia(base, exponente=2):`). Si el usuario no envía el segundo argumento, la función no falla y usa el predeterminado.
* **Módulos:** Un archivo `.py` es un módulo. Al usar la palabra reservada `import` (ej. `import math`), estamos trayendo código estructurado por otros desarrolladores a nuestro programa, evitando reinventar la rueda.

---

## Tema 3: Manejo de Archivos y Excepciones

Para que un programa sea útil en el mundo real, debe poder interactuar con almacenamiento persistente (Memoria Secundaria) y manejar escenarios inesperados sin colapsar.

### Interacción con Archivos
Se utiliza el manejador de contexto `with open(...) as ...`. La ventaja del `with` es que se encarga de cerrar (`close()`) el archivo automáticamente al terminar, liberando recursos en el sistema operativo.
* **Modo Lectura (`"r"`):** Lee el contenido existente. Arroja error si el archivo no existe.
* **Modo Escritura (`"w"`):** Crea un archivo nuevo o **sobrescribe** uno existente desde cero.
* *(Nota: Existe el modo `"a"` (append) para agregar datos al final sin borrar lo anterior).*

### Manejo de Excepciones (`try / except`)
Anticipar el fallo es una regla de oro en ingeniería de software. 
En lugar de que el intérprete lance un *traceback* y detenga el programa de golpe, el bloque `try` "intenta" ejecutar un código riesgoso (ej. leer un archivo, convertir un texto a número). Si ocurre un error específico, el bloque `except` lo captura y ejecuta un plan de contingencia.
* Ejemplos de excepciones comunes: `ValueError` (dato incorrecto), `FileNotFoundError` (archivo no encontrado), `KeyError` (clave de diccionario inexistente).