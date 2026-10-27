# Diccionario de Datos — I2-Sync

## 1. Introducción

El diccionario de datos describe las entidades, los atributos y las relaciones que forman parte del sistema I2-Sync. Su finalidad es establecer una definición clara y uniforme de la información utilizada para registrar pedidos, identificar clientes y usuarios, y facilitar la sincronización con el ERP local I2 de MTH S.R.L.

Los identificadores `id_cliente` e `id_usuario` pueden aparecer en más de una tabla porque permiten relacionar registros de distintas entidades. Por ejemplo, `id_cliente` identifica al cliente asociado a un pedido, mientras que `id_usuario` permite identificar al usuario responsable de registrar o gestionar una operación. En la tabla donde se define cada entidad, el identificador funciona como clave primaria (PK); cuando se utiliza en otra tabla para establecer una relación, funciona como clave foránea (FK). Esta repetición no implica duplicar la identidad del cliente o del usuario, sino mantener la integridad referencial entre las tablas.

## 2. Diccionario de datos inicial

### 2.1. Tabla: CLIENTE

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_cliente` | Identificador único del cliente | INT | PK |
| `nombre_cliente` | Nombre o razón social del cliente | VARCHAR | — |

### 2.2. Tabla: PRODUCTO

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_producto` | Identificador único del producto | INT | PK |
| `codigo_sku` | Código SKU utilizado para identificar el producto en el inventario | VARCHAR | — |

### 2.3. Tabla: USUARIO

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_usuario` | Identificador único del usuario del sistema | INT | PK |
| `nombre_completo` | Nombre y apellido del usuario | VARCHAR | — |
| `email_login` | Correo electrónico utilizado para iniciar sesión | VARCHAR | — |
| `rol_acceso` | Rol o perfil de permisos asignado al usuario | VARCHAR | — |
| `Activo` | Indica si el usuario se encuentra habilitado | BOOLEAN | — |

### 2.4. Tabla: PEDIDO_VENTA

Esta tabla representa los pedidos registrados durante el proceso de venta en ruta.

| Atributo | Descripción | Tipo de dato | Clave |
|---|---|---|---|
| `id_pedido` | Identificador único del pedido | INT | PK |
| `id_cliente` | Cliente al que corresponde el pedido | INT | FK |
| `id_usuario` | Usuario que registra o gestiona el pedido | INT | FK |
| `ped_estado_sincro` | Indica si el pedido fue sincronizado correctamente con el ERP | BOOLEAN | — |

## 3. Relaciones entre entidades

- **CLIENTE – PEDIDO_VENTA:** un cliente puede tener varios pedidos. El atributo `id_cliente` de PEDIDO_VENTA referencia a `id_cliente` de CLIENTE.
- **USUARIO – PEDIDO_VENTA:** un usuario puede registrar o gestionar varios pedidos. El atributo `id_usuario` de PEDIDO_VENTA referencia a `id_usuario` de USUARIO.

## 4. Consideraciones

Los tipos de datos y atributos incluidos constituyen una estructura inicial. Antes de considerar definitivo el diccionario, deben contrastarse con el modelo de datos completo y con las reglas de negocio del sistema I2-Sync.
