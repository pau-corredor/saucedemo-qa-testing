# Casos de prueba: SauceDemo

**Ambiente:** https://www.saucedemo.com, Google Chrome, Windows
**Línea base:** todos los casos se ejecutaron con `standard_user`. En "Usuarios con fallas" se indica en qué usuarios el resultado es distinto.

---

### TC-01: Login con usuario válido
- **Módulo:** Login
- **Precondición:** estar en la página de login
- **Pasos:**
  1. Escribir `standard_user` en Username
  2. Escribir la contraseña que aparece en la página
  3. Hacer clic en Login
- **Resultado esperado:** permite ingresar y se muestra la página principal con los productos
- **Resultado real:** permite ingresar y se muestra la página principal con los productos
- **Estado:** Pasó
- **Usuarios con fallas:** ninguno detectado

### TC-02: Login con usuario bloqueado
- **Módulo:** Login
- **Precondición:** estar en la página de login
- **Pasos:**
  1. Escribir `locked_out_user` en Username
  2. Escribir la contraseña que aparece en la página
  3. Hacer clic en Login
- **Resultado esperado:** no permite entrar y muestra el mensaje "Epic sadface: Sorry, this user has been locked out."
- **Resultado real:** no permite entrar y muestra el mensaje "Epic sadface: Sorry, this user has been locked out."
- **Estado:** Pasó

### TC-03: Login con credenciales incorrectas
- **Módulo:** Login
- **Precondición:** estar en la página de login
- **Pasos:**
  1. Escribir un usuario que no esté en la lista de usuarios de prueba
  2. Escribir una contraseña que no sea la de la página
  3. Hacer clic en Login
- **Resultado esperado:** no permite entrar y muestra el mensaje "Epic sadface: Username and password do not match any user in this service"
- **Resultado real:** no permite entrar y muestra el mensaje "Epic sadface: Username and password do not match any user in this service"
- **Estado:** Pasó

### TC-04: Login con Username vacío
- **Módulo:** Login
- **Precondición:** estar en la página de login
- **Pasos:**
  1. Dejar Username y Password vacíos
  2. Hacer clic en Login
- **Resultado esperado:** no permite entrar y muestra el mensaje "Epic sadface: Username is required"
- **Resultado real:** no permite entrar y muestra el mensaje "Epic sadface: Username is required"
- **Estado:** Pasó

### TC-05: Login con Password vacío
- **Módulo:** Login
- **Precondición:** estar en la página de login
- **Pasos:**
  1. Escribir `standard_user` en Username
  2. Dejar Password vacío
  3. Hacer clic en Login
- **Resultado esperado:** no permite entrar y muestra el mensaje "Epic sadface: Password is required"
- **Resultado real:** no permite entrar y muestra el mensaje "Epic sadface: Password is required"
- **Estado:** Pasó

### TC-06: Cerrar sesión desde el menú
- **Módulo:** Menú
- **Precondición:** sesión iniciada con `standard_user`
- **Pasos:**
  1. Estar en la página principal
  2. Abrir el menú de la esquina superior izquierda
  3. Hacer clic en Logout
- **Resultado esperado:** cierra la sesión y muestra la página de login
- **Resultado real:** cierra la sesión y muestra la página de login
- **Estado:** Pasó

### TC-07: Ordenar productos (las 4 opciones)
- **Módulo:** Inventario
- **Precondición:** sesión iniciada con `standard_user`
- **Pasos:**
  1. Estar en la página principal
  2. Abrir el desplegable de ordenar, arriba a la derecha (Name (A to Z))
  3. Elegir cada opción: Name (A to Z), Name (Z to A), Price (low to high) y Price (high to low)
- **Resultado esperado:** la lista se reordena correctamente con cada opción
- **Resultado real:** la lista se reordena correctamente con las 4 opciones
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `error_user`: muestra "Sorting is broken! This error has been reported to Backtrace" con las 4 opciones
  - `problem_user`: la lista no cambia y no aparece ningún aviso
  - `visual_user`: la lista se reordena de forma aleatoria, sin respetar el nombre ni el precio

### TC-08: Agregar un producto al carrito desde la lista
- **Módulo:** Inventario
- **Precondición:** sesión iniciada con `standard_user`
- **Pasos:**
  1. Hacer clic en "Add to cart" de un producto
- **Resultado esperado:** el botón cambia a "Remove" y el contador del carrito sube en 1
- **Resultado real:** el producto se agrega, el botón cambia a "Remove" y el contador sube en 1
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `error_user`: solo permite agregar 3 de los 6 productos (mochila, luz de bici y ropa de bebé), tanto desde la lista como desde el detalle
  - `problem_user`: solo permite agregar 3 de los 6 productos desde la lista; los demás sí se pueden agregar desde el detalle

### TC-09: Las imágenes de los productos son las correctas
- **Módulo:** Inventario
- **Precondición:** sesión iniciada con `standard_user`
- **Pasos:**
  1. Revisar la imagen de cada producto en la lista
- **Resultado esperado:** cada producto muestra su propia imagen
- **Resultado real:** cada producto muestra su imagen correcta
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `visual_user`: el primer producto de la lista muestra la imagen de un perro; en el detalle se ve la correcta
  - `problem_user`: todos los productos muestran la misma imagen incorrecta (un perro), y al abrir un producto el detalle corresponde a otro (por ejemplo, el nombre dice camiseta pero abre la ropa de bebé)

### TC-10: El precio de un producto es el mismo en la lista, el detalle y el carrito
- **Módulo:** Inventario / Carrito
- **Precondición:** sesión iniciada con `standard_user`
- **Pasos:**
  1. Anotar el precio de un producto en la lista
  2. Entrar al detalle del producto y comparar el precio
  3. Agregarlo al carrito y comparar el precio ahí
- **Resultado esperado:** el precio es el mismo en las 3 pantallas
- **Resultado real:** el precio es el mismo en las 3 pantallas
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `visual_user`: el precio de la lista es distinto al del detalle y al del carrito

### TC-11: Quitar un producto desde la lista y desde el detalle
- **Módulo:** Inventario
- **Precondición:** sesión iniciada con `standard_user` y un producto agregado al carrito
- **Pasos:**
  1. Hacer clic en "Remove" del producto en la página principal
  2. Agregarlo de nuevo, entrar al detalle del producto y hacer clic en "Remove"
- **Resultado esperado:** el botón vuelve a "Add to cart" y el contador baja en 1, tanto desde la lista como desde el detalle
- **Resultado real:** el producto se quita correctamente desde la lista y desde el detalle: el botón vuelve a "Add to cart" y el contador baja en 1
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `error_user`: no permite quitar el producto desde la lista ni desde el detalle
  - `problem_user`: no permite quitarlo desde la lista, y en el detalle el botón sigue diciendo "Add to cart" aunque el producto ya está agregado

### TC-12: Ver en el carrito los productos agregados
- **Módulo:** Carrito
- **Precondición:** sesión iniciada con `standard_user` y al menos un producto agregado
- **Pasos:**
  1. Hacer clic en el ícono del carrito
  2. Confirmar que se vean los productos agregados
- **Resultado esperado:** se ven en el carrito todos los productos agregados
- **Resultado real:** se ven en el carrito los productos agregados
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `problem_user`: el contador sube al agregar ciertos productos, pero el producto no aparece en el carrito (el detalle de ese producto muestra "Item not found")

### TC-13: Quitar un producto desde el carrito
- **Módulo:** Carrito
- **Precondición:** sesión iniciada con `standard_user` y un producto en el carrito
- **Pasos:**
  1. Abrir el carrito
  2. Hacer clic en "Remove" de un producto
- **Resultado esperado:** el producto desaparece del carrito y el contador baja en 1 (o desaparece si era el último)
- **Resultado real:** el producto se quita y el contador baja
- **Estado:** Pasó
- **Usuarios con fallas:** ninguno (`error_user` y `problem_user` sí pueden quitar productos desde el carrito)

### TC-14: Checkout con datos válidos
- **Módulo:** Checkout
- **Precondición:** sesión iniciada con `standard_user`, un producto en el carrito y en la pantalla de datos del comprador
- **Pasos:**
  1. Escribir nombre, apellido y código postal
  2. Hacer clic en Continue
- **Resultado esperado:** permite continuar a la pantalla de resumen del pedido
- **Resultado real:** permite continuar a la pantalla de resumen
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `error_user`: el campo Last Name no muestra lo que se escribe
  - `problem_user`: el campo Last Name modifica el campo First Name y Continue no permite avanzar

### TC-15: Checkout con el apellido vacío
- **Módulo:** Checkout
- **Precondición:** sesión iniciada con `standard_user`, un producto en el carrito y en la pantalla de datos del comprador
- **Pasos:**
  1. Escribir nombre y código postal, dejando Last Name vacío
  2. Hacer clic en Continue
- **Resultado esperado:** no avanza y muestra el error "Error: Last Name is required"
- **Resultado real:** no avanza y muestra el error "Error: Last Name is required"
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `error_user`: no valida el campo vacío y permite pasar a la pantalla de resumen

### TC-16: Completar la compra con el botón Finish
- **Módulo:** Checkout
- **Precondición:** sesión iniciada con `standard_user` y un producto en el carrito
- **Pasos:**
  1. Completar los datos del comprador y hacer clic en Continue
  2. En la pantalla de resumen, hacer clic en Finish
- **Resultado esperado:** muestra el mensaje de confirmación de la orden
- **Resultado real:** se confirma la orden
- **Estado:** Pasó
- **Usuarios con fallas:**
  - `error_user`: el botón Finish no permite completar la compra
  - `problem_user`: no se llega a Finish porque Continue no deja avanzar

### TC-17: El total del pedido coincide con la suma de los productos
- **Módulo:** Checkout
- **Precondición:** sesión iniciada con `standard_user`, dos productos en el carrito y en la pantalla de datos del comprador
- **Pasos:**
  1. Completar los datos y hacer clic en Continue
  2. En el resumen, sumar a mano los precios de los productos y comparar con Item total
  3. Verificar que Item total + Tax = Total
- **Resultado esperado:** la suma de los productos coincide con Item total, y Item total + Tax coincide con Total
- **Resultado real:** Sauce Labs Backpack $29.99 + Sauce Labs Bike Light $9.99 = $39.98 (Item total). Tax $3.20. Total $43.18. Todo coincide
- **Estado:** Pasó
- **Usuarios con fallas:** ninguno detectado

---

## Observaciones
- Los productos que un usuario deja en el carrito aparecen al iniciar sesión con otro usuario (probablemente el carrito se guarda en el navegador). Pendiente de confirmar.
- Antes de ejecutar cada caso se debe vaciar el carrito, para que el contador parta de 0.
- `performance_glitch_user`: funciona, pero con demoras en varias pantallas (ver video en `evidence/`). `locked_out_user`: cubierto en TC-02.

## Pendiente para después
- Mapa de funcionalidades y lista de riesgos
- Pruebas con números y caracteres especiales en los campos del checkout