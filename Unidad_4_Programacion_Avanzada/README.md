# 🚀 Unidad 4: Programación Avanzada e Integración Web
### Decoradores, Generadores y APIs

[![Python](https://img.shields.io/badge/Python-Avanzado-red.svg)](https://www.python.org/)
[![Status](https://img.shields.io/badge/Status-Completado-success.svg)]()
[![API](https://img.shields.io/badge/API-REST-blue.svg)]()

---

## 🎯 Objetivos de Aprendizaje

Al finalizar esta unidad, serás capaz de:

- ✅ Crear decoradores personalizados para extender funcionalidades
- ✅ Aplicar decoradores integrados (`@staticmethod`, `@classmethod`, `@property`)
- ✅ Usar `functools.wraps` para preservar metadatos de funciones
- ✅ Implementar generadores con `yield` para procesamiento eficiente de datos
- ✅ Optimizar memoria usando generadores en lugar de listas
- ✅ Realizar peticiones HTTP GET para consumir APIs REST
- ✅ Enviar datos con peticiones POST en formato JSON
- ✅ Manejar respuestas de APIs y códigos de estado HTTP
- ✅ Integrar servicios web externos en aplicaciones Python
- ✅ Comprender la diferencia entre `yield` y `return`

---

## 📚 Contenido de la Unidad

### Tema 1: Decoradores

**Conceptos clave:**
- Decoradores: funciones que modifican el comportamiento de otras funciones
- Sintaxis `@decorador` para aplicación declarativa
- Funciones wrapper (envolturas)
- Decoradores con y sin argumentos
- `functools.wraps` para preservar metadatos (`__name__`, `__doc__`)
- Decoradores integrados: `@staticmethod`, `@classmethod`, `@property`
- Ejecución de código antes y después de una función
- Patrón de diseño: Decorator Pattern
- Logging, timing y validación con decoradores

**📄 Archivo de práctica:**  
[`u4_tema_1_decoradores.py`](./u4_tema_1_decoradores.py)

**Ejercicios incluidos:**
- Decorador simple que ejecuta código antes y después de una función
- Aplicación de decoradores con `@mi_decorador`
- Decorador con argumentos para repetir ejecuciones
- Uso de `functools.wraps` para preservar información de función
- Casos prácticos: logging, medición de tiempo, validación

---

### Tema 2: Generadores

**Conceptos clave:**
- Generadores: funciones que producen valores "sobre la marcha"
- Palabra clave `yield` vs `return`
- Iteradores perezosos (lazy evaluation)
- Eficiencia de memoria: procesamiento ítem por ítem
- Estado suspendido de ejecución entre `yield`s
- Función `next()` para obtener siguiente valor
- Métodos `.send()` y `.close()` de generadores
- Expresiones generadoras: `(x*2 for x in range(10))`
- Casos de uso: big data, secuencias infinitas, pipelines de datos

**📄 Archivo de práctica:**  
[`u4_tema_2_generadores.py`](./u4_tema_2_generadores.py)

**Ejercicios incluidos:**
- Creación de generador de secuencias numéricas
- Comparación memoria: lista vs generador
- Generador de números pares
- Uso de `yield` para pausar y reanudar ejecución
- Procesamiento de grandes volúmenes de datos eficientemente

---

### Tema 3: Obtener y Enviar Datos a una API

**Conceptos clave:**
- API (Application Programming Interface): puente entre aplicaciones
- API REST y arquitectura cliente-servidor
- Librería `requests`: estándar de la industria para HTTP
- **Peticiones GET**: consultar y obtener datos (`requests.get()`)
- **Peticiones POST**: enviar y crear recursos (`requests.post()`)
- Códigos de estado HTTP:
  - `200 OK`: solicitud exitosa
  - `201 Created`: recurso creado exitosamente
  - `404 Not Found`: recurso no encontrado
  - `500 Internal Server Error`: error del servidor
- Formato JSON: intercambio de datos entre sistemas
- Métodos `.json()` para parsear respuestas
- Atributo `.status_code` para verificar resultado
- Headers y autenticación en APIs

**📄 Archivo de práctica:**  
[`u4_tema_3_obtener_y_enviar_datos_a_una_api.py`](./u4_tema_3_obtener_y_enviar_datos_a_una_api.py)

**Ejercicios incluidos:**
- GET request para obtener datos de API pública
- Verificación de `status_code` para manejo de errores
- Parseo de JSON a diccionarios Python
- POST request para enviar datos nuevos
- Construcción y envío de payload JSON
- Manejo de respuestas y errores de API

---

## 📖 Notas Conceptuales Detalladas

Para una comprensión profunda de decoradores, generadores y comunicación con APIs, consulta:

### 👉 [**notas.md - Documentación Conceptual Completa**](./notas.md)

Este documento incluye:
- Fundamentos de decoradores y patrón Decorator
- Diferencias clave entre `yield` y `return`
- Optimización de memoria con generadores
- Protocolo HTTP y arquitectura REST
- Guía completa de la librería `requests`
- Mejores prácticas de integración con APIs
- Seguridad en el consumo de servicios web

---

## 🚀 Cómo Ejecutar las Prácticas

### Prerequisitos

⚠️ **Importante:** La Unidad 4 requiere la instalación de la librería `requests`.

```bash
# Instalar requests
pip install requests
```

### Desde la Terminal / CMD

```bash
# Navegar a la carpeta de la Unidad 4
cd Unidad_4_Programacion_Avanzada

# Ejecutar práctica de decoradores
python u4_tema_1_decoradores.py

# Ejecutar práctica de generadores
python u4_tema_2_generadores.py

# Ejecutar práctica de API (requiere conexión a internet)
python u4_tema_3_obtener_y_enviar_datos_a_una_api.py
```

**⚠️ Nota sobre APIs:** El script del Tema 3 realiza peticiones a servicios web externos. Asegúrate de:
- Tener conexión a internet estable
- Usar APIs públicas de prueba (como JSONPlaceholder)
- Nunca compartir API keys o tokens en el código

### Desde VS Code

1. Abre el archivo `.py` que deseas ejecutar
2. Asegúrate de tener `requests` instalado en tu entorno
3. Presiona `F5` o usa el botón ▶️ "Run Python File"
4. Observa la salida en la terminal integrada

---

## 💡 Comparación de Conceptos Clave

### Decoradores vs Herencia

| Característica | Decoradores | Herencia |
|----------------|-------------|----------|
| **Propósito** | Extender comportamiento de funciones | Extender comportamiento de clases |
| **Sintaxis** | `@decorador` | `class Hijo(Padre):` |
| **Flexibilidad** | Combinar múltiples decoradores | Una clase padre a la vez (sin multi-herencia múltiple) |
| **Uso ideal** | Logging, timing, validación | Relaciones "es-un" |

### Generadores vs Listas

| Característica | Generador | Lista |
|----------------|-----------|-------|
| **Memoria** | Eficiente (un elemento a la vez) | Carga todos los elementos |
| **Sintaxis** | `yield` | `return` o `[]` |
| **Reutilización** | Una sola pasada (se agota) | Múltiples iteraciones |
| **Caso de uso** | Big data, secuencias infinitas | Datos pequeños, acceso aleatorio |

---

## 🎓 Patrones de Diseño Aplicados

Esta unidad introduce patrones profesionales de la ingeniería de software:

| Patrón | Aplicación en esta Unidad |
|--------|---------------------------|
| **Decorator Pattern** | Decoradores para extender funcionalidades sin modificar código |
| **Iterator Pattern** | Generadores implementan el protocolo de iteración |
| **Lazy Evaluation** | Generadores calculan valores solo cuando se necesitan |
| **Client-Server** | Comunicación con APIs REST |
| **Repository Pattern** | APIs como repositorios remotos de datos |

---

## 🏗️ Casos de Uso en el Mundo Real

### Decoradores se usan en:
- 🔐 **Autenticación:** `@login_required` en frameworks web (Flask, Django)
- ⏱️ **Profiling:** Medir tiempo de ejecución de funciones críticas
- 📝 **Logging:** Registrar llamadas a funciones automáticamente
- ✅ **Validación:** Verificar tipos de parámetros antes de ejecutar
- 💾 **Caching:** `@lru_cache` para memorizar resultados costosos

### Generadores se usan en:
- 📊 **Big Data:** Procesar archivos de varios GB línea por línea
- 🔄 **Pipelines ETL:** Transformar datos sin cargar todo en memoria
- 📡 **Streaming:** Procesar datos que llegan continuamente
- 🎲 **Secuencias infinitas:** Números primos, Fibonacci, eventos
- 📁 **Lectura de archivos:** Procesar logs masivos eficientemente

### APIs REST se usan en:
- 🌐 **Microservicios:** Comunicación entre servicios backend
- 📱 **Aplicaciones móviles:** Cliente móvil → API → Base de datos
- 🤖 **Bots y automatización:** Interactuar con Twitter, Telegram, etc.
- 💳 **Pasarelas de pago:** Stripe, PayPal, Mercado Pago
- 🗺️ **Servicios externos:** Google Maps, OpenWeather, GitHub API

---

## 🔗 Recursos Adicionales

- 📘 [Python para Todos - Capítulo 13: Web Services](https://www.py4e.com/book)
- 📄 [Documentación Oficial - Decoradores](https://docs.python.org/3/glossary.html#term-decorator)
- 📄 [Documentación Oficial - Generadores](https://docs.python.org/3/howto/functional.html#generators)
- 📄 [Requests Library - Documentación](https://requests.readthedocs.io/)
- 🎯 [Real Python - Decorators](https://realpython.com/primer-on-python-decorators/)
- 🎯 [Real Python - Generators](https://realpython.com/introduction-to-python-generators/)
- 🌐 [JSONPlaceholder - API de Prueba](https://jsonplaceholder.typicode.com/)
- 📚 [HTTP Status Codes](https://developer.mozilla.org/es/docs/Web/HTTP/Status)

---

## ✅ Checklist de Dominio

Marca tu progreso:

- [ ] Puedo crear decoradores simples con funciones wrapper
- [ ] Entiendo cómo funcionan múltiples decoradores apilados
- [ ] Uso `@functools.wraps` en mis decoradores personalizados
- [ ] Sé cuándo usar `yield` en lugar de `return`
- [ ] Comprendo la ventaja de memoria de los generadores
- [ ] Puedo hacer peticiones GET a APIs REST
- [ ] Envío datos con POST y valido el `status_code`
- [ ] Parseo respuestas JSON a estructuras Python
- [ ] Manejo errores de red y respuestas de API
- [ ] Entiendo la arquitectura cliente-servidor

---

## 🧪 Desafíos Propuestos

Para reforzar tu aprendizaje:

1. **Decoradores:**
   - Crea un decorador `@timer` que mida el tiempo de ejecución de funciones
   - Implementa `@validate_types` que verifique tipos de argumentos
   - Desarrolla `@retry` que reintente una función si falla

2. **Generadores:**
   - Generador de números Fibonacci infinito
   - Procesador de archivo CSV línea por línea sin cargar todo en memoria
   - Pipeline de transformación: leer → filtrar → transformar → escribir

3. **APIs:**
   - Consumir la API de GitHub para obtener tus repositorios
   - Crear un cliente para OpenWeather API que muestre el clima
   - Implementar un sistema de caché local para respuestas de API

---

## 📌 Unidades Relacionadas

### ⬅️ Prerequisito
[**Unidad 3: POO y Automatización**](../Unidad-3-POO-Automatizacion) - Repasar funciones y clases antes de decoradores.

### ➡️ Siguiente
[**Unidad 5: Temas Especializados**](../Unidad-5-Por-Definir) *(Si aplica)* - Async/await, testing, deployment.

---

<div align="center">
  <sub>Parte del Curso de Python - UNEMI 2026</sub>
</div>