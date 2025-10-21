# Estructura del Archivo Excel para Carga Masiva

## 1. Estructura General del Archivo Excel

- **Formato del archivo**: El archivo debe ser un Excel legible por la librería XLSX (formatos compatibles: `.xlsx`, `.xls`).
- **Hojas requeridas**:
  - **CabeceraPorLista**: Contiene la información general de las campañas.
  - **DetallePorLista**: Contiene los detalles de los artículos, listas de precios y requisitos asociados a las campañas.
- **Codificación de datos**:
  - Los campos de texto no deben contener espacios en blanco al inicio o al final.
  - Las fechas deben estar en un formato reconocible (ver sección de fechas).
  - Los números deben ser valores válidos (sin caracteres no numéricos, salvo en casos específicos).
- **Validaciones**:
  - El validador revisará que todas las columnas requeridas estén presentes.
  - Se asegurará de que los datos sean consistentes entre las hojas y cumplan con las reglas definidas.

---

## 2. Estructura de la Hoja `CabeceraPorLista`

Esta hoja contiene la información general de las campañas. Debe incluir las siguientes columnas requeridas:

| Columna                       | Descripción                              | Tipo de dato    | Ejemplo                       | Notas                                                                 |
|-------------------------------|------------------------------------------|-----------------|-------------------------------|----------------------------------------------------------------------|
| `campaigns/id`                | Identificador de la campaña (opcional)   | Texto/Número    | `0` o `CAMP-001`             | Puede estar vacío si es una nueva campaña.                            |
| `campaigns/campNombre`        | Nombre único de la campaña              | Texto           | `CAMP-000`                   | Requerido. Debe ser único en la hoja. No se permite vacío.            |
| `campaigns/campDescripcion`   | Descripción de la campaña               | Texto           | `Para compras al por mayor 2025` | Requerido. Puede ser vacío, pero se recomienda incluir una descripción. |
| `campaigns/campFechaInicio`   | Fecha de inicio de la campaña           | Fecha           | `2025-11-10 13:49:45.150` o `10/11/2025` | Requerido. Formato ISO o DD/MM/YYYY.                     |
| `campaigns/campFechaFin`      | Fecha de fin de la campaña              | Fecha           | `2026-01-25 13:49:45.150` o `25/01/2026` | Requerido. Debe ser posterior o igual a la fecha de inicio. |
| `campaigns/campPrioridad`     | Prioridad de la campaña                 | Texto           | `Alta`, `Media`, `Baja`      | Requerido. Solo se aceptan estos valores.                            |
| `campaigns/campTipo`          | Tipo de campaña                         | Texto           | `PorLista`                   | Requerido. Generalmente debe ser `PorLista`.                         |

### Validaciones de la Hoja `CabeceraPorLista`
- **Nombre de campaña (`campNombre`)**: No puede estar vacío ni repetirse en la hoja.
- **Fechas**:
  - Deben ser válidas (formato ISO `YYYY-MM-DD HH:mm:ss.SSS` o `DD/MM/YYYY`).
  - La fecha de inicio no puede ser posterior a la fecha de fin.
- **Prioridad**: Solo se aceptan los valores `Alta`, `Media`, `Baja`.
- **Columnas faltantes**: Si alguna columna requerida no está presente, el validador devolverá un error.

### Ejemplo de Datos Válidos para `CabeceraPorLista`

```excel
campaigns/id | campaigns/campNombre | campaigns/campDescripcion                | campaigns/campFechaInicio | campaigns/campFechaFin | campaigns/campPrioridad | campaigns/campTipo
-------------|---------------------|------------------------------------------|---------------------------|------------------------|-------------------------|-------------------
0            | CAMP-000            | Para compras al por mayor 2025           | 2025-11-10 13:49:45.150   | 2026-01-25 13:49:45.150 | Alta                    | PorLista
0            | CAMP-001            | Descuentos especiales fin de año 2025    | 2025-11-05                | 2026-01-13              | Alta                    | PorLista
```

---

## 3. Estructura de la Hoja `DetallePorLista`

Esta hoja contiene los detalles de los artículos, listas de precios y requisitos asociados a las campañas definidas en `CabeceraPorLista`. Incluye las siguientes columnas:

### Columnas Requeridas

| Columna                       | Descripción                                      | Tipo de dato | Ejemplo            | Notas                                                                 |
|-------------------------------|--------------------------------------------------|--------------|--------------------|----------------------------------------------------------------------|
| `articles/CampNombre`         | Nombre de la campaña                             | Texto        | `CAMP-000`         | Requerido. Debe existir en la hoja `CabeceraPorLista`.                |
| `articles/artid`              | Identificador del artículo                       | Texto        | `33-0-3-12`        | Requerido. No puede estar vacío.                                     |
| `articles/artNombre`          | Nombre del artículo                              | Texto        | `Producto A`       | Requerido. Puede estar vacío, pero se recomienda incluir un nombre.   |
| `articles/cantidadMin`        | Cantidad mínima del artículo                    | Número       | `1`                | Requerido. Debe ser mayor a 0.                                       |
| `articles/cantidadMax`        | Cantidad máxima del artículo                    | Número       | `13`               | Requerido. Debe ser mayor o igual a `cantidadMin`.                   |
| `articles/precioPromocional`  | Precio promocional del artículo                 | Número       | `3247.20`          | Requerido. No puede ser negativo.                                    |

### Columnas Opcionales

| Columna                           | Descripción                                      | Tipo de dato | Ejemplo            | Notas                                                                 |
|-----------------------------------|--------------------------------------------------|--------------|--------------------|----------------------------------------------------------------------|
| `ListaPrecio/CampNombre`          | Nombre de la campaña para la lista de precios    | Texto        | `CAMP-000`         | Debe coincidir con `articles/CampNombre` si se incluye.               |
| `ListaPrecio/LisId`               | Identificador de la lista de precios            | Número       | `3`                | Requerido si se incluye `ListaPrecio`.                               |
| `ListaPrecio/LisNombre`           | Nombre de la lista de precios                   | Texto        | `EMAPA`            | Requerido si se incluye `ListaPrecio`.                               |
| `requirements/CampNombre`         | Nombre de la campaña para requisitos            | Texto        | `CAMP-000`         | Debe coincidir con `articles/CampNombre` si se incluye.               |
| `requirements/artidRequisito`     | Identificador del artículo requerido            | Texto        | `33-0-3-12`        | Requerido si se incluyen requisitos.                                  |
| `requirements/cantidadRequisito`  | Cantidad requerida del artículo                 | Número       | `1`                | Requerido si se incluyen requisitos. Debe ser mayor a 0.              |
| `requirements/cantidadMin`        | Cantidad mínima del artículo requerido          | Número       | `1`                | Opcional. Si se incluye, debe ser válido.                            |
| `requirements/cantidadMax`        | Cantidad máxima del artículo requerido          | Número       | `13`               | Opcional. Debe ser mayor o igual a `cantidadMin` si se incluye.      |
| `requirements/precioPromocional`  | Precio promocional del artículo requerido       | Número       | `3247.20`          | Opcional. No puede ser negativo si se incluye.                       |

### Validaciones de la Hoja `DetallePorLista`
- **Consistencia de `CampNombre`**:
  - El valor de `articles/CampNombre` debe existir en la hoja `CabeceraPorLista`.
  - Si se incluyen `ListaPrecio/CampNombre` o `requirements/CampNombre`, deben coincidir con `articles/CampNombre`.
- **Artículos**:
  - `artid` no puede estar vacío.
  - `cantidadMin` debe ser mayor a 0.
  - `cantidadMax` debe ser mayor o igual a `cantidadMin`.
  - `precioPromocional` no puede ser negativo.
- **Lista de Precios (si se incluye)**:
  - `LisId` y `LisNombre` son requeridos si se define alguna columna de `ListaPrecio`.
- **Requisitos (si se incluyen)**:
  - `artidRequisito` y `cantidadRequisito` son requeridos.
  - `cantidadRequisito` debe ser mayor a 0.
  - Si se incluyen `cantidadMin` y `cantidadMax`, `cantidadMax` debe ser mayor o igual a `cantidadMin`.
  - `precioPromocional` no puede ser negativo si se incluye.
- **Columnas faltantes**: Si alguna columna requerida no está presente, el validador devolverá un error.

### Ejemplo de Datos Válidos para `DetallePorLista`

```excel
articles/CampNombre | articles/artid | articles/artNombre | articles/cantidadMin | articles/cantidadMax | articles/precioPromocional | ListaPrecio/CampNombre | ListaPrecio/LisId | ListaPrecio/LisNombre | requirements/CampNombre | requirements/artidRequisito | requirements/cantidadRequisito | requirements/cantidadMin | requirements/cantidadMax | requirements/precioPromocional
--------------------|----------------|--------------------|----------------------|----------------------|----------------------------|------------------------|-------------------|-----------------------|-------------------------|-----------------------------|-------------------------------|-------------------------|-------------------------|-------------------------------
CAMP-000            | 33-0-3-12      | Producto A         | 1                    | 13                   | 3247.20                    | CAMP-000               | 3                 | EMAPA                 | CAMP-000                | 33-0-3-12                   | 1                             | 1                       | 13                      | 3247.20
CAMP-001            | AM-CB12X530-620| Producto B         | 1                    | 27                   | 2957400.00                 | CAMP-001               | 43                | PROVINCIA - COMPRA    | CAMP-001                | AM-CB12X530-620             | 9                             | 1                       | 27                      | 2957400.00
```

---

## 4. Formato de Fechas

El validador acepta fechas en los siguientes formatos:
- **Formato ISO**: `YYYY-MM-DD HH:mm:ss.SSS` (ejemplo: `2025-11-10 13:49:45.150`).
- **Formato DD/MM/YYYY**: `DD/MM/YYYY` (ejemplo: `10/11/2025`).
- **Formato serial de Excel**: Si el valor es un número, el validador lo convierte automáticamente a una fecha (basado en el sistema de fechas de Excel, donde `1` equivale a `01/01/1900`).

### Recomendaciones para Fechas
- Usa el formato ISO para evitar ambigüedades.
- Asegúrate de que las fechas sean válidas y que la fecha de inicio no sea posterior a la fecha de fin.
- Si usas el formato `DD/MM/YYYY`, verifica que el día, mes y año sean correctos.

---

## 5. Errores Comunes y Cómo Evitarlos

El validador puede devolver errores si el archivo no cumple con las reglas. A continuación, se detallan los errores comunes y cómo prevenirlos:

| Error                                              | Causa                                                                 | Solución                                                                 |
|----------------------------------------------------|----------------------------------------------------------------------|-------------------------------------------------------------------------|
| Faltan hojas requeridas                            | El archivo no contiene las hojas `CabeceraPorLista` o `DetallePorLista`. | Asegúrate de que el archivo tenga ambas hojas con los nombres exactos.   |
| Faltan columnas requeridas en `CabeceraPorLista`    | Falta alguna columna requerida en `CabeceraPorLista`.                | Verifica que todas las columnas requeridas estén presentes y con nombres exactos. |
| Faltan columnas requeridas en `DetallePorLista`     | Falta alguna columna requerida en `DetallePorLista`.                 | Verifica que todas las columnas requeridas estén presentes y con nombres exactos. |
| Nombre de campaña requerido en `CabeceraPorLista` fila X | El campo `campNombre` está vacío.                                   | Asegúrate de que todas las filas en `CabeceraPorLista` tengan un `campNombre` único. |
| Nombre de campaña duplicado en `CabeceraPorLista`  | Hay nombres de campaña repetidos.                                    | Cada `campNombre` en `CabeceraPorLista` debe ser único.                 |
| Campaña "X" no definida en la hoja `CabeceraPorLista` | El `articles/CampNombre` en `DetallePorLista` no existe en `CabeceraPorLista`. | Asegúrate de que cada `CampNombre` en `DetallePorLista` coincida con uno en `CabeceraPorLista`. |
| Fecha de inicio no puede ser posterior a fecha de fin | La fecha de inicio es posterior a la fecha de fin.                 | Verifica que `campFechaInicio` sea anterior o igual a `campFechaFin`.   |
| Prioridad debe ser: `Alta`, `Media`, `Baja`        | El valor de `campPrioridad` no es válido.                            | Usa solo `Alta`, `Media` o `Baja` en `campaigns/campPrioridad`.        |
| Cantidad mínima debe ser mayor a 0                 | `cantidadMin` es 0 o negativo.                                      | Asegúrate de que `articles/cantidadMin` y `requirements/cantidadMin` sean mayores a 0. |
| Cantidad máxima debe ser mayor o igual a cantidad mínima | `cantidadMax` es menor que `cantidadMin`.                     | Asegúrate de que `articles/cantidadMax` ≥ `articles/cantidadMin` y lo mismo para `requirements`. |
| Precio promocional no puede ser negativo           | `precioPromocional` es negativo.                                    | Usa valores no negativos para `articles/precioPromocional` y `requirements/precioPromocional`. |
| El nombre de campaña en `ListaPrecio` debe coincidir | `ListaPrecio/CampNombre` no coincide con `articles/CampNombre`.     | Asegúrate de que todos los `CampNombre` en una fila sean idénticos.     |

---

## 6. Pasos para Cargar el Archivo

1. **Preparar el archivo Excel**:
   - Crea un archivo Excel con dos hojas: `CabeceraPorLista` y `DetallePorLista`.
   - Asegúrate de que las columnas tengan los nombres exactos especificados (respetando mayúsculas y barras `/`).
   - Completa los datos siguiendo las reglas de las secciones anteriores.
   - Verifica que las fechas estén en un formato válido y que los valores numéricos sean correctos.
2. **Cargar el archivo**:
   - Usa la interfaz o sistema donde se implementa el validador.
   - Selecciona el archivo Excel y súbelo.
   - El sistema ejecutará el validador (`validateCampaignListExcel`) para verificar el archivo.
3. **Revisar los resultados**:
   - Si el archivo es válido (`isValid: true`), los datos procesados estarán disponibles en el campo `data` del resultado.
   - Si hay errores (`isValid: false`), revisa el campo `errors` para identificar los problemas (indicará la fila, columna y mensaje de error).
   - Corrige los errores en el Excel y vuelve a cargar el archivo.

---

## 7. Ejemplo Completo de Archivo Excel

### Hoja: `CabeceraPorLista`

```excel
campaigns/id | campaigns/campNombre | campaigns/campDescripcion                | campaigns/campFechaInicio | campaigns/campFechaFin | campaigns/campPrioridad | campaigns/campTipo
-------------|---------------------|------------------------------------------|---------------------------|------------------------|-------------------------|-------------------
0            | CAMP-000            | Para compras al por mayor 2025           | 2025-11-10                | 2026-01-25             | Alta                    | PorLista
0            | CAMP-001            | Descuentos especiales fin de año 2025    | 2025-11-05                | 2026-01-13             | Alta                    | PorLista
```

### Hoja: `DetallePorLista`

```excel
articles/CampNombre | articles/artid | articles/artNombre | articles/cantidadMin | articles/cantidadMax | articles/precioPromocional | ListaPrecio/CampNombre | ListaPrecio/LisId | ListaPrecio/LisNombre | requirements/CampNombre | requirements/artidRequisito | requirements/cantidadRequisito | requirements/cantidadMin | requirements/cantidadMax | requirements/precioPromocional
--------------------|----------------|--------------------|----------------------|----------------------|----------------------------|------------------------|-------------------|-----------------------|-------------------------|-----------------------------|-------------------------------|-------------------------|-------------------------|-------------------------------
CAMP-000            | 33-0-3-12      | Producto A         | 1                    | 13                   | 3247.20                    | CAMP-000               | 3                 | EMAPA                 | CAMP-000                | 33-0-3-12                   | 1                             | 1                       | 13                      | 3247.20
CAMP-001            | AM-CB12X530-620| Producto B         | 1                    | 27                   | 2957400.00                 | CAMP-001               | 43                | PROVINCIA - COMPRA    | CAMP-001                | AM-CB12X530-620             | 9                             | 1                       | 27                      | 2957400.00
```

---

## 8. Notas Adicionales

- **Nombres de columnas**: Los nombres deben ser exactos, incluyendo las barras (`/`). Por ejemplo, `campaigns/campNombre` no debe escribirse como `campaigns_campNombre` o `CampNombre`.
- **Validación automática**: El validador revisará automáticamente la consistencia entre las hojas y la validez de los datos. No es necesario realizar validaciones manuales adicionales.
- **Transformación de datos**: Si el archivo pasa la validación, los datos se transformarán automáticamente al formato requerido por el backend usando la función `transformCampaignListForBackend`.
- **Errores detallados**: Los errores devueltos incluyen la fila, el campo y un mensaje específico, lo que facilita la corrección.

---

## 9. Solución de Problemas

- **El archivo no se carga**: Verifica que el archivo sea un Excel válido (`.xlsx` o `.xls`) y que no esté corrupto.
- **Errores de formato de fecha**: Usa el formato ISO (`YYYY-MM-DD HH:mm:ss.SSS`) para evitar problemas de interpretación.
- **Errores de columnas faltantes**: Compara los nombres de las columnas con las listas de columnas requeridas proporcionadas.
- **Errores de datos inconsistentes**: Asegúrate de que los valores de `CampNombre` sean consistentes entre las secciones `articles`, `ListaPrecio` y `requirements`.
