# Flujo: Reconciliación Bancaria Completa

Paso a paso reconciliar movimientos banco con Odoo.

## 📋 Pre-requisitos

- ✓ Extracto importado en Odoo
- ✓ Módulo `account_reconcile_oca` instalado
- ✓ Movimientos contables creados

## 🚀 Paso 1: Acceder Reconciliación

```
Contabilidad → Reconciliación Bancaria
→ Seleccionar banco
→ Botón: Reconciliar
```

Interfaz abre:

```
┌─────────────────────┬──────────────────┐
│  Movimientos Banco  │ Movimientos Odoo │
├─────────────────────┼──────────────────┤
│ 01/06 | 500€        │ INV-001 | 500€   │
│ 02/06 | -300€       │ PROV-001 | -300€ │
│ 03/06 | -2€         │ Comisión | -2€   │
└─────────────────────┴──────────────────┘
```

## 🚀 Paso 2: Búsqueda Automática

```
Botón: "Auto Match" / "Auto Reconcile"
```

Odoo intenta emparejar automáticamente:

```
✓ 500€ (banco) ↔ INV-001 500€ (Odoo) → MATCH
✓ -300€ (banco) ↔ PROV-001 -300€ (Odoo) → MATCH
✓ -2€ (banco) ↔ Comisión -2€ (Odoo) → MATCH
```

Si todo coincide → Todo reconciliado ✓

## 🚀 Paso 3: Reconciliación Manual

Si hay movimientos sin emparejar:

```
Seleccionar en banco:
01/06 | 500€ (INV-001)

Seleccionar en Odoo:
INV-001 | 500€

Botón: "Reconcile"
```

## ✅ Checklist

- [ ] Extracto importado
- [ ] Movimientos Odoo creados
- [ ] Auto Match ejecutado
- [ ] Totales cuadran
- [ ] Extracto validado

## Ver También

- [Importar Extractos](workflow-statement-import.md)
- [Flujo Pagos SEPA](workflow-payment-sepa.md)
