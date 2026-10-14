# SauceDemo QA Testing

Proyecto de pruebas manuales sobre [SauceDemo](https://www.saucedemo.com), una tienda en línea de demostración. Incluye plan de pruebas, casos de prueba, reportes de bugs con evidencia y seguimiento del trabajo en un tablero Kanban en Jira.

## Objetivo
Verificar que las funcionalidades principales de la app (login, inventario, carrito y checkout) funcionan correctamente, comparando el comportamiento de cada usuario de prueba contra `standard_user`, que se usó como línea base.

## Qué se hizo
- Exploración de la app con los 6 usuarios de prueba
- Plan de pruebas con objetivo, alcance, estrategia, ambiente y usuarios
- 17 casos de prueba manuales (positivos y negativos)
- 10 reportes de bugs, con capturas y videos como evidencia
- Tablero Kanban en Jira (To Do, In Progress, In Review, Done) con límite de trabajo en curso (WIP) de 2

## Resultados

| Usuario | Resultado |
|---|---|
| `standard_user` | Funciona correctamente (línea base) |
| `locked_out_user` | Bloqueado, como se espera |
| `problem_user` | Fallas en imágenes, carrito, ordenamiento y checkout |
| `error_user` | Fallas en carrito, ordenamiento y checkout (no permite completar la compra) |
| `visual_user` | Defectos visuales: precios en la lista, imágenes, ordenamiento y elementos desalineados |
| `performance_glitch_user` | Funciona, pero con demoras en varias pantallas |

**Bugs encontrados:** 10 en total. 4 de severidad alta, 5 media y 1 baja.

## Estructura del proyecto
- [`docs/test-plan.md`](docs/test-plan.md): plan de pruebas
- [`test-cases/test-cases.md`](test-cases/test-cases.md): casos de prueba
- [`bug-reports/bug-reports.md`](bug-reports/bug-reports.md): reportes de bugs
- [`evidence/`](evidence/): capturas y videos, organizados por usuario

## Herramientas
Jira (tablero Kanban y seguimiento), GitHub (repositorio), Google Chrome, grabación de pantalla de Windows.

## Pendiente para una próxima versión
- Mapa de funcionalidades y lista de riesgos
- Pruebas con números y caracteres especiales en los campos del checkout

## Autora
Paula, Bogotá, Colombia.