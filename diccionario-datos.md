
# Diccionario de Datos — I2-Sync

## 1. Introducción

El sistema I2-Sync es un módulo de gestión comercial desarrollado como propuesta para MTH S.R.L. Su finalidad es permitir la consulta de productos y stock, el registro de pedidos de venta desde dispositivos móviles y la sincronización de las operaciones con el ERP local I2.

El diccionario de datos define las entidades, atributos y relaciones necesarios para organizar la información del sistema.

Los identificadores `id_cliente` e `id_usuario` aparecen en más de una tabla porque permiten establecer relaciones entre entidades. En CLIENTE y USUARIO funcionan como claves primarias (PK), mientras que en PEDIDO_VENTA funcionan como claves foráneas (FK).

Esta repetición no representa una duplicación incorrecta de información. Permite relacionar cada pedido con su cliente y con el usuario que lo registró, manteniendo la integridad referencial.

## 2. Diccionario de datos inicial

### 2.1. Tabla: CLIENTE

Almacena la información de los clientes que realizan compras a MTH S.R.L.

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_cliente` | Identificador único del cliente | INT | PK |
| `nombre_cliente` | Nombre o razón social del cliente | VARCHAR | — |
| `cuit` | CUIT del cliente, almacenado como texto para conservar su formato | VARCHAR | — |
| `domicilio` | Dirección registrada del cliente | VARCHAR | — |
| `telefono` | Número de contacto del cliente | VARCHAR | — |

### 2.2. Tabla: PRODUCTO

Almacena la información de los productos comercializados por MTH S.R.L.

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_producto` | Identificador único del producto | INT | PK |
| `codigo_sku` | Código utilizado para identificar el producto en el inventario | VARCHAR | — |
| `nombre_producto` | Nombre comercial del producto | VARCHAR | — |
| `categoria` | Categoría a la que pertenece el producto | VARCHAR | — |
| `precio_unitario` | Precio de venta por unidad | DECIMAL | — |
| `stock_disponible` | Cantidad de unidades disponibles para venta o despacho | INT | — |

### 2.3. Tabla: USUARIO

Almacena los datos de las personas autorizadas para operar en I2-Sync, como vendedores, personal de depósito y administradores.

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_usuario` | Identificador único del usuario | INT | PK |
| `nombre_completo` | Nombre y apellido del usuario | VARCHAR | — |
| `email_login` | Correo electrónico utilizado para iniciar sesión | VARCHAR | — |
| `rol_acceso` | Perfil que determina los permisos del usuario | VARCHAR | — |
| `activo` | Indica si el usuario está habilitado para operar | BOOLEAN | — |

### 2.4. Tabla: PEDIDO_VENTA

Registra los pedidos comerciales realizados por vendedores o personal autorizado.

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_pedido` | Identificador único del pedido de venta | INT | PK |
| `fecha_emision` | Fecha y hora de registro del pedido | DATETIME | — |
| `id_cliente` | Identificador del cliente asociado al pedido | INT | FK |
| `id_usuario` | Identificador del usuario que registra el pedido | INT | FK |
| `monto_total` | Importe total del pedido | DECIMAL | — |
| `ped_estado_sincro` | Indica si el pedido fue sincronizado correctamente con el ERP I2 | BOOLEAN | — |

El campo `ped_estado_sincro` permanece en FALSE mientras la operación esté pendiente de sincronización. Solo se establece en TRUE después de recibir la confirmación satisfactoria del ERP I2.

### 2.5. Tabla: DETALLE_PEDIDO

Registra los productos incluidos en cada pedido, con sus respectivas cantidades y precios. Permite relacionar PEDIDO_VENTA con PRODUCTO.

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_detalle` | Identificador único del detalle | INT | PK |
| `id_pedido` | Identificador del pedido al que pertenece | INT | FK |
| `id_producto` | Identificador del producto incluido | INT | FK |
| `cantidad` | Cantidad de unidades solicitadas | INT | — |
| `precio_unitario` | Precio por unidad aplicado al registrar el pedido | DECIMAL | — |
| `subtotal` | Importe resultante de multiplicar cantidad por precio unitario | DECIMAL | — |

## 3. Relaciones entre entidades

- **CLIENTE – PEDIDO_VENTA:** un cliente puede tener varios pedidos. `PEDIDO_VENTA.id_cliente` referencia a `CLIENTE.id_cliente`.
- **USUARIO – PEDIDO_VENTA:** un usuario puede registrar varios pedidos. `PEDIDO_VENTA.id_usuario` referencia a `USUARIO.id_usuario`.
- **PEDIDO_VENTA – DETALLE_PEDIDO:** un pedido puede contener varios registros de detalle. `DETALLE_PEDIDO.id_pedido` referencia a `PEDIDO_VENTA.id_pedido`.
- **PRODUCTO – DETALLE_PEDIDO:** un producto puede aparecer en diferentes pedidos. `DETALLE_PEDIDO.id_producto` referencia a `PRODUCTO.id_producto`.

## 4. Consideraciones de diseño

Los nombres de atributos que aparecen en distintas entidades responden a relaciones entre tablas o a datos que cumplen funciones específicas.

Por ejemplo, `precio_unitario` en PRODUCTO representa el precio del producto, mientras que en DETALLE_PEDIDO registra el precio aplicado al momento de la operación.

El diccionario constituye una propuesta inicial del modelo de datos de I2-Sync. Los tipos y atributos deberán contrastarse con la estructura real del ERP I2 antes de implementar la sincronización definitiva.
