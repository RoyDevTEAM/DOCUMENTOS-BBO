```markdown
# Estructura del Archivo Excel para Carga Masiva de Lista de Precios por Artículo

## 1. Estructura General del Archivo Excel

- **Formato del archivo**: Debe ser un archivo Excel compatible con la librería `xlsx` (`.xlsx` o `.xls`).
- **Hoja requerida**:
  - **`ListaPrecioArticulo`**: Contiene todos los datos de precios por artículo y lista.
- **Codificación de datos**:
  - Los textos no deben tener espacios al inicio ni al final.
  - Las fechas deben estar en formato reconocible (ver sección de fechas).
  - Los valores numéricos deben ser válidos (sin letras ni símbolos, salvo decimales con `.`).
- **Validaciones**:
  - Se verifica la presencia de la hoja y columnas obligatorias.
  - Se validan tipos de datos, obligatoriedad y formato de fechas.
  - Se devuelve un resultado detallado con errores por fila y campo.

---

## 2. Estructura de la Hoja `ListaPrecioArticulo`

Esta hoja contiene los precios de artículos asociados a listas de precios con vigencia. Incluye **columnas requeridas** y **opcionales**.

### Columnas Requeridas

| Columna                                  | Descripción                                      | Tipo de dato | Ejemplo              | Notas                                                                 |
|------------------------------------------|--------------------------------------------------|--------------|----------------------|-----------------------------------------------------------------------|
| `ListaPrecioArticulo/artId`              | Código del artículo                              | Texto        | `61-0-11-6`          | **Requerido**. No puede estar vacío.                                  |
| `ListaPrecioArticulo/lisId`              | ID de la lista de precios                        | Número       | `202`                | **Requerido**. Debe ser un número entero.                             |
| `ListaPrecioArticulo/lpaFechaInicio`     | Fecha de inicio de vigencia del precio           | Fecha        | `29/10/2025`         | **Requerido**. Formato `DD/MM/YYYY`, ISO o serial Excel.              |
| `ListaPrecioArticulo/lpaFechaTermino`    | Fecha de fin de vigencia del precio              | Fecha        | `29/12/2025`         | **Requerido**. Debe ser igual o posterior a `lpaFechaInicio`.         |

### Columnas Opcionales

| Columna                                  | Descripción                                      | Tipo de dato | Ejemplo              | Notas                                                                 |
|------------------------------------------|--------------------------------------------------|--------------|----------------------|-----------------------------------------------------------------------|
| `ListaPrecioArticulo/ttxId`              | ID del tipo de transacción                       | Número       | `14`                 | Opcional. Si se incluye, debe ser un número.                          |
| `ListaPrecioArticulo/artNombre`          | Nombre del artículo                              | Texto        | `AGUA CON GAS 2 LITROS OW- X 6` | Opcional. Se recomienda incluir para claridad.              |
| `ListaPrecioArticulo/lpaPrecioBs`        | Precio en efectivo (Bs)                          | Número       | `22.00`              | Opcional. Debe ser positivo si se incluye.                            |
| `ListaPrecioArticulo/lpaPrecioCreditoBs` | Precio a crédito (Bs)                            | Número       | `22.00`              | Opcional. Debe ser positivo si se incluye.                            |
| `ListaPrecioArticulo/lisNombre`          | Nombre de la lista de precios                    | Texto        | `EVENTUAL 2`         | Opcional. Útil para auditoría.                                        |
| `ListaPrecioArticulo/lpaIceContado`      | ICE para pago al contado                         | Número       | `0`                  | Opcional. Valor por defecto: 0.                                       |
| `ListaPrecioArticulo/lpaIceCredito`      | ICE para pago a crédito                          | Número       | `0`                  | Opcional. Valor por defecto: 0.                                       |
| `ListaPrecioArticulo/lpaPrecioMin`       | Precio mínimo permitido                          | Número       | `20.00`              | Opcional. Valor por defecto: 0.                                       |
| `ListaPrecioArticulo/lpaPrecioMax`       | Precio máximo permitido                          | Número       | `25.00`              | Opcional. Valor por defecto: 0.                                       |

---

### Validaciones de la Hoja `ListaPrecioArticulo`

- **Hoja y columnas**:
  - La hoja debe llamarse exactamente `ListaPrecioArticulo`.
  - Las 4 columnas requeridas deben estar presentes con nombres **exactos** (incluyendo `/`).
- **Datos por fila**:
  - `artId`: No puede estar vacío ni contener solo espacios.
  - `lisId`: Debe ser un número entero válido.
  - `lpaFechaInicio` y `lpaFechaTermino`: Deben ser fechas válidas y `lpaFechaTermino ≥ lpaFechaInicio`.
  - Campos numéricos opcionales: Si se incluyen, deben ser números válidos (no negativos en precios).
- **Errores devueltos**:
  - Incluyen: `row` (número de fila), `field` (columna), `message` (descripción clara).

---

## 3. Formato de Fechas Aceptado

El validador acepta los siguientes formatos de fecha:

| Formato                     | Ejemplo                  | Notas |
|-----------------------------|--------------------------|-------|
| `DD/MM/YYYY`                | `29/10/2025`             | Recomendado. Día y mes de 1 o 2 dígitos. |
| `YYYY-MM-DD` (ISO parcial)  | `2025-10-29`             | También válido. |
| Serial de Excel (número)    | `46334`                  | Se convierte automáticamente (base 1900). |

> **Recomendación**: Usa `DD/MM/YYYY` para evitar ambigüedades.

---

## 4. Ejemplo de Datos Válidos

```excel
ListaPrecioArticulo/artId | ListaPrecioArticulo/artNombre              | ListaPrecioArticulo/lpaPrecioBs | ListaPrecioArticulo/lpaPrecioCreditoBs | ListaPrecioArticulo/lisId | ListaPrecioArticulo/lisNombre | ListaPrecioArticulo/lpaFechaInicio | ListaPrecioArticulo/lpaFechaTermino
---------------------------|--------------------------------------------|---------------------------------|----------------------------------------|----------------------------|-------------------------------|------------------------------------|-------------------------------------
61-0-11-6                  | AGUA CON GAS 2 LITROS OW- X 6              | 22.00                           | 22.00                                  | 202                        | EVENTUAL 2                    | 29/10/2025                         | 29/12/2025
33-0-3-12                  | ACEITE DE OLIVA 1L                         | 45.50                           | 48.00                                  | 101                        | MAYORISTA                     | 01/11/2025                         | 31/01/2026
```

---

## 5. Errores Comunes y Soluciones

| Error                                                  | Causa                                                                 | Solución                                                                 |
|--------------------------------------------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------------|
| `Falta hoja: ListaPrecioArticulo`                      | El archivo no tiene la hoja con ese nombre exacto.                    | Renombra la hoja a `ListaPrecioArticulo`.                                |
| `Faltan columnas: ListaPrecioArticulo/artId, ...`      | Faltan una o más columnas requeridas.                                 | Asegúrate de incluir las 4 columnas obligatorias con nombres exactos.    |
| `ArtId es obligatorio` (fila X)                        | Celda `artId` vacía o con espacios.                                   | Completa un código válido (ej: `61-0-11-6`).                             |
| `lpaFechaInicio es obligatorio`                        | Fecha de inicio vacía.                                                | Ingresa una fecha en formato `DD/MM/YYYY`.                               |
| `lpaFechaTermino es obligatorio`                       | Fecha de fin vacía.                                                   | Ingresa una fecha posterior o igual a la de inicio.                      |
| Fecha no válida                                        | Formato incorrecto o fecha imposible (ej: 32/13/2025).                | Usa `DD/MM/YYYY` con valores válidos.                                    |
| `lisId` no es número                                   | Valor no numérico en `lisId`.                                         | Ingresa solo números enteros.                                            |

---

## 6. Pasos para Cargar el Archivo

1. **Crear el archivo Excel**:
   - Crea una hoja llamada **`ListaPrecioArticulo`**.
   - Agrega las columnas con nombres **exactos** (incluye `/`).
   - Completa los datos respetando tipos y formatos.
2. **Subir el archivo**:
   - Usa la función de carga masiva en la aplicación.
   - Selecciona el archivo `.xlsx`.
3. **Revisar resultado**:
   - Si `isValid: true` → los datos están listos para procesar.
   - Si `isValid: false` → revisa `errors[]` para corregir fila por fila.

---

## 7. Notas Importantes

- **Nombres de columnas**: Deben ser **idénticos** a los especificados (case-sensitive, con `/`).
- **Filas vacías**: Se ignoran si están completamente vacías.
- **Transformación automática**:
  - Las fechas se convierten a `YYYY-MM-DD`.
  - Los campos opcionales ausentes se envían como `undefined`.
  - Los campos `lpaIceContado`, `lpaIceCredito`, `lpaPrecioMin`, `lpaPrecioMax` se envían como `0` si no están presentes.
- **Función de validación**: `validateLitaPreciiArticulo(file)` → devuelve:
  ```ts
  {
    isValid: boolean;
    errors: ValidationErrorListaPrecio[];
    validData: ListaPrecioArticuloMasivaDto[];
    processedRows: number;
  }
  ```

---

## 8. Ejemplo de Plantilla (Copiar y Pegar)

```excel
ListaPrecioArticulo/artId	ListaPrecioArticulo/artNombre	ListaPrecioArticulo/lpaPrecioBs	ListaPrecioArticulo/lpaPrecioCreditoBs	ListaPrecioArticulo/lisId	ListaPrecioArticulo/lisNombre	ListaPrecioArticulo/lpaFechaInicio	ListaPrecioArticulo/lpaFechaTermino	ListaPrecioArticulo/ttxId	ListaPrecioArticulo/lpaIceContado	ListaPrecioArticulo/lpaIceCredito	ListaPrecioArticulo/lpaPrecioMin	ListaPrecioArticulo/lpaPrecioMax
61-0-11-6	AGUA CON GAS 2 LITROS OW- X 6	22.00	22.00	202	EVENTUAL 2	29/10/2025	29/12/2025	14	0	0	20.00	25.00
```

> **Descarga esta plantilla** y complétala con tus datos.

---

**Listo para usar en tu repositorio ETS.**
```

---

**Para descargar como archivo `.md`:**

1. Copia todo el contenido de arriba.
2. Pégalo en un editor de texto (como VS Code, Notepad++ o Bloc de notas).
3. Guárdalo como: `PLANTILLA_LISTA_PRECIO_ARTICULO.md`

O haz clic derecho en este enlace (si estás en un navegador compatible):

[Descargar Plantilla Markdown](data:text/plain;charset=utf-8,{{URL_ENCODED_CONTENT}})

*(Nota: Si necesitas el enlace real para descargar, puedo generarte un gist o base64, pero aquí tienes el contenido 100% listo.)*
