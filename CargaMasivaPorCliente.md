
# Estructura del Archivo Excel para Carga Masiva de Campañas por Cliente

## 1. Estructura General del Archivo Excel

* **Formato del archivo**: El archivo debe ser un Excel legible por la librería `XLSX` (formatos compatibles: `.xlsx`, `.xls`).

* **Hojas requeridas**:
  * **`CabeceraPorCliente`**: Contiene la información general de las campañas.
  * **`DetallePorCliente`**: Contiene los detalles de artículos, clientes y requisitos asociados a las campañas.

* **Codificación de datos**:
  * Los campos de texto no deben contener espacios en blanco al inicio o al final.
  * Las fechas deben estar en un formato reconocible (ver sección de fechas).
  * Los números deben ser valores válidos (sin caracteres no numéricos, salvo en casos específicos como decimales con `.`).
  * El campo `campAgrupa` acepta valores como `Sí`, `Si`, `S`, `1`, `No`, `N`, `0` (case-insensitive).

* **Validaciones**:
  * El validador revisará que ambas hojas estén presentes y con nombres exactos.
  * Se verificará que todas las columnas requeridas estén presentes.
  * Se asegurará la consistencia entre hojas (campañas definidas en cabecera deben existir en detalle).
  * Se validan reglas de negocio: prioridad, cantidades, fechas, requisitos, y **no se permite el mismo artículo en múltiples campañas con la misma prioridad**.

---

## 2. Estructura de la Hoja `CabeceraPorCliente`

Esta hoja contiene la información general de las campañas. Debe incluir las siguientes columnas:

### Columnas Requeridas

| Columna                        | Descripción                                | Tipo de dato | Ejemplo             | Notas |
|--------------------------------|--------------------------------------------|--------------|---------------------|-------|
| `campaigns/campNombre`         | Nombre único de la campaña                 | Texto        | `PROMO-2025-11`     | **Requerido**. Debe ser único en toda la hoja. |
| `campaigns/campDescripcion`    | Descripción de la campaña                  | Texto        | `Promoción noviembre` | **Requerido**. |
| `campaigns/campFechaInicio`    | Fecha de inicio de la campaña              | Fecha        | `01/11/2025`        | **Requerido**. Formato `DD/MM/YYYY` o ISO. |
| `campaigns/campFechaFin`       | Fecha de fin de la campaña                 | Fecha        | `30/11/2025`        | **Requerido**. Debe ser ≥ `campFechaInicio`. |
| `campaigns/campPrioridad`      | Prioridad de la campaña                    | Texto        | `Alta`              | **Requerido**. Valores válidos: `Muy Alta`, `Alta`, `Media Alta`, `Media`, `Baja`. |
| `campaigns/campTipo`           | Tipo de campaña                            | Texto        | `PorCliente`        | **Requerido**. Generalmente `PorCliente`. |
| `campaigns/campAgrupa`         | ¿Agrupa artículos?                         | Sí/No        | `Sí`                | **Requerido**. Acepta: `Sí`, `Si`, `S`, `1`, `No`, `N`, `0`. |

### Validaciones de la Hoja `CabeceraPorCliente`

* **Nombre de campaña (`campNombre`)**: No puede estar vacío ni repetirse.
* **Fechas**:
  * Deben ser válidas.
  * `campFechaInicio` no puede ser posterior a `campFechaFin`.
* **Prioridad**: Solo se aceptan: `Muy Alta`, `Alta`, `Media Alta`, `Media`, `Baja`.
* **campAgrupa**: Solo valores `Sí`/`No` válidos.
* **Columnas faltantes**: Si falta alguna requerida, se devuelve error.

### Ejemplo de Datos Válidos para `CabeceraPorCliente`

```
campaigns/campNombre | campaigns/campDescripcion | campaigns/campFechaInicio | campaigns/campFechaFin | campaigns/campPrioridad | campaigns/campTipo | campaigns/campAgrupa
---------------------|---------------------------|---------------------------|------------------------|-------------------------|--------------------|---------------------
PROMO-2025-11        | Promo noviembre clientes  | 01/11/2025                | 30/11/2025             | Alta                    | PorCliente         | Sí
PROMO-2025-12        | Descuentos diciembre      | 01/12/2025                | 31/12/2025             | Media                   | PorCliente         | No
```

---

## 3. Estructura de la Hoja `DetallePorCliente`

Esta hoja contiene los detalles de artículos, clientes y requisitos asociados a las campañas definidas en `CabeceraPorCliente`.

### Columnas Requeridas

| Columna                        | Descripción                                | Tipo de dato | Ejemplo             | Notas |
|--------------------------------|--------------------------------------------|--------------|---------------------|-------|
| `articles/campNombre`          | Nombre de la campaña                       | Texto        | `PROMO-2025-11`     | **Requerido**. Debe existir en `CabeceraPorCliente`. |
| `articles/artid`               | Código del artículo                        | Texto        | `61-0-11-6`         | **Requerido**. No puede estar vacío. |
| `articles/artNombre`           | Nombre del artículo                        | Texto        | `Agua 2L x6`        | **Requerido**. |
| `articles/cantidadMin`         | Cantidad mínima                            | Número       | `6`                 | **Requerido**. > 0. |
| `articles/cantidadMax`         | Cantidad máxima                            | Número       | `24`                | **Requerido**. ≥ `cantidadMin`. |
| `articles/precioPromocional`   | Precio promocional                         | Número       | `19.50`             | **Requerido**. ≥ 0. |
| `clients/cliId`                | ID del cliente                             | Texto        | `CLI-1001`          | **Requerido**. |
| `clients/cliNombre`            | Nombre del cliente                         | Texto        | `Supermercado Central` | **Requerido**. |

### Columnas Opcionales (Requisitos)

| Columna                            | Descripción                                | Tipo de dato | Ejemplo             | Notas |
|------------------------------------|--------------------------------------------|--------------|---------------------|-------|
| `requirements/artidRequisito`      | Artículo requerido                         | Texto        | `33-0-3-12`         | Opcional. Si se incluye, debe ir con `cantidadRequisito`. |
| `requirements/cantidadRequisito`   | Cantidad requerida                         | Número       | `1`                 | Requerido si hay requisito. > 0. |
| `requirements/cantidadMin`         | Cantidad mínima del requisito              | Número       | `1`                 | Opcional. ≥ 0. |
| `requirements/cantidadMax`         | Cantidad máxima del requisito              | Número       | `12`                | Opcional. ≥ `cantidadMin`. |
| `requirements/precioPromocional`   | Precio del artículo requerido              | Número       | `45.00`             | Opcional. ≥ 0. |

### Validaciones de la Hoja `DetallePorCliente`

* **Consistencia de `campNombre`**:
  * `articles/campNombre` debe existir en `CabeceraPorCliente`.
* **Artículos**:
  * `artid` no puede estar vacío.
  * `cantidadMin > 0`.
  * `cantidadMax ≥ cantidadMin`.
  * `precioPromocional ≥ 0`.
* **Clientes**:
  * `cliId` y `cliNombre` obligatorios.
* **Requisitos (si se incluyen)**:
  * `artidRequisito` y `cantidadRequisito` son obligatorios juntos.
  * `cantidadRequisito > 0`.
  * No se permite que `artidRequisito` sea igual a `articles/artid`.
  * `cantidadMax ≥ cantidadMin` si ambos están presentes.
* **Regla global**:
  * **No se permite el mismo artículo (principal o requisito) en múltiples campañas con la misma prioridad.**

---

## 4. Formato de Fechas

El validador acepta fechas en los siguientes formatos:

* **Formato DD/MM/YYYY**: `01/11/2025` (recomendado).
* **Formato ISO parcial**: `2025-11-01`.
* **Formato serial de Excel**: Número (ej: `46306` → se convierte automáticamente).

> **Recomendación**: Usa `DD/MM/YYYY` para evitar ambigüedades.

---

## 5. Errores Comunes y Cómo Evitarlos

| Error | Causa | Solución |
|-------|-------|----------|
| `Faltan hojas requeridas` | Falta `CabeceraPorCliente` o `DetallePorCliente` | Asegúrate de tener ambas hojas con nombres exactos. |
| `Faltan columnas requeridas en CabeceraPorCliente` | Falta alguna columna obligatoria | Verifica nombres exactos (con `/`). |
| `Nombre de campaña duplicado` | Mismo `campNombre` en varias filas | Usa nombres únicos. |
| `Fecha de inicio posterior a fecha de fin` | Orden incorrecto | Corrige las fechas. |
| `Prioridad debe ser: Muy Alta, Alta, ...` | Valor no permitido | Usa solo los 5 valores válidos. |
| `campAgrupa debe ser: Sí, Si, S, 1, No, N, 0` | Valor inválido | Usa formato correcto. |
| `Cantidad mínima debe ser mayor a 0` | `cantidadMin ≤ 0` | Ingresa valor positivo. |
| `Cantidad máxima debe ser mayor o igual a mínima` | `cantidadMax < cantidadMin` | Ajusta cantidades. |
| `ID de cliente es requerido` | `cliId` vacío | Completa `cliId` y `cliNombre`. |
| `No se permite el mismo artículo como principal y requisito` | `artid` = `artidRequisito` | Usa artículo diferente. |
| `Producto X en múltiples campañas con prioridad "Y"` | Mismo artículo en 2+ campañas con misma prioridad | Ajusta prioridad o elimina duplicados. |

---

## 6. Pasos para Cargar el Archivo

1. **Preparar el archivo Excel**:
   * Crea dos hojas: `CabeceraPorCliente` y `DetallePorCliente`.
   * Usa nombres de columnas **exactos** (con `/`).
   * Completa datos respetando tipos y reglas.
   * Verifica que `campNombre` sea consistente entre hojas.

2. **Cargar el archivo**:
   * Usa la función `validateCampaignClientExcel(file)`.
   * Sube el archivo `.xlsx`.

3. **Revisar los resultados**:
   * Si `isValid: true` → datos listos para backend.
   * Si `isValid: false` → revisa `errors[]` (fila, campo, mensaje).
   * Corrige y vuelve a subir.

---

## 7. Ejemplo Completo de Archivo Excel

### Hoja: `CabeceraPorCliente`

```
campaigns/campNombre | campaigns/campDescripcion | campaigns/campFechaInicio | campaigns/campFechaFin | campaigns/campPrioridad | campaigns/campTipo | campaigns/campAgrupa
---------------------|---------------------------|---------------------------|------------------------|-------------------------|--------------------|---------------------
PROMO-2025-11        | Promo noviembre clientes  | 01/11/2025                | 30/11/2025             | Alta                    | PorCliente         | Sí
PROMO-2025-12        | Descuentos diciembre      | 01/12/2025                | 31/12/2025             | Media                   | PorCliente         | No
```

### Hoja: `DetallePorCliente`

```
articles/campNombre | articles/artid | articles/artNombre | articles/cantidadMin | articles/cantidadMax | articles/precioPromocional | clients/cliId | clients/cliNombre      | requirements/artidRequisito | requirements/cantidadRequisito | requirements/cantidadMin | requirements/cantidadMax | requirements/precioPromocional
--------------------|----------------|--------------------|----------------------|----------------------|----------------------------|---------------|------------------------|-----------------------------|-------------------------------|--------------------------|--------------------------|-------------------------------
PROMO-2025-11       | 61-0-11-6      | Agua 2L x6         | 6                    | 24                   | 19.50                      | CLI-1001      | Supermercado Central   | 33-0-3-12                   | 1                             | 1                        | 12                       | 45.00
PROMO-2025-11       | 61-0-11-7      | Gaseosa 3L x6      | 4                    | 12                   | 28.00                      | CLI-1002      | Tienda Doña María      |                             |                               |                          |                          | 
PROMO-2025-12       | 61-0-11-6      | Agua 2L x6         | 10                   | 50                   | 18.00                      | CLI-1003      | Bodega Sur             |                             |                               |                          |                          | 
```

---

## 8. Notas Adicionales

* **Nombres de columnas**: Exactos, con `/`. Ej: `campaigns/campNombre`, no `campNombre`.
* **Validación automática**: Consistencia entre hojas, reglas de negocio y transformación.
* **Transformación de datos**:
  * Fechas → `Date` → ISO string.
  * `campAgrupa` → `true`/`false`.
  * Campos opcionales → `undefined` si faltan.
* **Errores detallados**: Incluyen hoja, fila, campo y mensaje claro.
* **Función principal**: `validateCampaignClientExcel(file)` → retorna:
  ```ts
  {
    isValid: boolean;
    errors: ValidationError[];
    data: CampaignClientData[];
    rowCount: number;
  }
  ```

---

## 9. Solución de Problemas

* **Archivo no se carga**: Verifica formato `.xlsx` y que no esté corrupto.
* **Errores de fecha**: Usa `DD/MM/YYYY`.
* **Errores de columnas**: Compara con tablas arriba.
* **Errores de duplicados por prioridad**: Ajusta `campPrioridad` o elimina campañas duplicadas.

