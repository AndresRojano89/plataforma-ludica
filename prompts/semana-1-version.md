## Objetivo
Agregar el endpoint GET /api/version con su prueba.

## Herramienta y modelo
Copilot, modelo Auto.

## Prompt
Lee AGENTS.md. Agrega el endpoint GET /api/version, que devuelva la versión definida en app/proyecto.py, con su prueba en tests/test_inicio.py. Antes de escribir código, explícame qué archivos vas a modificar y espera mi aprobación.

## Resultado
El agente modificó los dos archivos del plan: agregó GET /api/version en app/rutas/api.py y una prueba en tests/test_inicio.py. Las 7 pruebas de tests/test_inicio.py pasan. Ruff no estaba instalado en .venv; se instaló y `ruff check .` pasó. No fue necesario corregir el código.
