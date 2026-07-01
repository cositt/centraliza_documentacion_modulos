# Flujo: Crear Orden de Pago SEPA

Paso a paso para crear orden de pago a proveedores.

## 📋 Pre-requisitos

- ✓ Módulos instalados en orden
- ✓ Proveedores creados
- ✓ Facturas sin pagar
- ✓ Modos de pago configurados

## 🚀 Paso 1: Verificar Factura

```
Contabilidad → Facturas Proveedor
→ Seleccionar factura sin pagar

Verificar:
├─ Proveedor: correcto
├─ Importe: correcto
├─ Vencimiento: correcto
├─ IBAN Proveedor: completado
└─ Estado: Validada
```

**Ejemplo:**

```
Factura: PROV/2026/001
├─ Proveedor: Materiales S.L.
├─ Importe: 500€
├─ IBAN: ES9121000418450200051332
├─ Vencimiento: 15/06/2026
└─ Estado: Posted ✓
```

## 🚀 Paso 2: Crear Orden de Pago

```
Contabilidad → Pagos → Órdenes de Pago
→ Botón: Nuevo
```

**Completar:**

| Campo | Valor |
|-------|-------|
| Nombre | Auto (PO-2026-001) |
| Fecha | Hoy |
| Modo Pago | Transferencia SEPA |
| Diario | Banco principal |
| Empresa | Mi Empresa S.L. |

```
Guardar como borrador
```

## 🚀 Paso 3: Agregar Líneas

### Opción A: Manual

```
Pestaña: Líneas de Pago
→ Agregar línea

Rellenar:
├─ Proveedor: Materiales S.L.
├─ IBAN: ES91...
├─ Importe: 500€
├─ Concepto: PROV/2026/001
└─ Fecha vencimiento: 15/06/2026
```

### Opción B: Asistente

```
Botón: "Agregar facturas"
→ Wizard

Filtrar:
├─ Proveedor: Materiales S.L.
├─ Estado: Ready to Pay
└─ Modo pago: SEPA

Seleccionar facturas
→ Confirmar
```

**Resultado:**

```
Líneas agregadas:
├─ PROV/2026/001: 500€
├─ PROV/2026/002: 300€
└─ PROV/2026/003: 200€
Total: 1.000€
```

## 🚀 Paso 4: Validar

```
Botón: "Validar"
```

Odoo verifica:
- ✓ IBAN válido
- ✓ Importes > 0
- ✓ Proveedor existe
- ✓ Modo pago asignado

**Si todo OK:**
```
Estado cambia: Draft → Open
```

## 🚀 Paso 5: Generar Archivo

```
Botón: "Generar Archivo"
```

Descarga:
```
PO-2026-001.xml
```

**Contenido SEPA:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Document>
  <CstmrCdtTrfInitn>
    <PmtInf>
      <NbOfTxns>3</NbOfTxns>
      <CtrlSum>1000.00</CtrlSum>
      <Dbtr>
        <Nm>Mi Empresa S.L.</Nm>
      </Dbtr>
      <CdtTrfTxInf>
        <PmtId>PROV/2026/001</PmtId>
        <Cdtr>
          <Nm>Materiales S.L.</Nm>
        </Cdtr>
        <CdtrAcct>
          <Id>
            <IBAN>ES91...</IBAN>
          </Id>
        </CdtrAcct>
        <Amt>
          <InstdAmt>500.00</InstdAmt>
        </Amt>
      </CdtTrfTxInf>
    </PmtInf>
  </CstmrCdtTrfInitn>
</Document>
```

## 🚀 Paso 6: Enviar a Banco

1. Descargar archivo XML
2. Abrir portal banco
3. Subir archivo SEPA
4. Confirmar pago
5. Banco procesa

## 🚀 Paso 7: Reconciliar

Una vez banco procese:

```
Contabilidad → Extractos Bancarios
→ Importar extracto
```

Los movimientos se reconcilian automáticamente.

```
Orden PO-2026-001: Status Done ✓
```

## ✅ Checklist Final

- [ ] Factura validada
- [ ] Orden creada
- [ ] Líneas agregadas
- [ ] Validada sin errores
- [ ] Archivo generado
- [ ] Enviado a banco
- [ ] Pago procesado
- [ ] Reconciliado

## 🚨 Troubleshooting

**Error: IBAN inválido**
```
→ Verificar IBAN proveedor
→ Debe ser: ES + 22 dígitos
```

**Error: "Ready to Pay"**
```
→ Factura debe estar Posted
→ No estar pagada parcialmente
```

**No descarga archivo**
```
→ Comprobar pop-up blocker
→ Validar primero
```

## 📌 Notas

- Archivo válido 30 días
- Banco puede tardar 1-3 días
- Guardar comprobante envío
- Cada proveedor = línea nueva
