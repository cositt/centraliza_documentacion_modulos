# Flujo: Pagos SEPA Completo

Visión general del proceso de pagos.

## 📊 Diagrama

```
FACTURAS PROVEEDOR (sin pagar)
  ↓
  ├─ Proveedor A: 500€
  ├─ Proveedor B: 300€
  └─ Proveedor C: 200€
  ↓
CREAR ORDEN DE PAGO
  ├─ Agrupar facturas
  ├─ Validar IBAN
  └─ Asignar modo pago: SEPA
  ↓
GENERAR ARCHIVO SEPA (XML/PAIN)
  ├─ Validar datos
  ├─ Generar PAIN-001
  └─ Descargar archivo
  ↓
ENVIAR A BANCO
  ├─ Subir archivo portal
  ├─ Confirmar envío
  └─ Obtener referencia
  ↓
BANCO PROCESA
  ├─ Adeuda cuentas
  ├─ Genera movimientos
  └─ Entra en estado: Done
  ↓
IMPORTAR EXTRACTO
  ├─ Descargar de banco
  ├─ Importar en Odoo
  └─ Crear movimientos
  ↓
RECONCILIAR
  ├─ Emparejar movimientos
  ├─ Validar totales
  └─ Cerrar extracto
  ↓
✓ PROCESO COMPLETO
```

## 🚀 Etapas Clave

### 1️⃣ Preparación

```
Verificar:
✓ Facturas validadas (Posted)
✓ Sin pagar (Open)
✓ Vencidas o próximas vencer
✓ Proveedores tienen IBAN
✓ Modo pago: SEPA Transfer
✓ Diario bancario activo
```

### 2️⃣ Agrupación

```
Crear Orden de Pago
  ├─ Parámetros:
  │  ├─ Fecha: hoy
  │  ├─ Modo: Transfer SEPA
  │  └─ Diario: Banco principal
  └─ Agregar facturas:
     ├─ Manual (1 por 1)
     └─ Automático (asistente)
```

### 3️⃣ Validación

```
Botón: Validate
Odoo verifica:
  ✓ IBAN correcto
  ✓ Importes > 0
  ✓ Proveedor existe
  ✓ Divisa = EUR
  ✓ Estado: Draft → Open
```

### 4️⃣ Generación

```
Botón: Generate File
Descargar: PO-2026-001.xml

Contenido XML:
  ├─ Empresa pagadora
  ├─ Banco
  ├─ 3 líneas pago
  ├─ Total: 1.000€
  └─ Datos validados
```

### 5️⃣ Envío

```
Portal Banco:
  1. Iniciar sesión
  2. Nuevo pago
  3. Subir archivo XML
  4. Revisar datos
  5. Confirmar
  6. Obtener ref: CONF-2026-001
```

### 6️⃣ Procesamiento

```
Banco (1-3 días laborales):
  ├─ Valida formato
  ├─ Adeuda cuentas
  ├─ Genera movimientos
  └─ Disponible en extracto
```

### 7️⃣ Reconciliación

```
Importar extracto
  ↓
Movimientos banco = Orden Odoo
  ↓
Auto-match: ✓ 1.000€ reconciliado
  ↓
Marcar como Done
```

## 📋 Campos Críticos

### Orden de Pago

```
name             → PO-2026-001 (auto)
date             → 01/06/2026
mode_id          → SEPA Transfer
journal_id       → Banco Principal
company_id       → Mi Empresa S.L.
state            → draft/open/done
```

### Línea de Pago

```
partner_id       → Proveedor (obligatorio)
amount           → 500.00 (obligatorio)
partner_bank_id  → IBAN (obligatorio)
date             → Vencimiento
reference        → PROV/2026/001
move_line_id     → Factura origen
```

## 🔐 Seguridad

```
✓ Archivo encriptado (SSL)
✓ Firma digital opcional
✓ Auditoría completa en Odoo
✓ Referencia única: PO-2026-001
✓ No se puede modificar después validar
```

## 📊 Estados Posibles

```
Draft (borrador)
  → Editable
  → Agregar/quitar líneas
  → Cambiar modo pago

Open (validada)
  → No editable
  → Archivo descargable
  → Lista enviar

Done (enviada)
  → Archivada
  → Trazable
  → Reconciliada

Cancelled (anulada)
  → Por error
  → No procesada por banco
  → Crear nueva orden
```

## 💡 Tips

```
1. Revisar facturas antes crear orden
2. Validar IBAN una sola vez
3. Guardar confirmación banco
4. Reconciliar en 3-5 días máximo
5. Archivar orden para auditoría
6. Crear regla para pagos recurrentes
```

## ⏰ Timeline Típico

```
Lunes 10:00
  ↓ Crear orden
Lunes 10:30
  ↓ Validar, generar archivo
Lunes 11:00
  ↓ Enviar a banco
Miércoles 16:00
  ↓ Banco procesa (2-3 días)
Jueves 09:00
  ↓ Importar extracto en Odoo
Jueves 10:00
  ↓ Reconciliar
Jueves 11:00
  ↓ ✓ Completo
```

## 📞 Próximos Pasos

- [Crear Orden Detallado](examples/create-payment-order.md)
- [Troubleshooting](../troubleshooting.md)
- [API Referencia](../api/models-fields.md)
