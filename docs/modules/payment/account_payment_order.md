# account_payment_order

Agrupa líneas de pago en órdenes para procesamiento bancario.

## ¿Qué es?

Crea **lotes de pagos** para enviar al banco:

- Agrupa múltiples pagos
- Genera archivos SEPA/PAIN
- Seguimiento de estado
- Auditoría de pago

## Instalación

```
Aplicaciones → Buscar "Payment Order"
Instalar: account_payment_order
```

## Configuración

### 1. Crear Orden de Pago

```
Contabilidad → Pagos → Órdenes de Pago
→ Nuevo
```

**Campos:**

| Campo | Descripción |
|-------|------------|
| **Name** | Generado automáticamente |
| **Date** | Fecha creación |
| **Mode** | Modo pago (Transferencia, etc) |
| **Journal** | Diario bancario |

### 2. Agregar Líneas

```
Pestaña: Payment Lines
→ Agregar línea

Opciones:
A) Manual → Crear línea directo
B) Asistente → Seleccionar facturas
```

### 3. Validar y Procesar

```
Botón: "Validate"
→ Verifica importes, IBAN
→ Cambiar estado: Draft → Open
```

### 4. Generar Archivo

```
Botón: "Generate File"
→ Descarga archivo SEPA/PAIN
→ Enviar a banco
```

## Ejemplo

```
Orden: PO-2026-001
├─ Modo: Transferencia SEPA
├─ Línea 1: Proveedor A → 500€
├─ Línea 2: Proveedor B → 300€
├─ Línea 3: Proveedor C → 200€
├─ Total: 1.000€
└─ Archivo generado: PO-2026-001.xml
```

## Estados

```
Draft        → Creada, editable
Open         → Validada, pronta enviar
Done         → Enviada al banco
Cancelled    → Anulada
```

## Líneas de Pago

**Campos principales:**

- **Partner**: Acreedor
- **Amount**: Importe
- **Due Date**: Vencimiento
- **Reference**: Referencia (número factura)
- **Bank Account**: Cuenta destino IBAN

## Generación de Archivo

Formatos soportados:

| Formato | Tipo | Uso |
|---------|------|-----|
| **PAIN XML** | SEPA | Transferencias, domiciliaciones |
| **CSV** | Importación | Bancos compatibles |
| **TXT** | Heredado | Compatibilidad |

## Reportes

```
Contabilidad → Reportes → Payment Orders
→ Seleccionar
→ Generar PDF
```

Muestra:
- Resumen pagos
- Detalles líneas
- Importes verificación

## Troubleshooting

**P: Error validación IBAN**
- R: Verificar cuenta bancaria proveedor

**P: No aparece factura en asistente**
- R: Factura debe estar "Ready to Pay"

**P: Archivo no descarga**
- R: Verificar permisos, browser pop-up blocker

## Relaciones

```
account_payment_order
    ├─ account_payment_mode
    ├─ account_payment_line
    ├─ account_move
    └─ account_journal
```

## Ver También

- [account_payment_mode](account_payment_mode.md)
- [account_banking_mandate](account_banking_mandate.md)
- [Crear Orden Pago - Guía](../../guides/examples/create-payment-order.md)
