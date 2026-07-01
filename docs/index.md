# Documentación Centraliza - Módulos Odoo 19

Bienvenido a la documentación oficial de los módulos de contabilidad y pagos SEPA para Odoo 19.

## 🚀 Empezar Rápido

### Instalación Básica

1. **[Ver orden de instalación](setup/installation-order.md)**
2. **[Instalar dependencias](setup/dependencies.md)**
3. Acceder a Odoo y activar módulos en orden

### Primeros Pasos

- 📱 [Configurar modos de pago](modules/payment/account_payment_mode.md)
- 🏦 [Crear orden de pago SEPA](guides/examples/create-payment-order.md)
- 📊 [Importar extracto bancario](guides/examples/import-csv.md)
- 🔄 [Reconciliar movimientos](guides/examples/reconcile-statements.md)

## 📚 Módulos

### Pagos (Payment)

| Módulo | Descripción |
|--------|-------------|
| **account_payment_mode** | Configuración de modos de pago (transferencia, domiciliación, etc) |
| **account_payment_order** | Gestión de órdenes de pago agrupadas |
| **account_banking_mandate** | Mandatos bancarios para domiciliaciones |

### SEPA

| Módulo | Descripción |
|--------|-------------|
| **account_banking_pain_base** | Base para formato PAIN (Payment Initiation) |
| **account_banking_sepa_direct_debit** | Domiciliación SEPA (adeudos) |
| **l10n_es_account_banking_sepa_fsdd** | FSDD (Anticipos de crédito) España |

### Reconciliación

| Módulo | Descripción |
|--------|-------------|
| **account_reconcile_oca** | Herramientas avanzadas de reconciliación |
| **account_reconcile_analytic_tag** | Tags analíticos en reconciliación |

### Extractos Bancarios

| Módulo | Descripción |
|--------|-------------|
| **account_statement_base** | Base para procesamiento de extractos |
| **account_statement_import_base** | Base para importar extractos |
| **account_statement_import_file** | Importar archivos PDF/TXT |
| **account_statement_import_sheet_file** | Importar archivos CSV/XLSX |

## 🎯 Flujos Principales

### 1️⃣ Crear Orden de Pago

```
Factura Proveedor
    ↓
Crear Línea de Pago (Payment Line)
    ↓
Agrupar en Orden de Pago
    ↓
Generar archivo SEPA
    ↓
Enviar a banco
    ↓
Reconciliar
```

### 2️⃣ Importar Extracto Bancario

```
Descargar extracto (CSV/XLSX)
    ↓
Cargar en Odoo (import wizard)
    ↓
Mapear columnas
    ↓
Crear movimientos bancarios
    ↓
Reconciliar con facturas
```

### 3️⃣ Reconciliar Movimientos

```
Ver movimientos sin reconciliar
    ↓
Seleccionar movimientos coincidentes
    ↓
Validar reconciliación
    ↓
Generar asiento contable
    ↓
Cerrar extracto
```

## 🔗 Enlaces Útiles

- [Documentación OCA Bank Payment](https://github.com/OCA/bank-payment)
- [Documentación OCA Account Reconcile](https://github.com/OCA/account-reconcile)
- [Documentación OCA Bank Statement Import](https://github.com/OCA/bank-statement-import)
- [Odoo 19 Docs](https://www.odoo.com/documentation/19.0/)

## ❓ Problemas

Consulta la sección [Troubleshooting](troubleshooting.md) para problemas comunes.

## 📄 Licencia

Todos los módulos están bajo licencia **AGPL-3.0**.

---

**Última actualización**: Junio 2026
