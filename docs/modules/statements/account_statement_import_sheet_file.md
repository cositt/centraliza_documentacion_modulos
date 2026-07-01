# account_statement_import_sheet_file

Importar CSV/XLSX de extractos.

## ¿Qué es?

Importación de hojas de cálculo:

- CSV (comas/puntos y comas)
- XLSX (Excel)
- Mapeo flexible
- Detección automática

## Instalación

```
Aplicaciones → Buscar "Bank Statement CSV/XLSX"
Instalar: account_statement_import_sheet_file
```

## Workflow

```
1. Exportar extracto como CSV/XLSX del banco
2. Odoo → Contabilidad → Extractos
3. Botón: Importar
4. Subir archivo
5. Mapear columnas
6. Crear extracto
7. Reconciliar
```

## Ejemplo CSV

```
fecha,concepto,debe,haber,saldo
01/06/2026,Ingreso cliente,500,0,500
02/06/2026,Pago proveedor,0,300,200
03/06/2026,Comisión banco,0,2,198
```

## Mapeo

| CSV | Odoo |
|-----|------|
| fecha | Date |
| concepto | Reference |
| debe | Debit |
| haber | Credit |
| saldo | Balance |

## Ver También

- [account_statement_import_file](account_statement_import_file.md)
- [Importar CSV - Guía](../../guides/examples/import-csv.md)
