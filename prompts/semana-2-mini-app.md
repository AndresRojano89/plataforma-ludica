# Mini-aplicación de práctica: Generador de contraseñas

## Versión A

**Objetivo:** construir la mini-aplicación con un prompt de una línea.

**Herramienta y modelo:** Copilot con el modelo [Copilot Fusion].

**Prompt:**

```
Haz una app web que genere contraseñas con FastAPI.
```

**Resultado:** el agente creó main.py en la raíz, sin carpeta app, con la ruta POST /api/generate, campos en inglés, longitud por defecto 20 y un grupo de símbolos distinto al pedido. La aplicación arranca y cumple 3 de 5 requisitos. Pruebas de aceptación aprobadas: 0 de 7 (ModuleNotFoundError: No module named 'app'). Errores de Ruff: 1.

## Versión B

**Objetivo:** construir la misma aplicación con un prompt estructurado, AGENTS.md y pruebas de aceptación.

**Herramienta y modelo:** Copilot con el modelo [Copilot Fusion].

**Prompt:**

```
## Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

## Objetivo
Construir la mini-aplicación web Generador de contraseñas con estos requisitos:
1. GET / muestra un formulario para elegir la longitud y si se incluyen números y símbolos, un botón para generar y un botón para copiar la contraseña.
2. GET /api/contrasena recibe los parámetros longitud, numeros y simbolos, y devuelve {"contrasena": texto, "longitud": número}. Valores por defecto: longitud 12, numeros true y simbolos false.
3. La contraseña siempre incluye letras minúsculas y mayúsculas. Si numeros es true, incluye al menos un número; si es false, no incluye ninguno. Si simbolos es true, incluye al menos un símbolo de este grupo: !@#$%&*?-_ ; si es false, no incluye ninguno.
4. La longitud debe estar entre 8 y 64; fuera de ese rango responde con el código 422.
5. La contraseña se genera con el módulo secrets de Python, no con random.

## Contexto
Lee AGENTS.md. El contrato de la API está en tests/test_aceptacion.py: las rutas, los nombres de los campos y los códigos de estado deben coincidir con esas pruebas.

## Restricciones
- Usa solo las dependencias de requirements.txt.
- Define las rutas en app/main.py y la lógica en app/servicios.py, sin importar FastAPI en servicios.
- Guarda los datos en memoria, sin base de datos ni archivos.
- No modifiques tests/test_aceptacion.py.
- La página usa HTML, CSS y JavaScript sin librerías externas.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a crear y espera mi aprobación. Al terminar, resume en una línea qué hace cada archivo.

## Ejemplo
GET /api/contrasena?longitud=16&numeros=true&simbolos=true devuelve:
{"contrasena": "q7G!mR2-xW9a#Lp4", "longitud": 16}

## Criterio de éxito
python -m pytest -v pasa todas las pruebas y ruff check . no reporta errores. Si después de 3 intentos las pruebas no pasan, detente y explica el problema.
```

**Resultado:** el agente propuso un plan con app/__init__.py, app/main.py, app/servicios.py y app/templates/index.html, y lo construyó en un solo intento (2 mensajes). Cumple 5 de 5 requisitos. Pruebas de aceptación aprobadas: 7 de 7. Errores de Ruff: 0. No modificó tests/test_aceptacion.py.

## Mejora

**Objetivo:** agregar el campo fuerza (débil, media o fuerte) a GET /api/contrasena y mostrarlo con color en la página.

**Herramienta y modelo:** Copilot con el modelo [Copilot Fusion].

**Prompt:**

```
## Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

## Objetivo
Agregar el campo fuerza a la respuesta de GET /api/contrasena. Su valor es:
- "fuerte" si la longitud es 16 o más e incluye números y símbolos;
- "débil" si la longitud es menor que 12 o no incluye números ni símbolos;
- "media" en los demás casos.
La página principal muestra la fuerza con un color: rojo para débil, amarillo para media y verde para fuerte.

## Contexto
Lee AGENTS.md, app/main.py, app/servicios.py, app/templates/index.html y tests/test_aceptacion.py.

## Restricciones
- No modifiques tests/test_aceptacion.py.
- Crea una prueba nueva en tests/test_mejora.py que compruebe el valor del campo fuerza en los tres casos, no solo el código de estado.
- Calcula la fuerza en app/servicios.py, sin importar FastAPI allí; la ruta sigue en app/main.py.
- Usa solo las dependencias de requirements.txt.
- La página usa HTML, CSS y JavaScript sin librerías externas.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a modificar o crear y espera mi aprobación. Al terminar, resume en una línea qué cambió en cada archivo.

## Ejemplo
GET /api/contrasena?longitud=16&numeros=true&simbolos=true devuelve:
{"contrasena": "q7G!mR2-xW9a#Lp4", "longitud": 16, "fuerza": "fuerte"}
GET /api/contrasena?longitud=8&numeros=false&simbolos=false devuelve "fuerza": "débil".
GET /api/contrasena (12, con números, sin símbolos) devuelve "fuerza": "media".

## Criterio de éxito
python -m pytest -v pasa todas las pruebas (tests/test_aceptacion.py y tests/test_mejora.py) y ruff check . no reporta errores. Si después de 3 intentos no se cumple, detente y explica el problema.
```

**Resultado:** el agente modificó app/main.py, app/servicios.py y app/templates/index.html, y creó tests/test_mejora.py con 3 pruebas que comprueban el valor de fuerza. Pasan las 10 pruebas y Ruff no reporta errores. No hubo que corregir nada.

## Comparación

| Criterio | Versión A | Versión B |
| --- | --- | --- |
| Pruebas de aceptación aprobadas | 0 de 7 | 7 de 7 |
| Requisitos cumplidos | 3 de 5 | 5 de 5 |
| Errores de Ruff | 1 | 0 |

**Conclusión:**

La parte del prompt B que más ayudó fue la descripción detallada de las funcionalidades y los módulos, porque le permitió al agente entender mejor lo que necesitaba el proyecto y desarrollar una solución más completa y organizada.

En la versión A el agente decidió hacer una aplicación más general y con algunas funcionalidades poco definidas, y por eso el resultado no se ajustaba completamente a las necesidades del usuario.

La próxima vez yo definiría mejor los requerimientos, explicaría el objetivo del proyecto y organizaría las funcionalidades antes de pedirle algo al agente.
