# Módulo de Preventa y Validación

Este documento describe la arquitectura, entidades clave, flujos y endpoints del módulo de Preventa y Validación. Incluye diagramas Mermaid para una visión técnica detallada y profesional.

## Resumen
- Objetivo: asegurar reglas de negocio de preventa (listas de precios, báuchers, campañas, aprobaciones y verificaciones) y exponer endpoints consistentes para validaciones.
- Capas: API (controllers), Application (commands/queries/handlers), Infrastructure (repositories/DbContext), Domain (entities), Shared (wrappers/responses).

## Arquitectura
```mermaid
graph TD
  A[API: PreventaController] -->|MediatR| B[Application: Commands/Queries]
  B --> C[Handlers]
  C --> D[Infrastructure: IPreventaValidacionRepository]
  D --> E[AppDbContext]
  E --> F[Domain: Entidades]

  subgraph API
    A
  end
  subgraph Application
    B
    C
  end
  subgraph Infrastructure
    D
    E
  end
  subgraph Domain
    F
  end
```

## Entidades Clave (ER)
```mermaid
erDiagram
  VdtTransaccionTxn ||--o{ VdtPedidoTransaccionDetalleTxn : contiene
  VntListaPrecio ||--o{ VntListaPrecioArticulo : define
  VdtConfigBaucher ||--o{ VdtConfigBaucherDetalle : detalla
  VdtPedidoTransaccionDetalleTxn ||--o{ VdtDetallePedidoBaucher : vincula
  VdtPedidoTransaccionDetalleTxn ||--o{ AuditoriaPedidoDetalle : audita
  VntListaPrecio ||--o{ VdtConfigCliente : asigna

  VdtTransaccionTxn {
    long TraId
    int TtxId
    long PedId
    string CliId
    datetime TraFechaTxn
  }

  VdtPedidoTransaccionDetalleTxn {
    long DtrId
    string ArtId
    long TraId
    long LpaId
    long CbIdBase
    long CbIdPorcentual
    decimal DtrCantidad
  }

  VntListaPrecio {
    long LisId
    string LisNombre
    string LpEstado
  }

  VntListaPrecioArticulo {
    long LpaId
    long LisId
    string ArtId
    int TtxId
    datetime LpaFechaInicio
    datetime LpaFechaTermino
  }

  VdtConfigBaucher {
    long CbId
    int CbEsBoucher
    int MarId
    int CalId
    string CbUnidadMinima
    datetime CbFechaInicio
    datetime CbFechaFinal
  }

  VdtConfigBaucherDetalle {
    long CbdId
    long CbId
    string CbdIdTipo
  }

  VdtDetallePedidoBaucher {
    long Id
    long IdPedido
    long IdDetalle
    long IdBaucher
  }

  AuditoriaPedidoDetalle {
    long AudId
    long DtrId_Original
    long LpaId_Original
    long CbIdBase_Original
    long CbIdPorcentual_Original
    long DtrId_Nuevo
    long LpaId_Nuevo
    long CbIdBase_Nuevo
    long CbIdPorcentual_Nuevo
    datetime AudFecha
  }

  VdtConfigCliente {
    string CliId
    long LisId
    string CliEstado
  }
```

## Flujos Principales

### Aplicar Lista de Precios y Báucher a Pedido
```mermaid
sequenceDiagram
  participant API as API
  participant HDR as AplicarListaPrecioPedidoCommandHandler
  participant REP as IPreventaValidacionRepository
  participant DB as AppDbContext

  API->>HDR: POST /api/Preventa/validaciones/pedidos/{pedId}/aplicar-lista-precio
  HDR->>REP: AplicarListaPrecioYBaucherAsync(pedId)
  REP->>DB: Query Transacción/Detalle/Cliente por pedId
  REP->>DB: Buscar LpaId en VntListaPrecioArticulos
  REP->>DB: Buscar CbIdBase/Porcentual en VdtConfigBaucher (+detalle)
  REP->>DB: Update VdtPedidoTransaccionDetalleTxn (LpaId/CbIdBase/CbIdPorcentual)
  REP->>DB: Insert VdtDetallePedidoBaucher (evitando duplicados)
  DB-->>REP: Confirmación
  REP-->>HDR: PreventaResponse<int> (detalles actualizados)
  HDR-->>API: 200 OK
```

### Verificar Cantidad Cero en Pedido
```mermaid
sequenceDiagram
  participant API as API
  participant QRY as VerificarCantidadCeroPedidoQueryHandler
  participant REP as IPreventaValidacionRepository
  participant DB as AppDbContext

  API->>QRY: GET /api/Preventa/validaciones/pedidos/{pedId}/cantidad-cero
  QRY->>REP: ObtenerClientesConCantidadCeroAsync(pedId)
  REP->>DB: Consulta detalles con DtrCantidad == 0
  DB-->>REP: Lista de clientes
  REP-->>QRY: List<string> cliIds
  QRY-->>API: 200 OK
```

### Aprobar Descuento en Detalle
```mermaid
sequenceDiagram
  participant API as API
  participant HDR as AprobarDescuentoDetalleCommandHandler
  participant REP as IPreventaValidacionRepository
  participant DB as AppDbContext

  API->>HDR: POST /api/Preventa/validaciones/detalles/{dtrId}/aprobar-descuento?entIdAprobador={entId}
  HDR->>REP: AprobarDescuentoDetalleAsync(dtrId, entId)
  REP->>DB: Update EntIdAprobacion/DtrAprobado en detalle
  DB-->>REP: Confirmación
  REP-->>HDR: PreventaResponse<bool>
  HDR-->>API: 200 OK
```

### Recorridos por Jefatura
```mermaid
sequenceDiagram
  participant API as API
  participant QRY as GetRecorridosPorJefaturaQueryHandler
  participant REP as IPreventaValidacionRepository
  participant DB as AppDbContext

  API->>QRY: GET /api/Preventa/validaciones/recorridos/jefatura
  QRY->>REP: GetRecorridosPorJefaturaAsync(filtros)
  REP->>DB: Query recorridos según roles (vendedor/supervisor/jefe/gerente)
  DB-->>REP: Recorridos
  REP-->>QRY: List<RecorridoPorJefaturaDto>
  QRY-->>API: 200 OK
```

## Endpoints
- `GET /api/Preventa/validaciones/usuario/{usrId}`
- `GET /api/Preventa/validaciones/clientes?recId={recId}&pedId={pedId}`
- `GET /api/Preventa/validaciones/recorridos/jefatura` (query: `entIdVendedor`, `entIdSupervisor`, `entIdJefeVentas`, `entIdGerenteVentas`)
- `POST /api/Preventa/validaciones/pedidos/{pedId}/aplicar-lista-precio`
- `GET /api/Preventa/validaciones/pedidos/{pedId}/cantidad-cero`
- `POST /api/Preventa/validaciones/detalles/{dtrId}/aprobar-descuento?entIdAprobador={entId}`

## Consideraciones de Auditoría
- Cambios de `LpaId`, `CbIdBase`, `CbIdPorcentual` pueden ser registrados en `AuditoriaPedidoDetalle` o en el sistema de auditoría (`SgtAuditoriaCambios`) según políticas.
- `VdtDetallePedidoBaucher` asegura trazabilidad del báucher aplicado a un detalle y pedido.

## Buenas Prácticas
- Validar vigencia por fecha al seleccionar `LpaId` y báuchers.
- Evitar duplicados en `VdtDetallePedidoBaucher` al re-aplicar reglas.
- Mantener transacciones unitarias y `SaveChanges` al final del lote.
- Usar `AsNoTracking` en consultas de solo lectura para performance.

## Pruebas sugeridas
- Pedido con lista de precios vigente y sin báucher: espera actualización de `LpaId`.
- Pedido con báucher base y porcentual aplicables: espera actualización de ambos y dos filas en `VdtDetallePedidoBaucher`.
- Pedido con detalles `DtrCantidad == 0`: espera respuesta con `cliIds` correspondientes.
- Aprobación de descuento: confirma `EntIdAprobacion` y `DtrAprobado == true`.

