# Orden de Instalación de Módulos

## ⚠️ Importante

**La instalación debe ser en orden específico** para evitar errores de dependencias.

## 📋 Orden Recomendada

### Paso 1: Base Contable
```
1. account
```
*(Ya viene con Odoo)*

### Paso 2: Base de Pagos
```
2. account_payment_mode
3. account_payment_order
```

### Paso 3: Mandatos Bancarios
```
4. account_banking_mandate
```

### Paso 4: SEPA Base
```
5. account_banking_pain_base
```

### Paso 5: SEPA Domiciliaciones
```
6. account_banking_sepa_direct_debit
```

### Paso 6: SEPA España
```
7. l10n_es_account_banking_sepa_fsdd
```

### Paso 7: Base Extractos
```
8. account_statement_base
```

### Paso 8: Importación Extractos
```
9. account_statement_import_base
10. account_statement_import_file
11. account_statement_import_sheet_file
```

### Paso 9: Reconciliación
```
12. account_reconcile_oca
13. account_reconcile_analytic_tag
```
*(Opcional si no necesitas tags analíticos)*

## 🔗 Árbol de Dependencias

```
account (Odoo)
    ├─ account_payment_mode
    │   └─ account_payment_order
    │       └─ account_banking_mandate
    │
    ├─ account_statement_base
    │   ├─ account_statement_import_base
    │   │   ├─ account_statement_import_file
    │   │   │   └─ account_statement_import_sheet_file
    │   │   └─ account_reconcile_oca
    │   │       └─ account_reconcile_analytic_tag
    │   │
    │   └─ account_banking_pain_base
    │       ├─ account_banking_sepa_direct_debit
    │       │   └─ l10n_es_account_banking_sepa_fsdd
```

## ✅ Verificación

Después de instalar cada módulo:

1. ✓ No hay errores en logs
2. ✓ Aplicación cargó correctamente
3. ✓ Menús aparecen correctamente

## ⚡ Instalación por Lotes

Si prefieres instalar múltiples a la vez:

**Lote 1:** Instalar simultáneamente
```
account_payment_mode
account_payment_order
account_statement_base
```

**Esperar a que terminen**, luego:

**Lote 2:**
```
account_banking_mandate
account_statement_import_base
account_reconcile_oca
```

**Esperar**, luego:

**Lote 3:**
```
account_banking_pain_base
account_statement_import_file
```

**Esperar**, luego:

**Lote 4:**
```
account_banking_sepa_direct_debit
account_statement_import_sheet_file
```

**Esperar**, luego:

**Lote 5:**
```
l10n_es_account_banking_sepa_fsdd
account_reconcile_analytic_tag
```

## 🚨 Si hay Errores

1. Revisa logs: `var/log/odoo.log`
2. Desinstala el último módulo
3. Recarga página
4. Intenta nuevamente

Ver [Troubleshooting](../troubleshooting.md)
