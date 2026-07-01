# account_banking_sepa_direct_debit

Domiciliación SEPA - Adeudos electrónicos.

## ¿Qué es?

Sistema de cobro automatizado:

- Adeudo directo en cuenta cliente
- Basado en mandatos SEPA
- Archivo PAIN-008
- Validación automática

## Instalación

```
Aplicaciones → Buscar "SEPA Direct Debit"
Instalar: account_banking_sepa_direct_debit
```

## Workflow

```
1. Cliente firma mandato
         ↓
2. Crear factura
         ↓
3. Asignar modo pago: "SEPA Direct Debit"
         ↓
4. Crear línea de pago con mandato
         ↓
5. Agrupar en orden de pago
         ↓
6. Generar archivo PAIN-008
         ↓
7. Enviar a banco
         ↓
8. Banco adeuda cuenta cliente
         ↓
9. Reconciliar movimiento
```

## Configuración

### 1. Payment Mode SEPA

```
Contabilidad → Modos de Pago
→ Nuevo/Editar

Name: SEPA Direct Debit
Code: sepa_dd
Type: SEPA Direct Debit
Instruction: Normal / High / Very High
```

### 2. En Factura

```
Factura Proveedor
├─ Monto: 500€
├─ Cliente: Empresa X
├─ Payment Mode: SEPA Direct Debit
└─ Mandato: MANDATE-2026-001 (automático)
```

### 3. Crear Orden

```
Contabilidad → Órdenes Pago (SEPA DD)
→ Nuevo
→ Agregar facturas
→ Validar
→ Generar archivo PAIN-008
```

## Archivo Generado

```
SEPA_DD_20260601.xml
├─ Mensaje ID: MSG-20260601-001
├─ Mandante: Mi Empresa S.L.
├─ Mandatos:
│  ├─ Empresa X: 500€ (OOFF)
│  ├─ Empresa Y: 300€ (RCUR)
│  └─ Empresa Z: 200€ (RCUR)
└─ Total: 1.000€
```

## Restricciones

- Mínimo importe: 0,01€
- Máximo: Sin límite
- Mandato debe ser válido
- Cliente en SEPA

## Troubleshooting

**P: Error "Mandato no válido"**
- R: Verificar mandato: estado Valid, no expirado

**P: Archivo rechazado banco**
- R: Validar UMR único, datos cliente

**P: IBAN cliente inválido**
- R: Actualizar IBAN en cliente

## Ver También

- [account_banking_mandate](account_banking_mandate.md)
- [l10n_es_account_banking_sepa_fsdd](l10n_es_account_banking_sepa_fsdd.md)
