# 📚 Notas Conceptuales - Unidad 3: POO y Scripts Automatizados

Este documento consolida los conceptos avanzados de diseño de software y automatización del sistema estudiados en la Unidad 3.

---

## Tema 1: Clases y Herencia

La Programación Orientada a Objetos (POO) nos permite agrupar datos (atributos) y comportamientos (métodos) en una sola entidad.


### 1. Clases y Objetos
* **Clase (`class`):** Es el "molde" o plantilla. A diferencia de otros lenguajes, en Python no se requiere sintaxis adicional como `new`.
* **Constructor (`__init__`):** Es el método mágico que se ejecuta automáticamente al instanciar (crear) un objeto. 
* **`self`:** Es el primer parámetro obligatorio en los métodos de instancia. Hace referencia al objeto mismo que está llamando al método, permitiendo acceder a sus propios atributos.

```python
# Definir una clase
class Persona:
    # Constructor
    def __init__(self, nombre, edad):
        self.nombre = nombre  # Atributo de instancia
        self.edad = edad
    
    # Método de instancia
    def saludar(self):
        return f"Hola, soy {self.nombre} y tengo {self.edad} años"
    
    # Método que modifica el estado
    def cumplir_anios(self):
        self.edad += 1
        print(f"¡Feliz cumpleaños! Ahora tienes {self.edad} años")

# Crear objetos (instancias)
persona1 = Persona("Ana", 25)
persona2 = Persona("Carlos", 30)

# Usar métodos
print(persona1.saludar())  # "Hola, soy Ana y tengo 25 años"
print(persona2.saludar())  # "Hola, soy Carlos y tengo 30 años"

# Acceder y modificar atributos
print(persona1.nombre)  # "Ana"
persona1.cumplir_anios()  # ¡Feliz cumpleaños! Ahora tienes 26 años

# Atributos de clase (compartidos por todas las instancias)
class Estudiante:
    escuela = "UNEMI"  # Atributo de clase
    
    def __init__(self, nombre):
        self.nombre = nombre  # Atributo de instancia
    
    def mostrar_info(self):
        return f"{self.nombre} estudia en {Estudiante.escuela}"

est1 = Estudiante("Juan")
est2 = Estudiante("María")

print(est1.mostrar_info())  # "Juan estudia en UNEMI"
print(est2.mostrar_info())  # "María estudia en UNEMI"

# Cambiar atributo de clase afecta a todos
Estudiante.escuela = "Universidad UNEMI"
print(est1.mostrar_info())  # "Juan estudia en Universidad UNEMI"
```

### 2. Herencia

Permite que una nueva clase (clase hija) adopte los atributos y métodos de una clase existente (clase padre), promoviendo la reutilización de código (principio DRY - *Don't Repeat Yourself*).
* **Sintaxis:** `class Estudiante(Persona):`
* **`super()`:** Se utiliza dentro de la clase hija para delegar responsabilidades al constructor o métodos de la clase padre. Ej: `super().__init__(nombre, edad)`.

```python
# Clase padre
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad
    
    def presentarse(self):
        return f"Soy {self.nombre}, tengo {self.edad} años"

# Clase hija que hereda de Persona
class Estudiante(Persona):
    def __init__(self, nombre, edad, carrera):
        # Llamar al constructor del padre con super()
        super().__init__(nombre, edad)
        # Añadir atributos propios
        self.carrera = carrera
    
    # Sobrescribir (override) método del padre
    def presentarse(self):
        # Reutilizar el método del padre con super()
        base = super().presentarse()
        return f"{base} y estudio {self.carrera}"
    
    # Método exclusivo de Estudiante
    def estudiar(self):
        return f"{self.nombre} está estudiando {self.carrera}"

# Usar herencia
estudiante = Estudiante("Ana", 20, "Ingeniería en Software")
print(estudiante.presentarse())  # Usa el método sobrescrito
print(estudiante.estudiar())     # Método propio de Estudiante

# Herencia múltiple
class Trabajador:
    def __init__(self, empresa):
        self.empresa = empresa
    
    def trabajar(self):
        return f"Trabajando en {self.empresa}"

class EstudianteTrabajador(Estudiante, Trabajador):
    def __init__(self, nombre, edad, carrera, empresa):
        # Inicializar ambas clases padre
        Estudiante.__init__(self, nombre, edad, carrera)
        Trabajador.__init__(self, empresa)
    
    def describirse(self):
        return f"{self.nombre} estudia {self.carrera} y trabaja en {self.empresa}"

est_trab = EstudianteTrabajador("Carlos", 25, "Sistemas", "TechCorp")
print(est_trab.describirse())
print(est_trab.estudiar())    # De Estudiante
print(est_trab.trabajar())    # De Trabajador
```

---

## Tema 2: Polimorfismo y Encapsulamiento

### 1. Polimorfismo y *Duck Typing*
El polimorfismo permite que diferentes objetos respondan a una misma interfaz o llamada de método de manera distinta.
* **Duck Typing:** En Python rige el principio *"Si camina como pato y suena como pato, entonces es un pato"*. 

No es necesario que los objetos hereden de la misma clase madre para ser tratados igual; basta con que implementen el método esperado (ej. un método `sonido()` presente tanto en un `Felino` como en un `Pato`). Esto simplifica enormemente la creación de código genérico.

```python
# Polimorfismo: diferentes clases, misma interfaz
class Perro:
    def sonido(self):
        return "Guau guau"
    
    def moverse(self):
        return "El perro corre"

class Gato:
    def sonido(self):
        return "Miau miau"
    
    def moverse(self):
        return "El gato camina sigilosamente"

class Pato:
    def sonido(self):
        return "Cuac cuac"
    
    def moverse(self):
        return "El pato nada"

# Función genérica que funciona con cualquier animal
def hacer_sonar_animal(animal):
    # No importa qué tipo de animal sea
    # Solo importa que tenga el método sonido()
    print(animal.sonido())
    print(animal.moverse())

# Duck Typing en acción
animales = [Perro(), Gato(), Pato()]

for animal in animales:
    hacer_sonar_animal(animal)
    print("---")

# Salida:
# Guau guau
# El perro corre
# ---
# Miau miau
# El gato camina sigilosamente
# ---
# Cuac cuac
# El pato nada
# ---

# Ejemplo práctico: procesar diferentes fuentes de datos
class ArchivoCSV:
    def leer(self):
        return ["dato1", "dato2", "dato3"]

class BaseDeDatos:
    def leer(self):
        return ["registro1", "registro2"]

class API:
    def leer(self):
        return [{"id": 1}, {"id": 2}]

def procesar_datos(fuente):
    # Duck typing: no importa el tipo, solo que tenga leer()
    datos = fuente.leer()
    print(f"Procesando {len(datos)} elementos")
    return datos

procesar_datos(ArchivoCSV())     # Funciona
procesar_datos(BaseDeDatos())    # Funciona
procesar_datos(API())            # Funciona
```

### 2. Encapsulamiento
Protege el estado interno de un objeto para evitar modificaciones accidentales desde el exterior.
* **Atributos privados:** En Python, el encapsulamiento se maneja por convención. Prefijar un atributo con doble guion bajo `__` activa el *name mangling*, dificultando su acceso directo desde afuera de la clase. Un solo guion bajo `_` indica que el atributo es de "uso interno".
* **Decorador `@property`:** Convierte un método para que pueda ser accedido como si fuera un atributo público (sin usar paréntesis `()`). Se combina con `@nombre.setter` para agregar lógica de validación antes de permitir que una variable externa modifique el dato interno.
```python
# Encapsulamiento con convenciones
class CuentaBancaria:
    def __init__(self, titular, saldo_inicial):
        self.titular = titular              # Público
        self._saldo = saldo_inicial         # Protegido (convención)
        self.__pin = "1234"                 # Privado (name mangling)
    
    def depositar(self, cantidad):
        if cantidad > 0:
            self._saldo += cantidad
            return f"Depositado: ${cantidad}. Saldo: ${self._saldo}"
        return "Cantidad inválida"
    
    def retirar(self, cantidad, pin):
        # Validación de seguridad
        if pin != self.__pin:
            return "PIN incorrecto"
        if cantidad > self._saldo:
            return "Saldo insuficiente"
        self._saldo -= cantidad
        return f"Retirado: ${cantidad}. Saldo: ${self._saldo}"
    
    def consultar_saldo(self):
        return f"Saldo actual: ${self._saldo}"

cuenta = CuentaBancaria("Ana", 1000)
print(cuenta.depositar(500))         # "Depositado: $500. Saldo: $1500"
print(cuenta.retirar(200, "1234"))   # "Retirado: $200. Saldo: $1300"
print(cuenta.retirar(100, "0000"))   # "PIN incorrecto"

# Intentar acceso directo
print(cuenta._saldo)      # 1300 (accesible pero no recomendado)
# print(cuenta.__pin)     # Error: AttributeError
print(cuenta._CuentaBancaria__pin)  # "1234" (name mangling, no recomendado)

# Decorador @property para getters y setters
class Persona:
    def __init__(self, nombre, edad):
        self._nombre = nombre
        self._edad = edad
    
    # Getter: acceso como atributo
    @property
    def edad(self):
        return self._edad
    
    # Setter: validación al asignar
    @edad.setter
    def edad(self, valor):
        if valor < 0:
            raise ValueError("La edad no puede ser negativa")
        if valor > 150:
            raise ValueError("Edad inválida")
        self._edad = valor
    
    @property
    def nombre(self):
        return self._nombre.title()  # Siempre con mayúscula inicial
    
    # Propiedad calculada (sin setter)
    @property
    def es_mayor_edad(self):
        return self._edad >= 18

persona = Persona("ana garcía", 25)

# Acceso como atributo (sin paréntesis)
print(persona.nombre)          # "Ana García"
print(persona.edad)            # 25
print(persona.es_mayor_edad)   # True

# Modificación con validación
persona.edad = 30              # OK
print(persona.edad)            # 30

try:
    persona.edad = -5          # Error: ValueError
except ValueError as e:
    print(f"Error: {e}")

# Ejemplo práctico: temperatura con validación
class Temperatura:
    def __init__(self):
        self._celsius = 0
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, valor):
        if valor < -273.15:  # Cero absoluto
            raise ValueError("Temperatura bajo cero absoluto")
        self._celsius = valor
    
    @property
    def fahrenheit(self):
        return (self._celsius * 9/5) + 32
    
    @fahrenheit.setter
    def fahrenheit(self, valor):
        self.celsius = (valor - 32) * 5/9

temp = Temperatura()
temp.celsius = 25
print(f"{temp.celsius}°C = {temp.fahrenheit}°F")  # "25°C = 77.0°F"

temp.fahrenheit = 100
print(f"{temp.celsius}°C = {temp.fahrenheit}°F")  # "37.78°C = 100°F"
```
---

## Tema 3: Creación de Scripts Automatizados

Python brilla en la automatización de tareas administrativas del sistema operativo. Para esto, utilizamos módulos de la biblioteca estándar que no requieren instalación previa:

* **Módulo `os`:** Permite interactuar con el sistema operativo subyacente. 
  * `os.path.exists()`: Verifica si una ruta o archivo es válido.
  * `os.listdir()`: Devuelve una lista con todos los elementos de un directorio.
  * `os.path.splitext()`: Separa de forma segura el nombre de un archivo de su extensión, ideal para categorizar datos.
* **Módulo `shutil`:** Ofrece operaciones de alto nivel sobre archivos y colecciones de archivos.
  * `shutil.move(origen, destino)`: Traslada archivos físicamente entre directorios, fundamental para crear *pipelines* de organización de descargas o datos crudos.

```python
import os
import shutil
from pathlib import Path

# ========== Módulo os: Operaciones básicas ==========

# Obtener directorio actual
print(os.getcwd())  # C:\Users\...

# Cambiar directorio
# os.chdir("C:\\datos")

# Listar archivos en un directorio
archivos = os.listdir(".")
print(archivos)  # ['archivo1.txt', 'carpeta1', ...]

# Verificar si existe
if os.path.exists("datos.txt"):
    print("El archivo existe")
else:
    print("No existe")

# Verificar tipo
ruta = "ejemplo.txt"
if os.path.isfile(ruta):
    print("Es un archivo")
elif os.path.isdir(ruta):
    print("Es un directorio")

# Separar nombre y extensión
nombre, extension = os.path.splitext("documento.pdf")
print(nombre)      # "documento"
print(extension)   # ".pdf"

# Construir rutas de forma segura
ruta_archivo = os.path.join("datos", "procesados", "reporte.csv")
print(ruta_archivo)  # "datos\\procesados\\reporte.csv" (Windows)
                     # "datos/procesados/reporte.csv" (Linux/Mac)

# Crear directorios
os.makedirs("datos/procesados", exist_ok=True)  # exist_ok evita error si existe

# Obtener información del archivo
if os.path.exists("ejemplo.txt"):
    tamano = os.path.getsize("ejemplo.txt")  # Tamaño en bytes
    print(f"Tamaño: {tamano} bytes")

# ========== Módulo shutil: Operaciones avanzadas ==========

# Copiar archivos
shutil.copy("origen.txt", "destino.txt")              # Copia archivo
shutil.copy("archivo.txt", "carpeta_destino/")        # Copia a carpeta
shutil.copytree("carpeta_origen", "carpeta_destino")  # Copia directorio completo

# Mover archivos
shutil.move("archivo.txt", "nueva_carpeta/archivo.txt")

# Renombrar (usando os)
os.rename("viejo_nombre.txt", "nuevo_nombre.txt")

# Eliminar archivos y directorios
os.remove("archivo.txt")          # Eliminar archivo
os.rmdir("carpeta_vacia")         # Eliminar directorio vacío
shutil.rmtree("carpeta_con_contenido")  # Eliminar directorio y todo su contenido

# ========== Script Práctico: Organizar Descargas ==========

def organizar_archivos(directorio):
    """
    Organiza archivos en carpetas según su extensión
    """
    # Categorizar extensiones
    categorias = {
        "Imagenes": [".jpg", ".jpeg", ".png", ".gif", ".bmp"],
        "Documentos": [".pdf", ".docx", ".txt", ".xlsx"],
        "Videos": [".mp4", ".avi", ".mkv", ".mov"],
        "Audio": [".mp3", ".wav", ".flac"],
        "Comprimidos": [".zip", ".rar", ".7z"],
        "Codigo": [".py", ".js", ".html", ".css", ".java"]
    }
    
    # Obtener lista de archivos
    archivos = [f for f in os.listdir(directorio) if os.path.isfile(os.path.join(directorio, f))]
    
    for archivo in archivos:
        # Obtener extensión
        _, extension = os.path.splitext(archivo)
        extension = extension.lower()
        
        # Buscar categoría
        for categoria, extensiones in categorias.items():
            if extension in extensiones:
                # Crear carpeta si no existe
                carpeta_destino = os.path.join(directorio, categoria)
                os.makedirs(carpeta_destino, exist_ok=True)
                
                # Mover archivo
                origen = os.path.join(directorio, archivo)
                destino = os.path.join(carpeta_destino, archivo)
                
                try:
                    shutil.move(origen, destino)
                    print(f"Movido: {archivo} -> {categoria}/")
                except Exception as e:
                    print(f"Error moviendo {archivo}: {e}")
                break

# Uso
# organizar_archivos("C:\\Users\\TuUsuario\\Downloads")

# ========== Script: Respaldo Automático ==========

import datetime

def crear_respaldo(carpeta_origen, carpeta_respaldos):
    """
    Crea una copia de respaldo con fecha y hora
    """
    # Crear nombre con timestamp
    timestamp = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
    nombre_respaldo = f"respaldo_{timestamp}"
    ruta_respaldo = os.path.join(carpeta_respaldos, nombre_respaldo)
    
    try:
        # Copiar todo el directorio
        shutil.copytree(carpeta_origen, ruta_respaldo)
        print(f"Respaldo creado: {ruta_respaldo}")
        return True
    except Exception as e:
        print(f"Error al crear respaldo: {e}")
        return False

# Uso
# crear_respaldo("C:\\proyectos\\mi_app", "C:\\respaldos")

# ========== Usando pathlib (alternativa moderna) ==========

from pathlib import Path

# Crear rutas de forma elegante
ruta = Path("datos") / "procesados" / "reporte.csv"
print(ruta)  # datos\procesados\reporte.csv

# Verificar existencia
if ruta.exists():
    print("Existe")

# Listar archivos con patrón
for archivo in Path(".").glob("*.py"):
    print(archivo.name)

# Leer/escribir archivos
ruta_texto = Path("ejemplo.txt")
ruta_texto.write_text("¡Hola desde pathlib!")
contenido = ruta_texto.read_text()
print(contenido)
```

### Mejores Prácticas para Scripts

```python
# ✅ Bueno: Verificar antes de operar
if os.path.exists(archivo):
    os.remove(archivo)
else:
    print(f"Archivo no encontrado: {archivo}")

# ✅ Bueno: Usar try-except para operaciones de archivos
try:
    shutil.move(origen, destino)
except FileNotFoundError:
    print("Archivo no encontrado")
except PermissionError:
    print("Sin permisos para mover el archivo")

# ✅ Bueno: Usar rutas absolutas en producción
ruta_absoluta = os.path.abspath("archivo.txt")

# ❌ Malo: No verificar existencia antes de eliminar
# os.remove("archivo.txt")  # Puede causar error

# ❌ Malo: Hardcodear separadores de ruta
# ruta = "datos\\archivo.txt"  # Solo funciona en Windows
# Usar: os.path.join("datos", "archivo.txt") o Path()
```

---

*Documento actualizado con ejemplos completos de POO, herencia, polimorfismo, encapsulamiento y automatización de scripts. Todos los conceptos ahora incluyen código ejecutable y casos de uso reales.*