# Política de uso de IA

Me comprometo a cumplir las siguientes reglas durante el desarrollo de este proyecto:

1. Uso solo las herramientas de IA del curso. Leo las skills y los servidores MCP de terceros antes de instalarlos.
2. No comparto con la IA datos personales, contraseñas ni claves.
3. Declaro en cada entrega el uso relevante de IA y guardo los prompts en `/prompts`.
4. Respondo por todo lo que entrego, lo haya escrito yo o la IA.
5. No guardo secretos en el repositorio: el archivo `.env` está en `.gitignore`.
6. Defino qué comandos puede ejecutar el agente sin pedirme confirmación:

| Comandos que el agente puede ejecutar sin confirmación | Comandos que requieren mi confirmación |
| --- | --- |
| `python -m pytest`, `pytest` | Crear, editar o borrar archivos |
| `ruff check .` | `pip install` y cualquier instalación de dependencias |
| `git status`, `git diff`, `git log` (solo lectura) | Cualquier otro comando de la terminal |
| | `git commit` y `git push`: nunca los ejecuta el agente, los hago yo |

## Aceptación

Leí esta política y la acepto. Respondo por todo lo que entrego.

**Nombre:** Andrés David Rojano Celin

**Fecha:** 2026-11-22
