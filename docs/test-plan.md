# Plan de pruebas: SauceDemo

## 1. Objetivo
Verificar que las funcionalidades principales de SauceDemo (https://www.saucedemo.com)
funcionan correctamente: iniciar sesión, ver productos, usar el carrito y completar una compra.

## 2. Alcance (qué se prueba)
- Login (credenciales válidas, inválidas y usuario bloqueado)
- Inventario (lista de productos, ordenar, agregar al carrito)
- Carrito (ver y quitar productos)
- Checkout (datos del comprador, resumen y confirmación)
- Menú (cerrar sesión)

## 3. Fuera de alcance (qué no se prueba)
- Pruebas de rendimiento y de seguridad
- Pruebas automatizadas
- Compatibilidad con múltiples navegadores y dispositivos

## 4. Estrategia
- Pruebas manuales funcionales, empezando por lo más importante: login y checkout.
- Los casos de prueba se documentan en `test-cases/` y los defectos en `bug-reports/`.
- La evidencia (capturas) se guarda en `evidence/`.
- El seguimiento del trabajo se hace en un tablero Kanban en Jira.

## 5. Ambiente
- Aplicación: https://www.saucedemo.com
- Navegador: Google Chrome (última versión)
- Sistema operativo: Windows

## 6. Usuarios de prueba
| Usuario | Qué observé |
|---|---|
| standard_user | Funciona con normalidad |
| locked_out_user | No permite iniciar sesión: muestra un mensaje indicando que el usuario está bloqueado. Con credenciales inventadas muestra un mensaje de error distinto |
| problem_user | Falla en varias áreas: todas las imágenes de productos muestran la misma foto incorrecta, el ordenamiento no cambia la lista, solo permite agregar 3 productos desde la lista y no deja quitarlos, el contador del carrito no coincide con su contenido, un producto muestra "Item not found", y en checkout el campo Last Name modifica el campo First Name e impide continuar |
| performance_glitch_user | Funciona, pero con lentitud: el login tarda cerca de 6 segundos y varias pantallas cargan con demora (por ejemplo, al volver a la lista desde un producto o al cambiar el orden). La compra se completa |
| error_user | Funciona parcialmente: solo permite agregar 3 de los 6 productos (mochila, luz de bici y ropa de bebé), tanto desde la lista como desde el detalle, y solo permite quitarlos desde el carrito. Las 4 opciones de ordenamiento fallan y muestran el mensaje "Sorting is broken!". En checkout el campo Last Name no muestra lo que se escribe y no valida que esté vacío (deja continuar), y el botón Finish no permite completar la compra. El contador del carrito funciona correctamente |
| visual_user | Funciona, pero tiene defectos visuales: imagen incorrecta en el primer producto, precios distintos a los de standard_user en los 6 productos, nombres de productos y botón "Add to cart" desalineados, y los botones del carrito y de checkout en una posición distinta a la esperada |