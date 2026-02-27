# 📦 Unidad 2: Manejo de Datos y Programación Intermedia
### Estructuras Complejas, Modularidad y Persistencia

[![Python](https://img.shields.io/badge/Python-Intermedio-orange.svg)](https://www.python.org/)
[![Status](https://img.shields.io/badge/Status-Completado-success.svg)]()

---

## 🎯 Objetivos de Aprendizaje

Al finalizar esta unidad, serás capaz de:

- ✅ Elegir la estructura de datos correcta según el caso de uso (listas, tuplas, sets, diccionarios)
- ✅ Aplicar list comprehensions para código más eficiente y Pythónico
- ✅ Realizar operaciones matemáticas de conjuntos (uniones, intersecciones)
- ✅ Estructurar datos complejos con diccionarios anidados (simulación de bases de datos)
- ✅ Crear funciones reutilizables con parámetros posicionales y por defecto
- ✅ Importar y utilizar módulos de la biblioteca estándar
- ✅ Leer y escribir archivos de texto usando context managers (`with`)
- ✅ Implementar manejo robusto de excepciones con `try/except`

---

## 📚 Contenido de la Unidad

### Tema 1: Estructuras de Datos Complejas

**Conceptos clave:**
- Listas (`list`): ordenadas, mutables, permiten duplicados
- Tuplas (`tuple`): ordenadas, **inmutables**, más eficientes en memoria
- Conjuntos (`set`): no ordenados, sin duplicados, operaciones matemáticas
- Diccionarios (`dict`): pares clave-valor, búsqueda O(1) con tablas hash
- List comprehensions: sintaxis compacta para filtrar y transformar
- Diccionarios anidados: estructuración de datos complejos

**📄 Archivo de práctica:**  
[`u2_tema_1_listas,_tuplas,_conjuntos_y_diccionarios.py`](./u2_tema_1_listas,_tuplas,_conjuntos_y_diccionarios.py)

**Ejercicios incluidos:**
- Filtrado de empleados con list comprehensions
- Ordenamiento personalizado con `sorted()` y `lambda`
- Uso de tuplas como claves de diccionarios (coordenadas)
- Desempaquetado de tuplas
- Operaciones de conjuntos (unión, intersección, diferencia)
- Manejo de diccionarios anidados para datos estructurados

---

### Tema 2: Funciones y Programación Modular

**Conceptos clave:**
- Definición de funciones con `def`
- Parámetros posicionales vs parámetros por defecto
- Retorno de valores con `return`
- Alcance de variables (scope): local vs global
- Importación de módulos nativos (`import math`, `import datetime`)
- Principio DRY (Don't Repeat Yourself)
- Encapsulación de lógica reutilizable

**📄 Archivo de práctica:**  
[`u2_tema_2_funciones_y_programación_modular.py`](./u2_tema_2_funciones_y_programación_modular.py)

**Ejercicios incluidos:**
- Función básica de saludo con parámetros
- Cálculo de área de rectángulo con múltiples parámetros
- Función de potencia con exponente por defecto
- Uso del módulo `math` para operaciones matemáticas avanzadas

---

### Tema 3: Manejo de Archivos y Excepciones

**Conceptos clave:**
- Context manager `with open()` - gestión automática de recursos
- Modos de apertura: `"r"` (lectura), `"w"` (escritura), `"a"` (append)
- Lectura completa vs lectura por líneas
- Escritura y creación de archivos
- Manejo estructurado de excepciones: `try/except`
- Excepciones comunes: `ValueError`, `FileNotFoundError`, `KeyError`
- Estrategias de contingencia y recuperación de errores
- Memoria secundaria: persistencia de datos

**📄 Archivo de práctica:**  
[`u2_tema_3_manejo_de_archivos_y_excepciones.py`](./u2_tema_3_manejo_de_archivos_y_excepciones.py)

**Ejercicios incluidos:**
- Escritura de archivo de texto desde Python
- Lectura de contenido de archivos
- Captura de `ValueError` en conversión de tipos
- Captura de `FileNotFoundError` al intentar abrir archivos inexistentes

---

## 📖 Notas Conceptuales Detalladas

Para una comprensión profunda de los conceptos teóricos, aplicaciones prácticas y perspectivas de ingeniería, consulta:

### 👉 [**notas.md - Documentación Conceptual Completa**](./notas.md)

Este documento incluye:
- Comparación detallada de estructuras de datos y cuándo usar cada una
- Optimización de rendimiento con list comprehensions
- Patrones de diseño modular y reutilización de código
- Gestión de recursos con context managers
- Estrategias profesionales de manejo de excepciones
- Preparación para trabajo con APIs (diccionarios ≈ JSON)

---

## 🚀 Cómo Ejecutar las Prácticas

### Desde la Terminal / CMD

```bash
# Navegar a la carpeta de la Unidad 2
cd Unidad-2-Manejo-de-Datos

# Ejecutar práctica de estructuras de datos
python u2_tema_1_listas,_tuplas,_conjuntos_y_diccionarios.py

# Ejecutar práctica de funciones
python u2_tema_2_funciones_y_programación_modular.py

# Ejecutar práctica de archivos y excepciones
python u2_tema_3_manejo_de_archivos_y_excepciones.py
```

**Nota:** El script del Tema 3 creará un archivo `ejemplo.txt` en el directorio actual.

### Desde VS Code

1. Abre el archivo `.py` que deseas ejecutar
2. Asegúrate de que el terminal esté en la carpeta correcta
3. Presiona `F5` o usa el botón ▶️ "Run Python File"
4. Observa la salida en la terminal integrada

---

## 💡 Matriz de Decisión: ¿Qué Estructura Usar?

| Necesitas... | Usa |
|--------------|-----|
| Lista ordenada que se puede modificar | `list` |
| Secuencia inmutable (datos fijos) | `tuple` |
| Eliminar duplicados automáticamente | `set` |
| Almacenar pares clave-valor (como JSON) | `dict` |
| Acceso rápido O(1) por identificador | `dict` |
| Operaciones matemáticas de conjuntos | `set` |
| Menor consumo de memoria (datos fijos) | `tuple` |

---

## 🎓 Conceptos Avanzados Introducidos

### List Comprehensions
```python
# Forma tradicional
resultado = []
for x in lista:
    if x > 0:
        resultado.append(x)

# List comprehension (más eficiente)
resultado = [x for x in lista if x > 0]
```

### Lambda Functions
```python
# Función anónima para ordenar por un criterio
empleados_ordenados = sorted(empleados, key=lambda e: e["edad"])
```

### Context Managers
```python
# Se cierra automáticamente al salir del bloque
with open("archivo.txt", "r") as f:
    contenido = f.read()
```

---

## 🔗 Recursos Adicionales

- 📘 [Python para Todos - Capítulos 6-10](https://www.py4e.com/book)
- 📄 [Documentación: Built-in Types](https://docs.python.org/3/library/stdtypes.html)
- 📄 [Documentación: File I/O](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)
- 🎯 [PEP 8 - List Comprehensions](https://pep8.org/#programming-recommendations)
- 📊 [Time Complexity de Estructuras](https://wiki.python.org/moin/TimeComplexity)

---

## ✅ Checklist de Dominio

Marca tu progreso:

- [ ] Puedo elegir entre lista, tupla, set o diccionario según el caso de uso
- [ ] Escribo list comprehensions en lugar de bucles simples
- [ ] Entiendo la complejidad algorítmica de cada estructura (ej: dict lookup O(1))
- [ ] Creo funciones con parámetros por defecto apropiadamente
- [ ] Uso `import` para evitar reinventar la rueda
- [ ] Siempre uso `with open()` para archivos (nunca `open()` solo)
- [ ] Implemento `try/except` en operaciones de I/O y conversiones
- [ ] Entiendo qué excepciones específicas capturar

---

## 🏗️ Conexión con el Mundo Real

Los conceptos de esta unidad son fundamentales para:

- **Backend Development:** Diccionarios = Objetos JSON en APIs REST
- **Data Science:** Estructuración y limpieza de datasets
- **DevOps:** Lectura/escritura de archivos de configuración
- **Scripting:** Automatización de tareas del sistema operativo
- **Bases de Datos:** Mapeo de registros a diccionarios (ORM)

---

## 📌 Unidades Relacionadas

### ⬅️ Prerequisito
[**Unidad 1: Fundamentos**](../Unidad-1-Fundamentos) - Si necesitas repasar variables, tipos de datos o control de flujo.

### ➡️ Siguiente
[**Unidad 3: Conceptos Avanzados**](../Unidad-3-Por-Definir) *(Próximamente)* - POO, decoradores, generadores, etc.

---

<div align="center">
  <sub>Parte del Curso de Python - UNEMI 2026</sub>
</div>