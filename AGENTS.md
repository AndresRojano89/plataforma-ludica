# AGENTS.md

Contexto del proyecto para los agentes de IA. Léalo antes de cualquier cambio.

## Proyecto

Plataforma web lúdica de cursos para niños. Curso: Inglés. Mecánica: Estrellas.
Roles: docente y niño. El niño entra con código de clase y avatar, sin correo.

## Stack

- Python 3.11+, FastAPI, SQLModel, Jinja2
- SQLite en desarrollo, PostgreSQL al publicar
- pytest con TestClient, httpx, ruff
- GitHub Actions (CI) y Render (despliegue)

## Comandos

- Instalar: `pip install -r requirements-dev.txt`
- Ejecutar: `uvicorn app.main:app --reload`
- Probar: `pytest -v`
- Estilo: `ruff check .`
- PDF entrega: `python entregar.py N` (N = número de semana)
- Pre-commit: `pre-commit install` (ejecuta ruff + pytest antes de commit)

## Estructura

- `app/proyecto.py`: datos del proyecto (APRENDIZ, CURSO, MECANICA, VERSION)
- `app/rutas/api.py`: endpoints REST (/salud, /api/proyecto)
- `app/rutas/paginas.py`: páginas HTML (/, /sw.js)
- `app/servicios/`: regla de negocio (pruebas propias)
- `app/modelos/`: tablas SQLModel
- `app/templates/`: Jinja2 HTML
- `app/static/`: archivos estáticos (manifest, sw.js, icons)
- `tests/`: pruebas unitarias; `tests/aceptacion/`: criterios Dado/Cuando/Entonces
- `prompts/`: prompts versionados por semana/tema

## Convenciones

- Nombres en español, claros y completos.
- Cambios pequeños, una tarea por rama y prueba antes del código.
- No escribir claves ni contraseñas en el código: leer de variables de entorno.
- No instalar dependencias sin verificar que existen en pypi.org.
- No modificar ni borrar pruebas para que pasen.
- No usar datos personales reales.
- Al iniciar cada sesión, leer STATE.md.

## Flujo CI (.github/workflows/ci.yml)

Se ejecuta en cada push a main y pull request:
1. `pip install -r requirements-dev.txt`
2. `ruff check .` — si falla, el build se detiene
3. `pytest -v` — si falla, el build se detiene
4. Arranca uvicorn y prueba `/salud` — asegura que la app levanta

## Entrega semanal (entregar.py)

- `python entregar.py N` genera `entregas/semana-N.pdf` a partir de `entregas/semana-N.md`
- Lee el estado de pruebas, ruff, URL desplegada y lecciones de AGENTS.md
- Requiere fpdf2 (incluido en requirements-dev.txt)
- La primera vez, correr `pre-commit install`

## PWA

- Service worker en `/sw.js` (servido desde la raíz)
- Manifiesto en `/static/manifest.json`
- Los icons deben tener tamaños 192x192 y 512x512

## Qué no hacer

- No modificar ni borrar pruebas para que pasen.
- No escribir claves ni contraseñas en el código: se leen de variables de entorno.
- No instalar dependencias sin verificar que existen en pypi.org.
- No usar datos personales reales.
- No hacer commit ni push: los hace el desarrollador.

## Lecciones aprendidas