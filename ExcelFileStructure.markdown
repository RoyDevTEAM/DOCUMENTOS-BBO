# Estructura del Archivo Excel para Carga Masiva de Campañas por Lista (Actualizado 2025)

## 1. Estructura General del Archivo Excel

- **Formato del archivo**: Excel compatible con `XLSX` (`.xlsx` o `.xls`).
- **Hojas requeridas**:
  - **`CabeceraPorLista`**: Información general de cada campaña.
  - **`DetallePorLista`**: Detalles de artículos, listas de precios y requisitos.

- **Codificación de datos**:
  - Texto sin espacios al inicio/final.
  - Fechas: `DD/MM/YYYY`, `YYYY-MM-DD` o número serial Excel.
  - Números: solo dígitos y punto decimal (ej: `19.50`).
  - `campAgrupa`: `Sí`, `Si`, `S`, `1`, `No`, `N`, `0` (no case-sensitive).

- **Validaciones clave**:
  - Columnas exactas (con `/`).
  - Consistencia entre hojas.
  - **NUEVO**: Prioridad ampliada a 5 niveles.
  - **NUEVO**: `campAgrupa` obligatorio (Sí/No).
  - **NUEVO**: No se permite el mismo artículo en múltiples campañas con la misma prioridad.
  - **ELIMINADO**: `campaigns/id` (siempre se crean campañas nuevas).

---

## 2. Hoja `CabeceraPorLista`

### Columnas Requeridas

| Columna                        | Descripción                          | Tipo     | Ejemplo            | Notas |
|--------------------------------|--------------------------------------|----------|--------------------|-------|
| `campaigns/campNombre`         | Nombre único de campaña              | Texto    | `CAMP-NOV2025`     | Único en toda la hoja |
| `campaigns/campDescripcion`    | Descripción                          | Texto    | `Promo noviembre`  | |
| `campaigns/campFechaInicio`    | Fecha inicio                         | Fecha    | `01/11/2025`       | DD/MM/YYYY |
| `campaigns/campFechaFin`       | Fecha fin                            | Fecha    | `30/11/2025`       | ≥ inicio |
| `campaigns/campPrioridad`      | Prioridad                            | Texto    | `Alta`             | **Valores válidos**: `Muy Alta`, `Alta`, `Media Alta`, `Media`, `Baja` |
| `campaigns/campTipo`           | Tipo                                 | Texto    | `PorLista`         | |
| `campaigns/campAgrupa`         | ¿Agrupa artículos?                   | Sí/No    | `Sí`               | Acepta: Sí, Si, S, 1, No, N, 0 |

### Validaciones

- `campNombre` no vacío ni duplicado.
- Fechas válidas y `inicio ≤ fin`.
- Prioridad exacta (5 opciones).
- `campAgrupa` formato correcto.

### Ejemplo

```excel
campaigns/campNombre | campaigns/campDescripcion | campaigns/campFechaInicio | campaigns/campFechaFin | campaigns/campPrioridad | campaigns/campTipo | campaigns/campAgrupa
---------------------|---------------------------|---------------------------|------------------------|-------------------------|--------------------|---------------------
CAMP-NOV2025         | Promo noviembre           | 01/11/2025                | 30/11/2025             | Alta                    | PorLista           | Sí
CAMP-DIC2025         | Fin de año                | 01/12/2025                | 31/12/2025             | Media                   | PorLista           | No
```

---

## 3. Hoja `DetallePorLista`

### Columnas Requeridas

| Columna                        | Descripción                          | Tipo     | Ejemplo       |
|--------------------------------|--------------------------------------|----------|---------------|
| `articles/CampNombre`          | Nombre campaña (igual que cabecera)  | Texto    | `CAMP-NOV2025`|
| `articles/artid`               | Código artículo                      | Texto    | `61-0-11-6`   |
| `articles/artNombre`           | Nombre artículo                      | Texto    | `Agua 2L x6`  |
| `articles/cantidadMin`         | Cantidad mínima                      | Número   | `6`           |
| `articles/cantidadMax`         | Cantidad máxima                      | Número   | `24`          |
| `articles/precioPromocional`   | Precio promo                         | Número   | `19.50`       |

### Columnas Opcionales

| Columna                            | Descripción                          | Tipo     | Ejemplo       |
|------------------------------------|--------------------------------------|----------|---------------|
| `ListaPrecio/LisId`                | ID lista precios                     | Número   | `202`         |
| `ListaPrecio/LisNombre`            | Nombre lista                         | Texto    | `EVENTUAL 2`  |
| `requirements/artidRequisito`      | Artículo requerido                   | Texto    | `33-0-3-12`   |
| `requirements/cantidadRequisito`   | Cantidad requerida                   | Número   | `1`           |
| `requirements/cantidadMin`         | Mínimo requisito                     | Número   | `1`           |
| `requirements/cantidadMax`         | Máximo requisito                     | Número   | `12`          |
| `requirements/precioPromocional`   | Precio requisito                     | Número   | `45.00`       |

### Validaciones

- `articles/CampNombre` debe existir en `CabeceraPorLista`.
- `cantidadMin > 0`, `cantidadMax ≥ cantidadMin`.
- Si hay `ListaPrecio/LisNombre` → `LisId` obligatorio.
- Si hay `artidRequisito` → no puede ser igual a `artid` principal.
- **GLOBAL**: Mismo artículo (principal o requisito) no puede repetirse en campañas con misma prioridad.

---

## 4. Formato de Fechas

| Formato            | Ejemplo       |
|--------------------|---------------|
| `DD/MM/YYYY`       | `01/11/2025`  |
| `YYYY-MM-DD`       | `2025-11-01`  |
| Serial Excel       | `46306`       |

> Usa `DD/MM/YYYY` → sin errores.

---

## 5. Errores Comunes (Actualizados)

| Error | Causa | Solución |
|------|-------|----------|
| `Faltan hojas` | Nombres mal escritos | Usa exactamente `CabeceraPorLista` y `DetallePorLista` |
| `campNombre duplicado` | Mismo nombre | Cambia nombre |
| `Prioridad debe ser: Muy Alta, Alta...` | Valor viejo | Usa los 5 nuevos |
| `campAgrupa debe ser: Sí, Si, S...` | Valor raro | Usa Sí/No |
| `Producto X en múltiples campañas con prioridad "Alta"` | Artículo repetido | Cambia prioridad o elimina |
| `No se permite el mismo artículo como principal y requisito` | artid = artidRequisito | Usa otro artículo |

---

## 6. Pasos para Cargar

1. Crea Excel con **2 hojas** exactas.
2. Copia columnas con `/`.
3. Rellena datos.
4. Sube → sistema valida con `validateCampaignListExcel`.
5. Si `isValid: true` → listo.
6. Si hay errores → corrige fila indicada.

---

## 7. Plantilla Lista para Copiar

### CabeceraPorLista
```excel
campaigns/campNombre	campaigns/campDescripcion	campaigns/campFechaInicio	campaigns/campFechaFin	campaigns/campPrioridad	campaigns/campTipo	campaigns/campAgrupa
CAMP-NOV2025	Promo noviembre	01/11/2025	30/11/2025	Alta	PorLista	Sí
```

### DetallePorLista
```excel
articles/CampNombre	articles/artid	articles/artNombre	articles/cantidadMin	articles/cantidadMax	articles/precioPromocional	ListaPrecio/LisId	ListaPrecio/LisNombre	requirements/artidRequisito	requirements/cantidadRequisito	requirements/cantidadMin	requirements/cantidadMax	requirements/precioPromocional
CAMP-NOV2025	61-0-11-6	Agua 2L x6	6	24	19.50	202	EVENTUAL 2	33-0-3-12	1	1	12	45.00
```

---

## 8. Notas Técnicas (2025)

- `campaigns/id` eliminado → siempre nuevas campañas.
- `campAgrupa` → `true/false` al backend.
- Prioridad: 5 niveles.
- Validación global de duplicados por prioridad.
- Función: `validateCampaignListExcel(file)`
- Transform: `transformCampaignListForBackend(data)`

