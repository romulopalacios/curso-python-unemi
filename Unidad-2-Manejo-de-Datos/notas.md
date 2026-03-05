# 📚 Notas Conceptuales - Unidad 2: Manejo de Datos Intermedio

Este documento sintetiza los conceptos de la Unidad 2 del curso de la UNEMI, enfocándose en la manipulación avanzada de datos, la encapsulación de lógica y la interacción con el sistema de archivos.

---

## Tema 1: Estructuras de Datos Complejas

Python ofrece colecciones nativas altamente optimizadas para manejar múltiples valores. Elegir la correcta es vital para el rendimiento y la memoria.

1. **Listas (`list`):**
   * **Características:** Ordenadas, mutables y permiten duplicados.
   * **Uso ideal:** Colecciones de elementos secuenciales.
   
   ```python
   # Crear listas
   numeros = [1, 2, 3, 4, 5]
   frutas = ["manzana", "banana", "naranja"]
   mixta = [1, "texto", 3.14, True]  # Pueden mezclar tipos
   
   # Acceso por índice
   print(frutas[0])     # "manzana"
   print(frutas[-1])    # "último elemento: naranja"
   
   # Modificar (mutables)
   frutas[1] = "fresa"
   frutas.append("uva")      # Añadir al final
   frutas.insert(1, "kiwi")  # Insertar en posición
   frutas.remove("manzana")  # Eliminar por valor
   eliminado = frutas.pop()  # Eliminar y retornar último
   
   # Slicing (rebanado)
   print(frutas[1:3])   # Elementos del índice 1 al 2
   print(frutas[:2])    # Primeros 2 elementos
   print(frutas[2:])    # Desde el índice 2 hasta el final
   ```
   
   * *Técnica avanzada:* **List Comprehensions** `[e for e in lista if e > 0]`. Permite filtrar y transformar listas en una sola línea de código optimizada a nivel de C.
   
   ```python
   # Forma tradicional
   cuadrados = []
   for x in range(10):
       cuadrados.append(x ** 2)
   
   # List comprehension (más eficiente)
   cuadrados = [x ** 2 for x in range(10)]
   
   # Con filtro
   pares = [x for x in range(20) if x % 2 == 0]
   
   # Transformación compleja
   nombres = ["ana", "juan", "pedro"]
   nombres_upper = [n.upper() for n in nombres]
   # Resultado: ["ANA", "JUAN", "PEDRO"]
   ```
2. **Tuplas (`tuple`):**
   * **Características:** Ordenadas, **inmutables** y permiten duplicados.
   * **Uso ideal:** Datos que no deben cambiar durante la ejecución (ej. coordenadas, configuraciones fijas). Son más rápidas y ocupan menos memoria que las listas.
   
   ```python
   # Crear tuplas
   coordenadas = (10, 20)
   persona = ("Ana", 25, "Python Developer")
   un_elemento = (42,)  # Nota: coma necesaria para tupla de 1 elemento
   
   # Acceso (igual que listas)
   print(coordenadas[0])    # 10
   print(persona[-1])       # "Python Developer"
   
   # Inmutables: NO se pueden modificar
   # coordenadas[0] = 15    # Error: TypeError
   
   # Desempaquetado de tuplas
   x, y = coordenadas
   nombre, edad, profesion = persona
   print(f"{nombre} tiene {edad} años")
   
   # Tuplas como claves de diccionario (listas no pueden)
   mapa = {
       (0, 0): "origen",
       (1, 0): "este",
       (0, 1): "norte"
   }
   print(mapa[(0, 0)])  # "origen"
   
   # Ventaja de memoria
   import sys
   lista = [1, 2, 3, 4, 5]
   tupla = (1, 2, 3, 4, 5)
   print(sys.getsizeof(lista))  # ~104 bytes
   print(sys.getsizeof(tupla))  # ~80 bytes
   ```
3. **Conjuntos (`set`):**
   * **Características:** No ordenadas, mutables, **sin elementos duplicados**. Sus elementos internos deben ser inmutables.
   * **Uso ideal:** Operaciones matemáticas de conjuntos (uniones, intersecciones) o para eliminar rápidamente duplicados de una lista.
   
   ```python
   # Crear conjuntos
   numeros = {1, 2, 3, 4, 5}
   letras = set(["a", "b", "c"])
   
   # Elimina duplicados automáticamente
   duplicados = {1, 2, 2, 3, 3, 3, 4}
   print(duplicados)  # {1, 2, 3, 4}
   
   # Añadir y eliminar
   numeros.add(6)
   numeros.remove(1)      # Error si no existe
   numeros.discard(10)    # No da error si no existe
   
   # Operaciones de conjuntos
   a = {1, 2, 3, 4}
   b = {3, 4, 5, 6}
   
   print(a | b)  # Unión: {1, 2, 3, 4, 5, 6}
   print(a & b)  # Intersección: {3, 4}
   print(a - b)  # Diferencia: {1, 2}
   print(a ^ b)  # Diferencia simétrica: {1, 2, 5, 6}
   
   # Caso de uso: eliminar duplicados de lista
   lista_con_duplicados = [1, 2, 2, 3, 3, 3, 4, 5, 5]
   sin_duplicados = list(set(lista_con_duplicados))
   print(sin_duplicados)  # [1, 2, 3, 4, 5]
   ```
4. **Diccionarios (`dict`):**
   * **Características:** Colecciones de pares **clave-valor**. Desde Python 3.7+ mantienen el orden de inserción.
   * **Uso ideal:** Estructurar datos complejos. Su lógica subyacente es una *tabla hash*, lo que hace que buscar un valor por su clave sea extremadamente rápido (O(1)), sin importar el tamaño del diccionario. Es el formato base para manipular JSONs en APIs.
   
   ```python
   # Crear diccionarios
   persona = {
       "nombre": "Ana",
       "edad": 25,
       "ciudad": "Quito"
   }
   
   # Acceso por clave
   print(persona["nombre"])        # "Ana"
   print(persona.get("edad"))      # 25
   print(persona.get("país", "Ecuador"))  # Valor por defecto si no existe
   
   # Modificar y agregar
   persona["edad"] = 26            # Modificar
   persona["profesión"] = "Ingeniera"  # Agregar nueva clave
   
   # Eliminar
   del persona["ciudad"]
   profesion = persona.pop("profesión")  # Elimina y retorna valor
   
   # Iterar sobre diccionarios
   for clave in persona:
       print(f"{clave}: {persona[clave]}")
   
   # Métodos útiles
   print(persona.keys())    # dict_keys(['nombre', 'edad'])
   print(persona.values())  # dict_values(['Ana', 26])
   print(persona.items())   # dict_items([('nombre', 'Ana'), ('edad', 26)])
   
   # Diccionarios anidados (simular base de datos)
   empleados = {
       "001": {
           "nombre": "Carlos",
           "salario": 2500,
           "departamento": "IT"
       },
       "002": {
           "nombre": "María",
           "salario": 3000,
           "departamento": "Ventas"
       }
   }
   
   # Acceso anidado
   print(empleados["001"]["nombre"])  # "Carlos"
   
   # Complejidad O(1) - búsqueda instantánea
   # No importa si el diccionario tiene 10 o 1,000,000 elementos
   salario_carlos = empleados["001"]["salario"]  # Instantáneo
   ```

---

## Tema 2: Funciones y Programación Modular

La programación modular consiste en dividir un sistema grande en partes más pequeñas, independientes y reutilizables.

* **Definición de Funciones (`def`):** Encapsulan una lógica específica. Reciben entradas (parámetros) y devuelven una salida (`return`).

```python
# Función simple
def saludar(nombre):
    """Retorna un saludo personalizado"""
    return f"Hola, {nombre}!"

resultado = saludar("Ana")
print(resultado)  # "Hola, Ana!"

# Función con múltiples parámetros
def calcular_area_rectangulo(base, altura):
    """Calcula el área de un rectángulo"""
    area = base * altura
    return area

print(calcular_area_rectangulo(5, 3))  # 15
```

* **Tipos de Parámetros:**
  * *Posicionales:* Los valores se asignan en el orden en que se definen.
  * *Por defecto:* Se asigna un valor base desde la definición (ej. `def potencia(base, exponente=2):`). Si el usuario no envía el segundo argumento, la función no falla y usa el predeterminado.

```python
# Parámetros por defecto
def potencia(base, exponente=2):
    """Eleva base al exponente (por defecto 2)"""
    return base ** exponente

print(potencia(5))      # 25 (usa exponente=2 por defecto)
print(potencia(5, 3))   # 125 (exponente explícito)

# Parámetros con nombre (keyword arguments)
print(potencia(exponente=3, base=2))  # Orden no importa

# *args y **kwargs para argumentos variables
def sumar_todos(*numeros):
    """Suma cualquier cantidad de números"""
    return sum(numeros)

print(sumar_todos(1, 2, 3))        # 6
print(sumar_todos(1, 2, 3, 4, 5))  # 15

def crear_perfil(**datos):
    """Crea un perfil con datos variables"""
    for clave, valor in datos.items():
        print(f"{clave}: {valor}")

crear_perfil(nombre="Ana", edad=25, ciudad="Quito")
```

* **Módulos:** Un archivo `.py` es un módulo. Al usar la palabra reservada `import` (ej. `import math`), estamos trayendo código estructurado por otros desarrolladores a nuestro programa, evitando reinventar la rueda.

```python
# Importar módulo completo
import math
print(math.sqrt(16))    # 4.0
print(math.pi)          # 3.141592653589793

# Importar funciones específicas
from math import sqrt, pi, cos
print(sqrt(25))         # 5.0

# Importar con alias
import datetime as dt
ahora = dt.datetime.now()
print(ahora)

# Crear tu propio módulo
# Archivo: mis_funciones.py
# def mi_funcion():
#     return "Hola desde el módulo"

# Usar tu módulo
# import mis_funciones
# mis_funciones.mi_funcion()
```

### Scope (Alcance de Variables)

```python
# Variable global
x = 10

def modificar():
    # Variable local (no afecta la global)
    x = 20
    print(f"Dentro de la función: {x}")  # 20

modificar()
print(f"Fuera de la función: {x}")  # 10 (no cambió)

# Modificar variable global
def modificar_global():
    global x
    x = 30

modificar_global()
print(x)  # 30 (sí cambió)
```

---

## Tema 3: Manejo de Archivos y Excepciones

Para que un programa sea útil en el mundo real, debe poder interactuar con almacenamiento persistente (Memoria Secundaria) y manejar escenarios inesperados sin colapsar.

### Interacción con Archivos
Se utiliza el manejador de contexto `with open(...) as ...`. La ventaja del `with` es que se encarga de cerrar (`close()`) el archivo automáticamente al terminar, liberando recursos en el sistema operativo.

```python
# Escribir archivo
with open("ejemplo.txt", "w") as archivo:
    archivo.write("Primera línea\n")
    archivo.write("Segunda línea\n")
    archivo.writelines(["Tercera\n", "Cuarta\n"])

# Leer archivo completo
with open("ejemplo.txt", "r") as archivo:
    contenido = archivo.read()
    print(contenido)

# Leer línea por línea (eficiente para archivos grandes)
with open("ejemplo.txt", "r") as archivo:
    for linea in archivo:
        print(linea.strip())  # strip() quita \n
# Leer todas las líneas en una lista
with open("ejemplo.txt", "r") as archivo:
    lineas = archivo.readlines()
    print(lineas)  # ['Primera línea\n', 'Segunda línea\n', ...]
```

* **Modo Lectura (`"r"`):** Lee el contenido existente. Arroja error si el archivo no existe.
* **Modo Escritura (`"w"`):** Crea un archivo nuevo o **sobrescribe** uno existente desde cero.
* **Modo Append (`"a"`):** Agrega datos al final sin borrar lo anterior.
* **Modo Binario (`"rb"`, `"wb"`):** Para archivos no texto (imágenes, PDFs, etc.)

```python
# Append: agregar sin borrar
with open("ejemplo.txt", "a") as archivo:
    archivo.write("Línea adicional\n")

# Trabajar con rutas
import os

# Verificar si existe
if os.path.exists("ejemplo.txt"):
    print("El archivo existe")

# Obtener ruta absoluta
ruta_absoluta = os.path.abspath("ejemplo.txt")
print(ruta_absoluta)

# Crear directorios
os.makedirs("datos/procesados", exist_ok=True)
```

### Manejo de Excepciones (`try / except`)
Anticipar el fallo es una regla de oro en ingeniería de software. 

En lugar de que el intérprete lance un *traceback* y detenga el programa de golpe, el bloque `try` "intenta" ejecutar un código riesgoso (ej. leer un archivo, convertir un texto a número). Si ocurre un error específico, el bloque `except` lo captura y ejecuta un plan de contingencia.

```python
# Manejo básico
try:
    numero = int(input("Ingresa un número: "))
    resultado = 10 / numero
    print(f"Resultado: {resultado}")
except ValueError:
    print("Error: Debes ingresar un número válido")
except ZeroDivisionError:
    print("Error: No se puede dividir entre cero")

# Múltiples excepciones en un bloque
try:
    archivo = open("datos.txt", "r")
    contenido = archivo.read()
except (FileNotFoundError, PermissionError) as e:
    print(f"Error al abrir archivo: {e}")

# try-except-else-finally
try:
    archivo = open("datos.txt", "r")
    datos = archivo.read()
except FileNotFoundError:
    print("Archivo no encontrado")
else:
    # Se ejecuta si NO hubo excepciones
    print("Archivo leído exitosamente")
    print(f"Tamaño: {len(datos)} caracteres")
finally:
    # SIEMPRE se ejecuta (haya o no error)
    try:
        archivo.close()
        print("Archivo cerrado")
    except:
        pass

# Capturar cualquier excepción
try:
    operacion_riesgosa()
except Exception as e:
    print(f"Error inesperado: {type(e).__name__}: {e}")

# Lanzar excepciones personalizadas
def validar_edad(edad):
    if edad < 0:
        raise ValueError("La edad no puede ser negativa")
    if edad > 150:
        raise ValueError("Edad inválida")
    return True

try:
    validar_edad(-5)
except ValueError as e:
    print(f"Error de validación: {e}")
```

* Ejemplos de excepciones comunes: 
  - `ValueError`: dato incorrecto (ej. int("abc"))
  - `FileNotFoundError`: archivo no encontrado
  - `KeyError`: clave de diccionario inexistente
  - `IndexError`: índice fuera de rango en lista
  - `TypeError`: operación con tipos incompatibles
  - `ZeroDivisionError`: división entre cero
  - `ImportError`: módulo no encontrado

### Mejores Prácticas

```python
# ❌ Malo: capturar todo sin especificar
try:
    codigo()
except:
    pass  # Oculta todos los errores, incluso bugs

# ✅ Bueno: excepciones específicas
try:
    codigo()
except ValueError as e:
    print(f"Error de valor: {e}")
except KeyError as e:
    print(f"Clave no encontrada: {e}")

# ❌ Malo: try-except muy amplio
try:
    linea1()
    linea2()
    linea3()
    # ... 100 líneas más
except ValueError:
    print("Error")  # ¿Dónde ocurrió?

# ✅ Bueno: try-except específico y acotado
try:
    numero = int(entrada)  # Solo la parte riesgosa
except ValueError:
    print("Entrada inválida")
    numero = 0
```

---

*Documento actualizado para proporcionar ejemplos prácticos completos de todas las estructuras de datos, funciones, archivos y manejo de excepciones. Cada concepto ahora incluye código ejecutable y casos de uso reales.*