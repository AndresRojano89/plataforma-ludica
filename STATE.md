# STATE.md

Estado del proyecto. Léalo al iniciar cada sesión de trabajo y actualícelo al cerrarla.

## Estado actual

Repositorio publicado en GitHub con el CI en verde.
El endpoint GET /api/version está implementado y devuelve proyecto.VERSION; las 7
pruebas de tests/test_inicio.py pasan. La aplicación está configurada en
https://plataforma-ludica-ort4.onrender.com; al verificar /api/version hoy,
respondió HTTP 503.

## Decisiones

| Fecha | Decisión | Motivo |
| --- | --- | --- |
| 2026-11-13 | Usar la plantilla del curso con FastAPI | Es el stack definido para el
proyecto |
| 2026-11-14 | Exponer GET /api/version usando proyecto.VERSION | Mantener una sola fuente de versión y verificar el contrato con una prueba |

## Siguiente paso

Implementar el acceso del niño con código de clase y selección de avatar, sin correo, con pruebas de aceptación.
