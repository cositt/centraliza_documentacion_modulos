# Centraliza - Documentación Módulos Odoo 19

Documentación completa de módulos de contabilidad, pagos SEPA y reconciliación bancaria para Odoo 19.

📚 **[Ver Documentación Online](https://cositt.github.io/centraliza_documentacion_modulos/)**

## Módulos Documentados

### 💳 Pagos
- `account_payment_mode` - Configuración de modos de pago
- `account_payment_order` - Órdenes de pago
- `account_banking_mandate` - Mandatos bancarios

### 🏦 SEPA
- `account_banking_pain_base` - Base PAIN
- `account_banking_sepa_direct_debit` - Domiciliación SEPA
- `l10n_es_account_banking_sepa_fsdd` - FSDD España

### 🔄 Reconciliación
- `account_reconcile_oca` - Reconciliación contable
- `account_reconcile_analytic_tag` - Tags analíticos

### 📊 Extractos
- `account_statement_base` - Base extractos
- `account_statement_import_base` - Importación base
- `account_statement_import_file` - Importación archivos
- `account_statement_import_sheet_file` - Importación CSV/XLSX

## Estructura

```
docs/
├── setup/              # Instalación y configuración
├── modules/            # Documentación de módulos
│   ├── payment/
│   ├── sepa/
│   ├── reconciliation/
│   └── statements/
├── guides/             # Guías de uso
├── examples/           # Ejemplos prácticos
├── api/                # Referencia técnica
└── troubleshooting.md  # Solución de problemas
```

## Guías Rápidas

- [Orden de Instalación](docs/setup/installation-order.md)
- [Crear Orden de Pago](docs/guides/examples/create-payment-order.md)
- [Reconciliar Extractos](docs/guides/examples/reconcile-statements.md)
- [Importar CSV](docs/guides/examples/import-csv.md)

## Desarrollo

Editado con Markdown + MkDocs + GitHub Pages.

Deploy automático: push → live en minutos.

## Licencia

AGPL-3.0 (igual que módulos OCA)
