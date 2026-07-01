# account_banking_mandate

Mandatos para domiciliaciones SEPA (adeudos).

## ¿Qué es?

Autorización del cliente para adeudos:

- Consentimiento para domiciliación
- Mandato único (OOF)
- Mandato recurrente (RC)
- Validación y seguimiento

## Instalación

```
Aplicaciones → Buscar "Banking Mandate"
Instalar: account_banking_mandate
```

## Configuración

### 1. Crear Mandato

```
Contabilidad → Mandatos Bancarios
→ Nuevo
```

**Campos:**

| Campo | Descripción |
|-------|------------|
| **Name** | MANDATE-001 |
| **Partner** | Cliente |
| **Signature Date** | Fecha firma |
| **Type** | OOF (única) o RC (recurrente) |
| **Account Number** | IBAN cliente |

### 2. Estado del Mandato

```
Draft         → Borrador, editable
Valid         → Válido, puede usarse
Expired       → Expirado
Cancelled     → Anulado
Closed        → Cerrado (archivado)
```

### 3. Validar Mandato

```
Botón: "Validate"
→ Verifica datos
→ Cambia estado: Draft → Valid
```

## Ejemplo

```
Mandato: MANDATE-2026-001
├─ Cliente: Empresa X S.L.
├─ IBAN: ES9121000418450200051332
├─ Tipo: RC (recurrente)
├─ Firma: 01/06/2026
├─ Válido desde: 01/06/2026
└─ Válido hasta: 31/12/2030
```

## Relación con Órdenes de Pago

En `account_payment_order`:

```
Orden de Pago (Domiciliación)
    ├─ Mandato: MANDATE-2026-001
    ├─ Cliente: Empresa X
    ├─ Importe: 500€
    └─ Ejecutar: Sistema verifica mandato válido
```

## Campos Avanzados

### Unique Mandate Reference (UMR)

Identificador único SEPA:
```
MANDATE-ES-2026-001
```

### Sequence Type

```
OOFF    → Pago único, primer mandato
FNAL    → Pago único, último mandato
RCUR    → Recurrente, medio
OOFF    → Recurrente, primero
FNAL    → Recurrente, último
```

### Creditor Reference

Referencia acredor (para banco):
```
RF98NOZ11QWERTY98765
```

## Validaciones

Odoo valida:

- ✓ IBAN correcto
- ✓ Mandato activo
- ✓ Tipo pago compatible
- ✓ No expirado
- ✓ No cancelado

## Reportes

```
Contabilidad → Mandatos Bancarios
→ Seleccionar
→ Imprimir → PDF con acuerdo
```

## Troubleshooting

**P: Mandato rechazado por banco**
- R: Verificar UMR único, firma válida

**P: Error "Mandato expirado"**
- R: Crear nuevo mandato si cliente consiente

**P: IBAN inválido**
- R: Verificar formato: ES + 22 dígitos

## Relaciones

```
account_banking_mandate
    ├─ res_partner (cliente)
    ├─ res_partner_bank (IBAN)
    ├─ account_payment_order
    └─ account_payment_line
```

## Ver También

- [account_payment_order](account_payment_order.md)
- [account_banking_sepa_direct_debit](../sepa/account_banking_sepa_direct_debit.md)
