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

## 🚀 Paso 3: Reconciliación Manual (si no auto)

Si hay movimientos sin emparejar:

```
Seleccionar en banco:
01/06 | 500€ (INV-001)

Seleccionar en Odoo:
INV-001 | 500€

Botón: "Reconcile"
```

**Resultado:**
```
Movimiento reconciliado ✓
```

## 🚀 Paso 4: Validar Totales

```
Suma banco:     500€ - 300€ - 2€ = 198€
Suma Odoo:      500€ - 300€ - 2€ = 198€
Estado:         ✓ CUADRA
```

## 🚀 Paso 5: Comisiones/Gastos (si no están en Odoo)

Si banco tiene comisión:

```
Movimiento banco: -2€ (Comisión)
Odoo:             (vacío - no existe)
```

**Opción A: Crear apunte manual**

```
Contabilidad → Asientos
→ Nuevo

Línea 1:
├─ Cuenta: Gastos financieros
├─ Debe: 0
├─ Haber: 2€

Línea 2:
├─ Cuenta: Banco
├─ Debe: 2€
├─ Haber: 0

Validar
```

Luego reconciliar.

**Opción B: Usar reglas automáticas**

```
Configuración → Reglas Reconciliación
→ Nuevo

Regla: Comisión banco
├─ Si descripción contiene: "comisión"
├─ Crear apunte automático
└─ Cuenta: Gastos financieros
```

## 🚀 Paso 6: Cerrar Extracto

Una vez todo reconciliado:

```
Botón: "Validate Reconciliation"
```

O:

```
Botón: "Mark as Done"
```

**Estado cambia:**
```
Draft → Done
```

**Extracto cerrado:**
```
ST/2026/001 - RECONCILIADO ✓
Saldo: 198€
```

## ✅ Checklist

- [ ] Extracto importado
- [ ] Movimientos Odoo creados
- [ ] Auto Match ejecutado
- [ ] Coincidencias visuales correctas
- [ ] Comisiones/gastos tratados
- [ ] Totales cuadran
- [ ] Extracto validado

## 🚨 Troubleshooting

**No hay coincidencias**

```
Problema: Banco 500€, Odoo 0€
Causas:
- Factura no registrada en Odoo
- Importe diferente
- Referencia no coincide
- Fecha muy antigua (sin factura)

Solución:
→ Crear apunte manual
→ O crear factura faltante
```

**Saldo no cuadra**

```
Banco: 198€
Odoo:  200€

Falta: -2€

Solución:
→ Revisar movimientos desapareados
→ Comprobar comisiones
→ Verificar transacciones pendientes
```

**Error: "Reconciliación fallida"**

```
Error: Cannot reconcile move lines

Causas:
- Movimiento ya reconciliado antes
- Movimiento bloqueado
- Moneda diferente

Solución:
→ Deshacer reconciliación anterior
→ Desbloquear movimiento
→ Verificar moneda = EUR
```

## 📌 Notas

- Reconciliar mismo día recepción extracto
- Guardar comprobantes bancarios
- Revisar resumen mensual
- Alertas si no cuadra
