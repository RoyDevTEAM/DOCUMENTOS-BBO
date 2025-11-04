# Estructura del Archivo Excel para Carga Masiva de Campañas por Cliente

## 1. Estructura General del Archivo Excel

- **Formato del archivo**: Excel compatible con `xlsx` (`.xlsx` o `.xls`).
- **Hoja requerida**:
  - **`CampañaPorCliente`**: Contiene toda la información de campañas, artículos, clientes y requisitos.
- **Codificación de datos**:
  - Textos sin espacios al inicio/final.
  - Fechas en formato válido (ver sección de fechas).
  - Números sin símbolos (excepto `.` para decimales).
- **Validaciones**:
  - Se verifica hoja, columnas obligatorias y consistencia de datos.
  - Errores detallados por fila y campo.

---

## 2. Estructura de la Hoja `CampañaPorCliente`

### Columnas Requeridas

| Columna                          | Descripción                                      | Tipo de dato | Ejemplo                  | Notas                                                                 |
|----------------------------------|--------------------------------------------------|--------------|--------------------------|-----------------------------------------------------------------------|
| `campaigns/campNombre`           | Nombre único de la campaña                       | Texto        | `PROMO-2025-11`          | **Requerido**. Debe ser único en el archivo.                          |
| `campaigns/campDescripcion`      | Descripción de la campaña                        | Texto        | `Promoción noviembre`    | **Requerido**.                                                                |
| `campaigns/campFechaInicio`      | Fecha de inicio                                  | Fecha        | `01/11/2025`             | **Requerido**. Formato `DD/MM/YYYY` o ISO.                            |
| `campaigns/campFechaFin`         | Fecha de fin                                     | Fecha        | `30/11/2025`             | **Requerido**. Debe ser ≥ `campFechaInicio`.                          |
| `campaigns/campPrioridad`        | Prioridad                                        | Texto        | `Alta`                   | **Requerido**. Solo: `Alta`, `Media`, `Baja`.                         |
| `campaigns/campTipo`             | Tipo de campaña                                  | Texto        | `PorCliente`             | **Requerido**. Generalmente `PorCliente`.                             |
| `articles/campNombre`            | Nombre de campaña (para artículo)                | Texto        | `PROMO-2025-11`          | **Requerido**. Debe coincidir con `campaigns/campNombre`.             |
| `articles/artid`                 | Código del artículo                              | Texto        | `61-0-11-6`              | **Requerido**. No puede estar vacío.                                  |
| `articles/cantidadMin`           | Cantidad mínima                                  | Número       | `6`                      | **Requerido**. > 0.                                                   |
| `articles/cantidadMax`           | Cantidad máxima                                  | Número       | `24`                     | **Requerido**. ≥ `cantidadMin`.                                       |
| `articles/precioPromocional`     | Precio promocional                               | Número       | `19.50`                  | **Requerido**. ≥ 0.                                                   |
| `clients/cliId`                  | ID del cliente                                   | Texto        | `CLI-1001`               | **Requerido**. Identificador único del cliente.                       |
| `clients/cliNombre`              | Nombre del cliente                               | Texto        | `Supermercado Central`   | **Requerido**.                                                                |

---

### Columnas Opcionales

| Columna                            | Descripción                                      | Tipo de dato | Ejemplo                  | Notas                                                                 |
|------------------------------------|--------------------------------------------------|--------------|--------------------------|-----------------------------------------------------------------------|
| `campaigns/id`                     | ID existente (para actualización)                | Texto        | `CAMP-001`               | Opcional. Si se omite, se crea nueva campaña.                         |
| `campaigns/campEstado`             | Estado de la campaña                             | Texto        | `Activa`                 | Opcional. Valor por defecto: `Activa`.                                |
| `articles/artNombre`               | Nombre del artículo                              | Texto        | `Agua 2L x6`             | Opcional. Recomendado para claridad.                                  |
| `clients/campNombre`               | Nombre de campaña (para cliente)                 | Texto        | `PROMO-2025-11`          | Opcional. Debe coincidir con `campaigns/campNombre` si se usa.         |
| `requirements/campNombre`          | Nombre de campaña (para requisito)               | Texto        | `PROMO-2025-11`          | Opcional. Solo si hay requisito.                                      |
| `requirements/artidRequisito`      | Artículo requerido                               | Texto        | `33-0-3-12`              | Opcional. Requerido si hay requisito.                                 |
| `requirements/cantidadRequisito`   | Cantidad requerida                               | Número       | `1`                      | Opcional. > 0 si se incluye.                                          |
| `requirements/cantidadMin`         | Cantidad mínima del requisito                    | Número       | `1`                      | Opcional. ≥ 0.                                                        |
| `requirements/cantidadMax`         | Cantidad máxima del requisito                    | Número       | `12`                     | Opcional. ≥ `cantidadMin` si se incluye.                              |
| `requirements/precioPromocional`   | Precio del artículo requerido                    | Número       | `45.00`                  | Opcional. ≥ 0.                                                        |

---

### Validaciones Clave

| Regla                                                   | Descripción                                                                 |
|---------------------------------------------------------|-----------------------------------------------------------------------------|
| `campNombre` único                                      | No se repite en ninguna fila.                                               |
| `articles/campNombre` = `campaigns/campNombre`          | Deben coincidir en la misma fila.                                           |
| Fechas válidas                                          | `campFechaFin ≥ campFechaInicio`.                                           |
| Cantidades                                              | `cantidadMax ≥ cantidadMin > 0`.                                            |
| Cliente requerido                                       | `cliId` y `cliNombre` obligatorios.                                         |
| Requisitos consistentes                                 | Si se incluye `artidRequisito`, también debe ir `cantidadRequisito`.        |
| `campPrioridad` válida                                  | Solo `Alta`, `Media`, `Baja`.                                               |

---

## 3. Formato de Fechas Aceptado

| Formato                     | Ejemplo             | Notas |
|-----------------------------|---------------------|-------|
| `DD/MM/YYYY`                | `01/11/2025`        | Recomendado. |
| `YYYY-MM-DD`                | `2025-11-01`        | Válido. |
| Serial Excel (número)       | `46306`             | Se convierte automáticamente. |

---

## 4. Ejemplo de Datos Válidos

```excel
campaigns/id | campaigns/campNombre | campaigns/campDescripcion | campaigns/campFechaInicio | campaigns/campFechaFin | campaigns/campPrioridad | campaigns/campEstado | campaigns/campTipo | articles/campNombre | articles/artid | articles/artNombre     | articles/cantidadMin | articles/cantidadMax | articles/precioPromocional | clients/campNombre | clients/cliId | clients/cliNombre      | requirements/campNombre | requirements/artidRequisito | requirements/cantidadRequisito | requirements/cantidadMin | requirements/cantidadMax | requirements/precioPromocional
-------------|----------------------|---------------------------|---------------------------|------------------------|-------------------------|----------------------|--------------------|---------------------|----------------|------------------------|----------------------|----------------------|----------------------------|--------------------|---------------|------------------------|-------------------------|-----------------------------|-------------------------------|--------------------------|--------------------------|-------------------------------
             | PROMO-2025-11        | Promo noviembre clientes  | 01/11/2025                | 30/11/2025             | Alta                    | Activa               | PorCliente         | PROMO-2025-11       | 61-0-11-6      | Agua 2L x6             | 6                    | 24                   | 19.50                      | PROMO-2025-11      | CLI-1001      | Supermercado Central   | PROMO-2025-11           | 33-0-3-12                   | 1                             | 1                        | 12                       | 45.00
             | PROMO-2025-11        | Promo noviembre clientes  | 01/11/2025                | 30/11/2025             | Alta                    | Activa               | PorCliente         | PROMO-2025-11       | 61-0-11-7      | Gaseosa 3L x6          | 4                    | 12                   | 28.00                      | PROMO-2025-11      | CLI-1002      | Tienda Doña María      |                         |                             |                               |                          |                          | 
```

---

## 5. Errores Comunes y Soluciones

| Error                                                      | Causa                                                                 | Solución                                                                 |
|------------------------------------------------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------------|
| `Falta hoja: CampañaPorCliente`                            | Hoja con nombre incorrecto.                                           | Renombra a `CampañaPorCliente`.                                          |
| `Faltan columnas requeridas`                               | Falta alguna columna obligatoria.                                     | Verifica nombres exactos (con `/`).                                      |
| `campNombre duplicado`                                     | Mismo nombre en varias filas.                                         | Usa nombres únicos.                                                      |
| `campFechaFin anterior a campFechaInicio`                  | Fecha de fin menor que inicio.                                        | Corrige las fechas.                                                      |
| `cantidadMax < cantidadMin`                                | Cantidad máxima menor que mínima.                                     | Asegúrate de que `max ≥ min`.                                            |
| `cliId es obligatorio`                                     | Cliente sin ID.                                                       | Completa `cliId` y `cliNombre`.                                          |
| `artidRequisito sin cantidadRequisito`                     | Requisito incompleto.                                                 | Incluye ambos o elimina el requisito.                                    |
| `campPrioridad debe ser Alta, Media o Baja`                | Valor no permitido.                                                   | Usa solo los 3 valores permitidos.                                       |

---

## 6. Pasos para Cargar

1. **Crear archivo Excel**:
   - Hoja: `CampañaPorCliente`
   - Copia las columnas con nombres **exactos**.
2. **Completar datos**:
   - Respeta tipos y formatos.
   - Usa mismo `campNombre` en campaña, artículo y cliente.
3. **Subir archivo**:
   - Usa función de carga masiva.
4. **Revisar resultado**:
   - `isValid: true` → datos listos.
   - `isValid: false` → corrige errores listados.

---

## 7. Plantilla para Copiar (Excel)

```excel
campaigns/id	campaigns/campNombre	campaigns/campDescripcion	campaigns/campFechaInicio	campaigns/campFechaFin	campaigns/campPrioridad	campaigns/campEstado	campaigns/campTipo	articles/campNombre	articles/artid	articles/artNombre	articles/cantidadMin	articles/cantidadMax	articles/precioPromocional	clients/campNombre	clients/cliId	clients/cliNombre	requirements/campNombre	requirements/artidRequisito	requirements/cantidadRequisito	requirements/cantidadMin	requirements/cantidadMax	requirements/precioPromocional
	PROMO-2025-11	Promoción noviembre clientes	01/11/2025	30/11/2025	Alta	Activa	PorCliente	PROMO-2025-11	61-0-11-6	Agua 2L x6	6	24	19.50	PROMO-2025-11	CLI-1001	Supermercado Central	PROMO-2025-11	33-0-3-12	1	1	12	45.00
```

> **Copia esta fila como plantilla base.**

---

## 8. Notas Técnicas

- **Transformación automática**:
  - Fechas → `Date` objeto.
  - Números → `number`.
  - Campos opcionales ausentes → `undefined`.
- **Resultado de validación**:
  ```ts
  {
    isValid: boolean;
    errors: ValidationError[];
    data: CampaignClientData[];
    rowCount: number;
  }
  ```
