# Dependencias del Sistema

## Python

Odoo 19 requiere Python 3.10+

```bash
python3 --version  # Verificar versión
```

## Paquetes Python OCA

Los módulos OCA no tienen dependencias Python adicionales por defecto.

Solo si necesitas:

### Importación de Archivos

Si usas `account_statement_import_sheet_file` (CSV/XLSX):

```bash
pip install openpyxl xlrd
```

### Operaciones Avanzadas

Para formatos SEPA avanzados:

```bash
pip install lxml
```

## Sistema Operativo

### Ubuntu/Debian

```bash
sudo apt-get install python3-dev libpq-dev
```

### macOS

```bash
brew install python@3.10
```

### Windows

Usar Python.org installer

## Odoo Requisitos

- **Versión**: Odoo 19
- **BD**: PostgreSQL 12+
- **Almacenamiento**: 500MB mínimo

## Opcional pero Recomendado

### Herramientas de Desarrollo

```bash
pip install -r requirements.txt
```

### Linters

```bash
pip install flake8 pylint
```

## Verificación

Ejecutar en terminal Odoo:

```python
from odoo.addons.account_payment_mode.models import account_payment_mode
print("✓ Módulos instalados correctamente")
```

## Troubleshooting Dependencias

### Error: "No module named 'openpyxl'"

```bash
pip install openpyxl
```

### Error: "psycopg2 not found"

Ya viene con Odoo, si falla:

```bash
pip install psycopg2-binary
```

### Error: "lxml not available"

```bash
pip install lxml
```
