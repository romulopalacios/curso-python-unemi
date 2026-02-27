# 🎯 Unidad 3: POO y Automatización de Scripts
### Programación Orientada a Objetos y Scripting de Sistema

[![Python](https://img.shields.io/badge/Python-Avanzado-red.svg)](https://www.python.org/)
[![Status](https://img.shields.io/badge/Status-Completado-success.svg)]()

---

## 🎯 Objetivos de Aprendizaje

Al finalizar esta unidad, serás capaz de:

- ✅ Diseñar y crear clases con atributos y métodos
- ✅ Implementar el constructor `__init__` y entender el uso de `self`
- ✅ Aplicar herencia para reutilizar código y extender funcionalidades
- ✅ Utilizar `super()` para delegar al constructor de la clase padre
- ✅ Implementar polimorfismo mediante Duck Typing
- ✅ Aplicar encapsulamiento con atributos privados y `@property`
- ✅ Automatizar tareas del sistema operativo con `os` y `shutil`
- ✅ Crear scripts que organicen archivos por extensión automáticamente
- ✅ Modelar entidades del mundo real con POO

---

## 📚 Contenido de la Unidad

### Tema 1: Clases y Herencia

**Conceptos clave:**
- Programación Orientada a Objetos (POO)
- Clases como plantillas/moldes para crear objetos
- Constructor `__init__`: inicialización automática de objetos
- Parámetro `self`: referencia al objeto instanciado
- Atributos de instancia vs atributos de clase
- Métodos de instancia
- Herencia: reutilización de código mediante extensión
- `super()`: delegación al constructor de la clase padre
- Relaciones "es-un" (Estudiante es una Persona)

**📄 Archivo de práctica:**  
[`u3_tema_1_clases,_herencias.py`](./u3_tema_1_clases,_herencias.py)

**Ejercicios incluidos:**
- Definición de clase `Persona` con constructor
- Creación de instancias y llamada a métodos
- Implementación de herencia: clase `Estudiante` extiende `Persona`
- Uso de `super().__init__()` para reutilizar el constructor padre
- Sobrescritura (override) de métodos en clases hijas

---

### Tema 2: Polimorfismo y Encapsulamiento

**Conceptos clave:**
- Polimorfismo: misma interfaz, comportamientos diferentes
- Duck Typing: "Si camina como pato y suena como pato, es un pato"
- Múltiples clases respondiendo al mismo método sin herencia común
- Encapsulamiento: protección del estado interno
- Convenciones de privacidad: `_atributo` (interno) y `__atributo` (privado)
- Name mangling con doble guion bajo
- Decorador `@property`: acceso controlado a atributos
- `@nombre.setter`: validación antes de modificar atributos
- Getters y setters Pythónicos

**📄 Archivo de práctica:**  
[`u3_tema_2_polimorfismo.py`](./u3_tema_2_polimorfismo.py)

**Ejercicios incluidos:**
- Implementación de múltiples clases con método común `sonido()`
- Demostración de Duck Typing sin jerarquía de herencia
- Función genérica que trabaja con cualquier objeto que tenga el método esperado
- Uso de `@property` para getters
- Uso de `@atributo.setter` para validación de datos

---

### Tema 3: Creación de Scripts Automatizados

**Conceptos clave:**
- Automatización de tareas del sistema operativo
- Módulo `os`: interacción con el sistema de archivos
  - `os.path.exists()`: verificación de rutas
  - `os.listdir()`: listar contenido de directorios
  - `os.path.splitext()`: separar nombre y extensión
  - `os.makedirs()`: crear directorios recursivamente
- Módulo `shutil`: operaciones de alto nivel con archivos
  - `shutil.move()`: mover archivos entre directorios
  - `shutil.copy()`: copiar archivos
- Organización automática de archivos por tipo/extensión
- Scripting para administración del sistema
- Pipelines de procesamiento de datos

**📄 Archivo de práctica:**  
[`u3_tema_3_creación_de_scripts_automatizados.py`](./u3_tema_3_creación_de_scripts_automatizados.py)

**Ejercicios incluidos:**
- Lectura y listado de archivos en un directorio
- Extracción de extensiones de archivos
- Creación de carpetas por tipo de archivo
- Script para organizar descargas automáticamente
- Movimiento de archivos basado en extensión

---

## 📖 Notas Conceptuales Detalladas

Para una comprensión profunda de POO, patrones de diseño y automatización, consulta:

### 👉 [**notas.md - Documentación Conceptual Completa**](./notas.md)

Este documento incluye:
- Fundamentos de Programación Orientada a Objetos
- Diferencias entre clases y objetos
- Herencia vs Composición
- Duck Typing y tipado dinámico de Python
- Mejores prácticas de encapsulamiento
- Guía completa de módulos `os` y `shutil`
- Casos de uso reales de automatización

---

## 🚀 Cómo Ejecutar las Prácticas

### Desde la Terminal / CMD

```bash
# Navegar a la carpeta de la Unidad 3
cd Unidad-3-POO-Automatizacion

# Ejecutar práctica de clases y herencia
python u3_tema_1_clases,_herencias.py

# Ejecutar práctica de polimorfismo
python u3_tema_2_polimorfismo.py

# Ejecutar script de automatización
python u3_tema_3_creación_de_scripts_automatizados.py
```

**⚠️ Nota importante:** El script del Tema 3 interactúa con el sistema de archivos. Asegúrate de:
- Revisar el código antes de ejecutarlo
- Tener backup de archivos importantes
- Entender qué directorios va a modificar

### Desde VS Code

1. Abre el archivo `.py` que deseas ejecutar
2. Revisa el código para entender qué hará (especialmente en scripts de automatización)
3. Presiona `F5` o usa el botón ▶️ "Run Python File"
4. Observa la salida en la terminal integrada

---

## 💡 Principios SOLID Aplicados

Esta unidad introduce conceptos fundamentales de diseño de software:

| Principio | Aplicación en esta Unidad |
|-----------|---------------------------|
| **Single Responsibility** | Cada clase tiene una única responsabilidad clara |
| **Open/Closed** | Clases abiertas para extensión (herencia) pero cerradas para modificación |
| **Liskov Substitution** | Las clases hijas pueden sustituir a las padres sin romper el código |
| **Interface Segregation** | Duck Typing permite interfaces implícitas mínimas |
| **Dependency Inversion** | Código genérico que depende de interfaces, no implementaciones |

---

## 🎓 Conceptos de POO en Acción

### Anatomía de una Clase

```python
class Persona:                          # Definición de clase
    def __init__(self, nombre, edad):   # Constructor
        self.nombre = nombre            # Atributo de instancia
        self.edad = edad
    
    def presentarse(self):              # Método
        return f"Soy {self.nombre}"
```

### Herencia

```python
class Estudiante(Persona):              # Herencia
    def __init__(self, nombre, edad, curso):
        super().__init__(nombre, edad)  # Llamada al padre
        self.curso = curso              # Atributo adicional
```

### Polimorfismo con Duck Typing

```python
def hacer_sonar(animal):                # Función genérica
    print(animal.sonido())              # Funciona con cualquier objeto que tenga sonido()
```

---

## 🏗️ Casos de Uso en el Mundo Real

### POO se usa en:
- 🎮 **Desarrollo de juegos:** Cada personaje/enemigo es una clase
- 🌐 **Frameworks web:** Flask, Django usan POO extensivamente
- 📊 **Análisis de datos:** Pandas usa clases (DataFrame, Series)
- 🤖 **Machine Learning:** Scikit-learn estructura modelos como clases
- 🏢 **Sistemas empresariales:** Modelado de entidades (Cliente, Producto, Orden)

### Scripts de Automatización se usan en:
- 📁 **DevOps:** Organización de logs y archivos de configuración
- 📸 **Fotografía digital:** Ordenar fotos por fecha/tipo
- 📥 **Gestión de descargas:** Clasificar automáticamente archivos descargados
- 🔄 **ETL pipelines:** Mover y transformar datos entre sistemas
- 🧹 **Limpieza de sistemas:** Scripts de mantenimiento periódico

---

## 🔗 Recursos Adicionales

- 📘 [Python para Todos - Capítulo 14: POO](https://www.py4e.com/book)
- 📄 [Documentación Oficial - Clases](https://docs.python.org/3/tutorial/classes.html)
- 📄 [Documentación - Módulo os](https://docs.python.org/3/library/os.html)
- 📄 [Documentación - Módulo shutil](https://docs.python.org/3/library/shutil.html)
- 🎯 [Real Python - OOP in Python](https://realpython.com/python3-object-oriented-programming/)
- 📚 [Design Patterns en Python](https://refactoring.guru/design-patterns/python)

---

## ✅ Checklist de Dominio

Marca tu progreso:

- [ ] Puedo crear clases con atributos y métodos
- [ ] Entiendo la diferencia entre `self`, atributos y parámetros
- [ ] Sé cuándo usar herencia para extender funcionalidad
- [ ] Uso `super()` correctamente para llamar al constructor padre
- [ ] Implemento Duck Typing sin depender de herencia estricta
- [ ] Aplico encapsulamiento con `_` y `__` apropiadamente
- [ ] Uso `@property` para getters/setters Pythónicos
- [ ] Puedo automatizar tareas con `os` y `shutil`
- [ ] Entiendo los riesgos de scripts que modifican archivos
- [ ] Modelar entidades del mundo real con clases

---

## 🧪 Desafíos Propuestos

Para reforzar tu aprendizaje:

1. **POO:** Crea un sistema de gestión de biblioteca con clases `Libro`, `Biblioteca` y `Usuario`
2. **Herencia:** Extiende el sistema con clases `LibroDigital` y `LibroFisico`
3. **Polimorfismo:** Implementa un método `prestar()` que funcione diferente para cada tipo
4. **Automatización:** Crea un script que organice tu carpeta de Descargas por fecha y tipo

---

## 📌 Unidades Relacionadas

### ⬅️ Prerequisito
[**Unidad 2: Manejo de Datos**](../Unidad-2-Manejo-de-Datos) - Repasar funciones y estructuras de datos antes de POO.

### ➡️ Siguiente
**Unidad 4: Temas Avanzados** *(Si aplica)* - Decoradores, generadores, context managers personalizados.

---

<div align="center">
  <sub>Parte del Curso de Python - UNEMI 2026</sub>
</div>