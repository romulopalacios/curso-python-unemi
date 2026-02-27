# 📚 Notas Conceptuales - Unidad 3: POO y Scripts Automatizados

Este documento consolida los conceptos avanzados de diseño de software y automatización del sistema estudiados en la Unidad 3.

---

## Tema 1: Clases y Herencia

La Programación Orientada a Objetos (POO) nos permite agrupar datos (atributos) y comportamientos (métodos) en una sola entidad.


### 1. Clases y Objetos
* **Clase (`class`):** Es el "molde" o plantilla. A diferencia de otros lenguajes, en Python no se requiere sintaxis adicional como `new`.
* **Constructor (`__init__`):** Es el método mágico que se ejecuta automáticamente al instanciar (crear) un objeto. 
* **`self`:** Es el primer parámetro obligatorio en los métodos de instancia. Hace referencia al objeto mismo que está llamando al método, permitiendo acceder a sus propios atributos.

### 2. Herencia

Permite que una nueva clase (clase hija) adopte los atributos y métodos de una clase existente (clase padre), promoviendo la reutilización de código (principio DRY - *Don't Repeat Yourself*).
* **Sintaxis:** `class Estudiante(Persona):`
* **`super()`:** Se utiliza dentro de la clase hija para delegar responsabilidades al constructor o métodos de la clase padre. Ej: `super().__init__(nombre, edad)`.

---

## Tema 2: Polimorfismo y Encapsulamiento

### 1. Polimorfismo y *Duck Typing*
El polimorfismo permite que diferentes objetos respondan a una misma interfaz o llamada de método de manera distinta.
* **Duck Typing:** En Python rige el principio *"Si camina como pato y suena como pato, entonces es un pato"*. 

No es necesario que los objetos hereden de la misma clase madre para ser tratados igual; basta con que implementen el método esperado (ej. un método `sonido()` presente tanto en un `Felino` como en un `Pato`). Esto simplifica enormemente la creación de código genérico.

### 2. Encapsulamiento
Protege el estado interno de un objeto para evitar modificaciones accidentales desde el exterior.
* **Atributos privados:** En Python, el encapsulamiento se maneja por convención. Prefijar un atributo con doble guion bajo `__` activa el *name mangling*, dificultando su acceso directo desde afuera de la clase. Un solo guion bajo `_` indica que el atributo es de "uso interno".
* **Decorador `@property`:** Convierte un método para que pueda ser accedido como si fuera un atributo público (sin usar paréntesis `()`). Se combina con `@nombre.setter` para agregar lógica de validación antes de permitir que una variable externa modifique el dato interno.

---

## Tema 3: Creación de Scripts Automatizados

Python brilla en la automatización de tareas administrativas del sistema operativo. Para esto, utilizamos módulos de la biblioteca estándar que no requieren instalación previa:

* **Módulo `os`:** Permite interactuar con el sistema operativo subyacente. 
  * `os.path.exists()`: Verifica si una ruta o archivo es válido.
  * `os.listdir()`: Devuelve una lista con todos los elementos de un directorio.
  * `os.path.splitext()`: Separa de forma segura el nombre de un archivo de su extensión, ideal para categorizar datos.
* **Módulo `shutil`:** Ofrece operaciones de alto nivel sobre archivos y colecciones de archivos.
  * `shutil.move(origen, destino)`: Traslada archivos físicamente entre directorios, fundamental para crear *pipelines* de organización de descargas o datos crudos.