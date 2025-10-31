# Documentación de Endpoints de la API

## Tabla de Contenidos

- [Autenticación](#autenticación)
- [Campañas](#campañas)
- [Autenticación CFE](#autenticación-cfe)
- [Clientes](#clientes)
- [Conceptos](#conceptos)
- [Dashboard](#dashboard)
- [Lista de Precios](#lista-de-precios)
- [Marcas](#marcas)
- [Recorridos](#recorridos)
- [Rutas](#rutas)
- [Artículos](#artículos)

---

## Autenticación

**Controlador:** `AuthController`
**Ruta Base:** `/api/Auth`

### Iniciar Sesión

- **Endpoint:** `POST /api/Auth/login`
- **Descripción:** Autentica a un usuario utilizando LDAP y devuelve un token JWT si la autenticación es exitosa.
- **Request Body:**
  ```json
  {
    "username": "nombre_de_usuario",
    "password": "contraseña"
  }
  ```
- **Respuestas:**
  - `200 OK`: Autenticación exitosa. Devuelve un `AuthenticationResultDto`.
  - `401 Unauthorized`: Credenciales inválidas.
  - `500 Internal Server Error`: Error interno del servidor.

### Validar Token

- **Endpoint:** `POST /api/Auth/validate-token`
- **Descripción:** Valida un token JWT.
- **Request Body:**
  ```json
  {
    "token": "jwt_token"
  }
  ```
- **Respuestas:**
  - `200 OK`: Devuelve `true` si el token es válido, `false` en caso contrario.
  - `500 Internal Server Error`: Error interno del servidor.

### Obtener Información del Usuario

- **Endpoint:** `GET /api/Auth/user-info`
- **Descripción:** Obtiene la información del usuario autenticado.
- **Autenticación:** Requiere token JWT.
- **Respuestas:**
  - `200 OK`: Devuelve un `UserInfoDto`.
  - `401 Unauthorized`: No autorizado.
  - `500 Internal Server Error`: Error interno del servidor.

---

## Campañas

**Controlador:** `CampaignsController`
**Ruta Base:** `/api/Campaigns`

### Obtener Campañas

- **Endpoint:** `GET /api/Campaigns`
- **Descripción:** Obtiene una lista paginada de campañas con filtros opcionales.
- **Query Parameters:**
  - `campNombre` (string): Filtrar por nombre de campaña.
  - `campEstado` (string): Filtrar por estado de campaña.
  - `campPrioridad` (int): Filtrar por prioridad de campaña.
  - `campFechaInicio` (DateTime): Filtrar por fecha de inicio.
  - `campFechaFin` (DateTime): Filtrar por fecha de fin.
  - `pageNumber` (int): Número de página.
  - `pageSize` (int): Tamaño de página.
- **Respuestas:**
  - `200 OK`: Devuelve un `CampaignPagedDto`.
  - `400 Bad Request`: Error en la solicitud.

### Obtener Campaña por ID

- **Endpoint:** `GET /api/Campaigns/{id}`
- **Descripción:** Obtiene una campaña por su ID.
- **Respuestas:**
  - `200 OK`: Devuelve un `CampaignDto`.
  - `404 Not Found`: Campaña no encontrada.

### Obtener Campañas Activas

- **Endpoint:** `GET /api/Campaigns/activas`
- **Descripción:** Obtiene una lista de todas las campañas activas.
- **Respuestas:**
  - `200 OK`: Devuelve una lista de `CampaignDto`.

### Crear Campaña

- **Endpoint:** `POST /api/Campaigns`
- **Descripción:** Crea una nueva campaña.
- **Request Body:** `CampaignCreateDto`
- **Respuestas:**
  - `201 Created`: Campaña creada exitosamente. Devuelve un `CampaignDto`.
  - `400 Bad Request`: Error en la solicitud.

### Cambiar Estado de Campaña

- **Endpoint:** `PUT /api/Campaigns/{id}/estado`
- **Descripción:** Cambia el estado de una campaña.
- **Request Body:**
  ```json
  {
    "newEstado": "nuevo_estado"
  }
  ```
- **Respuestas:**
  - `200 OK`: Estado actualizado. Devuelve un `CampaignDto`.
  - `404 Not Found`: Campaña no encontrada.

### Actualizar Campaña (Básico)

- **Endpoint:** `PUT /api/Campaigns/{id}/basic`
- **Descripción:** Actualiza los campos básicos de una campaña.
- **Request Body:** `CampaignUpdateBasicDto`
- **Respuestas:**
  - `200 OK`: Campaña actualizada. Devuelve un `CampaignDto`.
  - `404 Not Found`: Campaña no encontrada.

### Actualizar Campaña

- **Endpoint:** `PUT /api/Campaigns/{id}`
- **Descripción:** Actualiza una campaña completa.
- **Request Body:** `CampaignCreateDto`
- **Respuestas:**
  - `200 OK`: Campaña actualizada. Devuelve un `CampaignDto`.
  - `404 Not Found`: Campaña no encontrada.

### Eliminar Campaña

- **Endpoint:** `DELETE /api/Campaigns/{id}`
- **Descripción:** Elimina una campaña.
- **Respuestas:**
  - `200 OK`: Campaña eliminada. Devuelve `true`.
  - `404 Not Found`: Campaña no encontrada.

---

## Autenticación CFE

**Controlador:** `CfeAuthController`
**Ruta Base:** `/api/CfeAuth`

### Iniciar Sesión CFE

- **Endpoint:** `POST /api/CfeAuth/login`
- **Descripción:** Autentica a un usuario utilizando CFE y devuelve un token JWT.
- **Request Body:**
  ```json
  {
    "username": "nombre_de_usuario",
    "password": "contraseña"
  }
  ```
- **Respuestas:**
  - `200 OK`: Autenticación exitosa. Devuelve un `AuthenticationResultDto`.
  - `401 Unauthorized`: Credenciales inválidas.
  - `500 Internal Server Error`: Error interno del servidor.

### Validar Token CFE

- **Endpoint:** `POST /api/CfeAuth/validate-token`
- **Descripción:** Valida un token JWT.
- **Request Body:**
  ```json
  {
    "token": "jwt_token"
  }
  ```
- **Respuestas:**
  - `200 OK`: Devuelve `true` si el token es válido, `false` en caso contrario.
  - `500 Internal Server Error`: Error interno del servidor.

### Obtener Información del Usuario CFE

- **Endpoint:** `GET /api/CfeAuth/user-info`
- **Descripción:** Obtiene la información del usuario autenticado.
- **Autenticación:** Requiere token JWT.
- **Respuestas:**
  - `200 OK`: Devuelve un `UserInfoDto`.
  - `401 Unauthorized`: No autorizado.
  - `500 Internal Server Error`: Error interno del servidor.

---

## Clientes

**Controlador:** `ClientesController`
**Ruta Base:** `/api/Clientes`

### Obtener Clientes

- **Endpoint:** `GET /api/Clientes`
- **Descripción:** Obtiene una lista paginada de clientes.
- **Query Parameters:**
  - `estado` (string): Filtrar por estado.
  - `lisId` (long): Filtrar por ID de lista de precios.
  - `pageNumber` (int): Número de página.
  - `pageSize` (int): Tamaño de página.
  - `disablePagination` (bool): Deshabilitar paginación.
- **Respuestas:**
  - `200 OK`: Devuelve un `VdtConfigClientePagedDto`.

### Obtener Clientes (Dropdown)

- **Endpoint:** `GET /api/Clientes/dropdown`
- **Descripción:** Obtiene una lista de clientes para un dropdown.
- **Query Parameters:**
  - `estado` (string): Filtrar por estado.
- **Respuestas:**
  - `200 OK`: Devuelve una lista de `VdtConfigClienteDto`.

### Obtener Cliente por ID

- **Endpoint:** `GET /api/Clientes/{id}`
- **Descripción:** Obtiene un cliente por su ID.
- **Respuestas:**
  - `200 OK`: Devuelve un `VdtConfigClienteDto`.
  - `404 Not Found`: Cliente no encontrado.

### Obtener Cliente por Código

- **Endpoint:** `GET /api/Clientes/codigo/{codigo}`
- **Descripción:** Obtiene un cliente por su código.
- **Respuestas:**
  - `200 OK`: Devuelve un `VdtConfigClienteDto`.
  - `404 Not Found`: Cliente no encontrado.

### Crear Cliente

- **Endpoint:** `POST /api/Clientes`
- **Descripción:** Crea un nuevo cliente.
- **Request Body:** `VdtConfigClienteCreateDto`
- **Respuestas:**
  - `201 Created`: Cliente creado. Devuelve un `VdtConfigClienteDto`.

### Actualizar Cliente

- **Endpoint:** `PUT /api/Clientes/{id}`
- **Descripción:** Actualiza un cliente.
- **Request Body:** `VdtConfigClienteCreateDto`
- **Respuestas:**
  - `200 OK`: Cliente actualizado. Devuelve un `VdtConfigClienteDto`.
  - `404 Not Found`: Cliente no encontrado.

### Eliminar Cliente

- **Endpoint:** `DELETE /api/Clientes/{id}`
- **Descripción:** Elimina un cliente.
- **Respuestas:**
  - `200 OK`: Cliente eliminado. Devuelve `true`.
  - `404 Not Found`: Cliente no encontrado.

---

## Conceptos

**Controlador:** `ConceptosController`
**Ruta Base:** `/api/Conceptos`

### Obtener Conceptos

- **Endpoint:** `GET /api/Conceptos`
- **Descripción:** Obtiene una lista de conceptos.
- **Query Parameters:**
  - `filter` (string): Filtro de búsqueda.
- **Respuestas:**
  - `200 OK`: Devuelve una lista de `VdtConceptoDto`.

---

## Dashboard

**Controlador:** `DashboardController`
**Ruta Base:** `/api/Dashboard`

### Obtener Datos del Dashboard

- **Endpoint:** `GET /api/Dashboard`
- **Descripción:** Obtiene los datos para el dashboard.
- **Respuestas:**
  - `200 OK`: Devuelve un `DashboardDto`.

---

## Lista de Precios

**Controlador:** `ListaPreciosController`
**Ruta Base:** `/api/ListaPrecios`

### Obtener Listas de Precios

- **Endpoint:** `GET /api/ListaPrecios`
- **Descripción:** Obtiene una lista paginada de listas de precios.
- **Query Parameters:**
  - `estado` (string): Filtrar por estado.
  - `nombre` (string): Filtrar por nombre.
  - `categoria` (int): Filtrar por categoría.
  - `pageNumber` (int): Número de página.
  - `pageSize` (int): Tamaño de página.
  - `disablePagination` (bool): Deshabilitar paginación.
- **Respuestas:**
  - `200 OK`: Devuelve un `VntListaPrecioPagedDto`.

### Obtener Listas de Precios (Dropdown)

- **Endpoint:** `GET /api/ListaPrecios/dropdown`
- **Descripción:** Obtiene listas de precios para un dropdown.
- **Query Parameters:**
  - `estado` (string): Filtrar por estado.
- **Respuestas:**
  - `200 OK`: Devuelve una lista de `VntListaPrecioDto`.

---

## Marcas

**Controlador:** `MarcasController`
**Ruta Base:** `/api/Marcas`

### Obtener Marcas

- **Endpoint:** `GET /api/Marcas`
- **Descripción:** Obtiene todas las marcas.
- **Respuestas:**
  - `200 OK`: Devuelve una lista de `VdtMarcaDto`.

---

## Recorridos

**Controlador:** `RecorridosController`
**Ruta Base:** `/api/Recorridos`

### Obtener Recorridos

- **Endpoint:** `GET /api/Recorridos`
- **Descripción:** Obtiene una lista paginada de recorridos.
- **Query Parameters:**
  - `entIdVendedor` (int): Filtrar por ID de vendedor.
  - `nombre` (string): Filtrar por nombre.
  - `pageNumber` (int): Número de página.
  - `pageSize` (int): Tamaño de página.
- **Respuestas:**
  - `200 OK`: Devuelve un `VdtRecorridoPagedDto`.

---

## Rutas

**Controlador:** `RutasController`
**Ruta Base:** `/api/Rutas`

### Obtener Rutas

- **Endpoint:** `GET /api/Rutas`
- **Descripción:** Obtiene una lista paginada de rutas.
- **Query Parameters:**
  - `entIdVendedor` (int): Filtrar por ID de vendedor.
  - `nombre` (string): Filtrar por nombre.
  - `pageNumber` (int): Número de página.
  - `pageSize` (int): Tamaño de página.
- **Respuestas:**
  - `200 OK`: Devuelve un `VdtRutaPagedDto`.

---

## Artículos

**Controlador:** `VntConfigArticulosController`
**Ruta Base:** `/api/VntConfigArticulos`

### Obtener Artículos

- **Endpoint:** `GET /api/VntConfigArticulos`
- **Descripción:** Obtiene una lista paginada de artículos.
- **Query Parameters:**
  - `estado` (string): Filtrar por estado.
  - `nombre` (string): Filtrar por nombre.
  - `pageNumber` (int): Número de página.
  - `pageSize` (int): Tamaño de página.
  - `disablePagination` (bool): Deshabilitar paginación.
- **Respuestas:**
  - `200 OK`: Devuelve un `VntConfigArticuloPagedDto`.

### Obtener Artículos (Dropdown)

- **Endpoint:** `GET /api/VntConfigArticulos/dropdown`
- **Descripción:** Obtiene artículos para un dropdown.
- **Query Parameters:**
  - `estado` (string): Filtrar por estado.
  - `artTipoArticulo` (string): Filtrar por tipo de artículo.
- **Respuestas:**
  - `200 OK`: Devuelve una lista de `VntConfigArticuloDto`.
