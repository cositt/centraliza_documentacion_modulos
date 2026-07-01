# account_reconcile_oca

Herramientas avanzadas de reconciliación contable.

## ¿Qué es?

Interfaz visual para reconciliar:

- Movimientos bancarios ↔ Factura
- Multidivisa soportada
- Reglas automáticas
- Auditoría completa

## Instalación

```
Aplicaciones → Buscar "Account Reconcile"
Instalar: account_reconcile_oca
```

## Reconciliación Básica

```
Contabilidad → Reconciliación Bancaria
→ Seleccionar extracto
→ Movimientos sin reconciliar
```

**Interfaz:**
- Izquierda: Movimientos banco
- Derecha: Movimientos Odoo
- Centro: Match automático

### Ejemplo

```
Extracto bancario: 01/06/2026
├─ Ingreso: 500€ (Ref: INV-001)
├─ Gasto: 300€ (Ref: PROV-001)
└─ Comisión: 2€

Odoo movimientos:
├─ Factura cliente INV-001: 500€ ✓ Match
├─ Factura proveedor PROV-001: 300€ ✓ Match
└─ Comisión banco: 2€ ✓ Match
```

## Estados

```
Draft            → No reconciliado
In Progress      → Parcialmente
Done             → Completo
```

## Reglas de Reconciliación

```
Contabilidad → Configuración → Reglas Reconciliación
→ Nuevo

Regla: Comisión banco
├─ Criterio: Descripción contiene "comisión"
├─ Cuenta: Gastos financieros
└─ Automático: Sí
```

## Ver También

- [account_reconcile_analytic_tag](account_reconcile_analytic_tag.md)
- [account_statement_import_file](../statements/account_statement_import_file.md)
