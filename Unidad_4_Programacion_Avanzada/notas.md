# 📚 Notas Conceptuales - Unidad 4: Programación Avanzada

Este documento consolida los conceptos de optimización y conectividad web esenciales para el desarrollo de backend modernos.

---

## Tema 1: Decoradores

### ¿Qué es un Decorador?

Un decorador es una función que modifica el comportamiento de otra función sin alterar su código interno. Se aplica de forma declarativa y elegante utilizando el símbolo `@nombre_decorador` justo antes de la definición de la función objetivo.

**Concepto fundamental:** Los decoradores aprovechan que en Python las funciones son objetos de primera clase, es decir, pueden ser pasadas como argumentos, retornadas desde otras funciones y asignadas a variables.

### Anatomía de un Decorador

```python
def mi_decorador(funcion):
    def wrapper(*args, **kwargs):
        # Código ANTES de ejecutar la función
        print("Antes de ejecutar")
        resultado = funcion(*args, **kwargs)
        # Código DESPUÉS de ejecutar la función
        print("Después de ejecutar")
        return resultado
    return wrapper

@mi_decorador
def saludar(nombre):
    return f"Hola, {nombre}"

# Equivale a: saludar = mi_decorador(saludar)
```

### Conceptos Clave

* **Función Envoltura (Wrapper):** El decorador envuelve a la función original, permitiendo ejecutar código antes y después de la misma. La firma `*args, **kwargs` permite que el decorador funcione con cualquier función, sin importar sus parámetros.

* **Decoradores Comunes Integrados:** Python ofrece varios por defecto:
  - `@staticmethod`: Método estático sin acceso a `self` ni `cls`
  - `@classmethod`: Recibe la clase `cls` como primer argumento
  - `@property`: Convierte un método en atributo de solo lectura
  - `@lru_cache` (de `functools`): Memoriza resultados de funciones

* **Buenas Prácticas - `functools.wraps`:** Al crear decoradores personalizados, es altamente recomendado importar `wraps` del módulo `functools`. Usar `@wraps(func)` dentro del decorador asegura que la función decorada no pierda sus metadatos originales (como `__name__`, `__doc__`, etc.).

```python
from functools import wraps

def timer(func):
    @wraps(func)  # Preserva el nombre y docstring de func
    def wrapper(*args, **kwargs):
        import time
        inicio = time.time()
        resultado = func(*args, **kwargs)
        fin = time.time()
        print(f"{func.__name__} tardó {fin - inicio:.4f} segundos")
        return resultado
    return wrapper

@timer
def calcular_fibonacci(n):
    """Calcula el n-ésimo número de Fibonacci"""
    if n <= 1:
        return n
    return calcular_fibonacci(n-1) + calcular_fibonacci(n-2)
```

### Decoradores con Argumentos

Para crear decoradores que acepten parámetros, necesitamos un nivel adicional de anidamiento:

```python
def repetir(veces):
    def decorador(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(veces):
                resultado = func(*args, **kwargs)
            return resultado
        return wrapper
    return decorador

@repetir(3)
def decir_hola():
    print("¡Hola!")

# Ejecutará print 3 veces
decir_hola()
```

### Casos de Uso Reales

1. **Logging:** Registrar automáticamente cuándo y con qué parámetros se llama una función
2. **Autenticación:** Verificar permisos antes de ejecutar funciones sensibles (`@login_required`)
3. **Validación:** Verificar tipos de datos de los argumentos
4. **Caché/Memoization:** Guardar resultados de funciones costosas
5. **Manejo de errores:** Reintentar una función si falla (`@retry`)

---

## Tema 2: Generadores

### ¿Qué es un Generador?

Los generadores son funciones especializadas que producen una secuencia de valores "sobre la marcha" utilizando la palabra clave `yield` en lugar de `return`. Son una implementación elegante del patrón Iterator en Python.

**Ventaja principal:** Generan valores uno a la vez, consumiendo memoria mínima sin importar el tamaño de la secuencia.

### Anatomía de un Generador

```python
def contador(limite):
    """Generador simple que cuenta hasta un límite"""
    n = 0
    while n < limite:
        yield n  # Pausa aquí y devuelve n
        n += 1   # Se reanuda desde aquí en el próximo next()

# Uso
gen = contador(5)
print(next(gen))  # 0
print(next(gen))  # 1
print(next(gen))  # 2

# O en un bucle
for numero in contador(3):
    print(numero)  # 0, 1, 2
```

### Diferencias Clave

#### **`yield` vs `return`**

| Característica | `return` | `yield` |
|----------------|----------|---------|
| **Termina la función** | Sí, inmediatamente | No, pausa temporalmente |
| **Estado de variables** | Se pierde | Se preserva |
| **Valores devueltos** | Uno solo | Secuencia de valores |
| **Llamadas sucesivas** | Re-ejecuta desde inicio | Resume desde el último `yield` |

```python
# Función normal con return
def lista_cuadrados(n):
    resultado = []
    for i in range(n):
        resultado.append(i ** 2)
    return resultado  # Devuelve TODA la lista de una vez

# Generador con yield
def generar_cuadrados(n):
    for i in range(n):
        yield i ** 2  # Devuelve UN valor a la vez

# Comparación
lista = lista_cuadrados(1000000)     # Carga 1 millón de números en RAM
generador = generar_cuadrados(1000000)  # Solo guarda el estado actual
```

#### **Eficiencia de Memoria**

A diferencia de una lista convencional que carga todos sus elementos en la memoria RAM simultáneamente, un generador es **lazy** (perezoso) y procesa un elemento a la vez, haciéndolo ideal para:
- **Big data:** Procesar archivos de varios GB línea por línea
- **Secuencias infinitas:** Números primos, Fibonacci sin límite
- **Pipelines de datos:** ETL (Extract, Transform, Load)

```python
import sys

# Lista: Consume mucha memoria
lista = [x**2 for x in range(1000000)]
print(sys.getsizeof(lista))  # ~8 MB

# Generador: Consume memoria mínima
generador = (x**2 for x in range(1000000))
print(sys.getsizeof(generador))  # ~128 bytes
```

### Métodos Útiles de Generadores

* **`next(generador)`:** Obtiene el siguiente valor. Lanza `StopIteration` cuando se agota.
* **`generador.send(valor)`:** Envía un valor AL generador (comunicación bidireccional)
* **`generador.close()`:** Detiene el generador anticipadamente
* **`generador.throw(exception)`:** Lanza una excepción dentro del generador

```python
def receptor():
    print("Listo para recibir")
    while True:
        valor = yield  # Espera recibir un valor
        print(f"Recibí: {valor}")

gen = receptor()
next(gen)  # Arranca el generador hasta el primer yield
gen.send(10)   # Recibí: 10
gen.send(20)   # Recibí: 20
gen.close()
```

### Expresiones Generadoras

Similar a list comprehensions pero con paréntesis `()` en lugar de corchetes `[]`:

```python
# List comprehension: crea lista completa en memoria
cuadrados_lista = [x**2 for x in range(1000000)]

# Expresión generadora: evalúa bajo demanda
cuadrados_gen = (x**2 for x in range(1000000))

# Uso en funciones
suma_total = sum(x**2 for x in range(1000000))  # Eficiente
```

### Casos de Uso Reales

1. **Lectura de archivos grandes:**
```python
def leer_lineas(archivo):
    with open(archivo, 'r') as f:
        for linea in f:  # Generador implícito
            yield linea.strip()
```

2. **Secuencia de Fibonacci infinita:**
```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b
```

3. **Pipeline de procesamiento:**
```python
def leer_datos(archivo):
    for linea in open(archivo):
        yield linea

def parsear(lineas):
    for linea in lineas:
        yield linea.split(',')

def filtrar(filas):
    for fila in filas:
        if int(fila[2]) > 100:
            yield fila

# Encadenar generadores
datos = leer_datos('data.csv')
parseado = parsear(datos)
filtrado = filtrar(parseado)
```

---

## Tema 3: Obtener y Enviar Datos a una API

### ¿Qué es una API?

Una API (Application Programming Interface - Interfaz de Programación de Aplicaciones) es el puente que permite la comunicación entre diferentes aplicaciones de software. En el contexto web, las **APIs REST** son el estándar para que aplicaciones intercambien datos mediante el protocolo HTTP.

**Analogía:** Una API es como el menú de un restaurante. El menú te dice qué puedes pedir (endpoints disponibles), qué información necesitas dar (parámetros), y qué recibirás a cambio (respuesta).

### La Librería `requests`

Para conectar Python con la web, el estándar de la industria es utilizar el módulo externo `requests`. Se instala con:

```bash
pip install requests
```

**Ventajas sobre urllib (librería nativa):**
- Sintaxis más simple y Pythónica
- Manejo automático de JSON
- Sesiones persistentes
- Manejo de SSL/TLS integrado

### Operaciones HTTP Fundamentales

#### 1. **Peticiones GET - Consultar Datos**

Se utilizan para consultar y obtener datos de un servidor externo. Son idempotentes (puedes llamarlas múltiples veces sin efectos secundarios).

```python
import requests

# GET simple
respuesta = requests.get('https://api.github.com/users/octocat')

# Verificar que fue exitosa
if respuesta.status_code == 200:
    datos = respuesta.json()  # Convierte JSON a dict
    print(f"Usuario: {datos['name']}")
    print(f"Repos públicos: {datos['public_repos']}")
else:
    print(f"Error: {respuesta.status_code}")
```

**Con parámetros de consulta (query params):**

```python
# URL: https://api.example.com/users?edad=25&ciudad=Quito
params = {
    'edad': 25,
    'ciudad': 'Quito'
}
respuesta = requests.get('https://api.example.com/users', params=params)
```

#### 2. **Peticiones POST - Enviar Datos**

Sirven para enviar nueva información al servidor (crear recursos).

```python
# Datos a enviar
nuevo_usuario = {
    'nombre': 'Juan Pérez',
    'email': 'juan@example.com',
    'edad': 30
}

# POST enviando JSON
respuesta = requests.post(
    'https://jsonplaceholder.typicode.com/users',
    json=nuevo_usuario  # Automáticamente serializa a JSON
)

# Verificar creación exitosa
if respuesta.status_code == 201:  # 201 = Created
    usuario_creado = respuesta.json()
    print(f"Usuario creado con ID: {usuario_creado['id']}")
```

#### 3. **Otras Operaciones HTTP**

```python
# PUT: Actualizar recurso completo
requests.put('https://api.example.com/users/1', json={'nombre': 'Carlos'})

# PATCH: Actualizar parcialmente
requests.patch('https://api.example.com/users/1', json={'edad': 31})

# DELETE: Eliminar recurso
requests.delete('https://api.example.com/users/1')
```

### Códigos de Estado HTTP

Es vital verificar el `status_code` antes de procesar la respuesta:

| Código | Significado | Acción |
|--------|-------------|--------|
| **200** | OK | Petición exitosa (GET) |
| **201** | Created | Recurso creado exitosamente (POST) |
| **204** | No Content | Exitoso pero sin contenido (DELETE) |
| **400** | Bad Request | Datos inválidos enviados |
| **401** | Unauthorized | Falta autenticación |
| **403** | Forbidden | Sin permisos |
| **404** | Not Found | Recurso no existe |
| **500** | Internal Server Error | Error del servidor |

```python
respuesta = requests.get('https://api.example.com/data')

if respuesta.status_code == 200:
    datos = respuesta.json()
elif respuesta.status_code == 404:
    print("Recurso no encontrado")
elif respuesta.status_code == 500:
    print("Error del servidor")
else:
    print(f"Error inesperado: {respuesta.status_code}")
```

### Manejo de JSON

El método `.json()` convierte automáticamente la respuesta desde texto JSON a estructuras Python:

```python
respuesta = requests.get('https://jsonplaceholder.typicode.com/todos/1')
datos = respuesta.json()

# JSON → Diccionario Python
print(type(datos))  # <class 'dict'>
print(datos['title'])
print(datos['completed'])
```

### Headers y Autenticación

#### **Headers Personalizados**

```python
headers = {
    'User-Agent': 'MiApp/1.0',
    'Accept': 'application/json',
    'Content-Type': 'application/json'
}

respuesta = requests.get('https://api.example.com/data', headers=headers)
```

#### **Autenticación Básica**

```python
from requests.auth import HTTPBasicAuth

respuesta = requests.get(
    'https://api.example.com/secure',
    auth=HTTPBasicAuth('usuario', 'contraseña')
)
```

#### **API Keys y Tokens**

```python
# API Key en headers (común en APIs modernas)
headers = {
    'Authorization': 'Bearer mi_token_secreto_123'
}

respuesta = requests.get(
    'https://api.example.com/data',
    headers=headers
)

# API Key en parámetros
params = {'api_key': 'mi_clave_api'}
respuesta = requests.get('https://api.example.com/data', params=params)
```

### Manejo de Errores y Timeouts

```python
try:
    respuesta = requests.get(
        'https://api.example.com/data',
        timeout=5  # Timeout de 5 segundos
    )
    respuesta.raise_for_status()  # Lanza excepción si status >= 400
    datos = respuesta.json()
    
except requests.exceptions.Timeout:
    print("La petición tardó demasiado")
except requests.exceptions.ConnectionError:
    print("Error de conexión")
except requests.exceptions.HTTPError as e:
    print(f"Error HTTP: {e}")
except requests.exceptions.RequestException as e:
    print(f"Error general: {e}")
```

### Sesiones y Persistencia

Para múltiples peticiones al mismo servidor, usa sesiones para reutilizar conexiones:

```python
with requests.Session() as session:
    # Headers comunes para todas las peticiones
    session.headers.update({'Authorization': 'Bearer token123'})
    
    # Primera petición
    usuarios = session.get('https://api.example.com/users').json()
    
    # Segunda petición (reutiliza conexión)
    posts = session.get('https://api.example.com/posts').json()
```

### Ejemplo Completo: Cliente de API

```python
import requests

class APIClient:
    def __init__(self, base_url, api_key):
        self.base_url = base_url
        self.session = requests.Session()
        self.session.headers.update({
            'Authorization': f'Bearer {api_key}',
            'Content-Type': 'application/json'
        })
    
    def obtener_usuarios(self):
        """GET: Obtener lista de usuarios"""
        url = f"{self.base_url}/users"
        respuesta = self.session.get(url)
        respuesta.raise_for_status()
        return respuesta.json()
    
    def crear_usuario(self, datos):
        """POST: Crear nuevo usuario"""
        url = f"{self.base_url}/users"
        respuesta = self.session.post(url, json=datos)
        if respuesta.status_code == 201:
            return respuesta.json()
        else:
            raise Exception(f"Error: {respuesta.status_code}")
    
    def __del__(self):
        self.session.close()

# Uso
cliente = APIClient('https://api.example.com', 'mi_token_123')
usuarios = cliente.obtener_usuarios()
nuevo = cliente.crear_usuario({'nombre': 'Ana', 'email': 'ana@example.com'})
```

### Mejores Prácticas

1. **Siempre verificar `status_code`** antes de procesar datos
2. **Usar timeouts** para evitar peticiones colgadas
3. **Manejar excepciones** específicas de `requests`
4. **Nunca hardcodear** API keys en el código (usar variables de entorno)
5. **Respetar rate limits** de las APIs (límite de peticiones por minuto)
6. **Usar sesiones** para múltiples peticiones al mismo servidor
7. **Validar datos** antes de enviarlos con POST/PUT
8. **Cerrar sesiones** explícitamente o usar context managers (`with`)

---

*Documento actualizado para consolidar los conocimientos de optimización, decoradores, generadores y conectividad web. Estos conceptos son fundamentales para el desarrollo de sistemas backend modernos y escalables.*