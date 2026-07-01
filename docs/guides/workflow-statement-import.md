# Flujo: Importación de Extractos Bancarios

Visión general completa del proceso.

## 📊 Diagrama Completo

```
BANCO
  ↓ (Descargar extracto)
  ↓ CSV / XLSX / PDF
  ↓
ODOO - Import Wizard
  ├─ Seleccionar archivo
  ├─ Mapear columnas
  ├─ Validar datos
  └─ Crear extracto
  ↓
Bank Statement (ST-2026-001)
  ├─ Movimientos importados
  ├─ Estado: Draft
  └─ Líneas: 10 movimientos
  ↓
Reconciliation
  ├─ Auto-match movimientos
  ├─ Revisar discrepancias
  └─ Resolver manualmente
  ↓
Validar Reconciliación
  ├─ Totales cuadran
  ├─ Todo reconciliado
  └─ Estado: Done
  ↓
Cierre Contable
  ├─ Extracto cerrado
  ├─ Asientos creados
  └─ Informes disponibles
```

## 🔄 Flujo Detallado

### Fase 1: Descarga

```
Banco (BBVA, Santander, etc)
  → Portal Banca Electrónica
  → Seleccionar período
  → Descargar extracto
  → Guardar CSV/XLSX en escritorio
```

### Fase 2: Importación

```
Odoo
  → Contabilidad → Extractos
  → Botón "Importar"
  → Subir archivo
  → Mapear columnas
  → Confirmar datos
```

### Fase 3: Creación Extracto

```
Odoo crea:
  → account.bank.statement (ST-2026-001)
  → account.bank.statement.line (múltiples)
  → Estados: draft
```

### Fase 4: Reconciliación

```
Reconciliation Widget
  ← Banco (movimientos importados)
  ↔ Odoo (facturas, apuntes)
  → Match automático
  → Revisión manual
```

### Fase 5: Validación

```
Verificar:
  ✓ Totales cuadren
  ✓ Todo reconciliado
  ✓ Sin errores
  → Marcar como Done
```

### Fase 6: Cierre

```
Generar:
  ✓ Asientos contables
  ✓ Saldos actualizados
  ✓ Reportes disponibles
```

## 📋 Formatos Soportados

| Formato | Software | Extensión | Estado |
|---------|----------|-----------|--------|
| CSV | Excel, Google Sheets | .csv | ✓ Soportado |
| XLSX | Excel, Libre Office | .xlsx | ✓ Soportado |
| PDF | Banco | .pdf | ⚠️ Manual OCR |
| TXT | Plano | .txt | ⚠️ Con estructura |
| ODS | Libre Office | .ods | ✗ Convertir a XLSX |

## 🛠️ Herramientas Auxiliares

### Para Conversión

```
PDF → CSV
  → Usar: https://extracttable.com/
  → O: Copiar/pegar manual
  → O: OCR (Tesseract)

XLS → XLSX
  → Excel: Guardar como XLSX
  → LibreOffice: Exportar

```

## 📊 Campos Requeridos

Mínimo necesario:

```
Obligatorio:
  ✓ Fecha (Date)
  ✓ Concepto/Referencia (String)
  ✓ Importe (Float)

Optativo pero útil:
  - Saldo (Float)
  - Tipo (Debit/Credit)
  - Referencia extendida
```

## ✅ Validaciones Odoo

Odoo verifica automáticamente:

```
✓ Formato fecha válido
✓ Importes son números
✓ No hayan duplicados
✓ Diario bancario activo
✓ Moneda coincida
✓ Saldo cuadre (si proporcionado)
```

## 📈 Casos de Uso

### Caso 1: Empresa Pequeña

```
Extracto mensual
  ↓ 1 archivo CSV
  ↓ 20-50 movimientos
  ↓ 30 minutos procesado
  ↓ Reconciliación automática
```

### Caso 2: Empresa Grande

```
Múltiples bancos
  ↓ 3-5 extractos diarios
  ↓ 200+ movimientos por extracto
  ↓ Reglas reconciliación automáticas
  ↓ Alertas por discrepancias
```

### Caso 3: Consolidación

```
Múltiples cuentas
  ↓ Consolidar en extracto único
  ↓ Mapeo multi-diario
  ↓ Reconciliación cruzada

```

## 🚨 Errores Comunes

```
❌ Columnas desordenadas
   → Reorder: fecha, concepto, debe, haber

❌ Moneda mixta
   → Usar moneda única: EUR

❌ Duplicados
   → Limpiar: no importar dos veces

❌ Formato fecha incorrecto
   → Usar: DD/MM/YYYY o YYYY-MM-DD

❌ Números con símbolo €
   → Usar: 500.00 (sin €)
```

## 📌 Checklist Proceso

- [ ] Extracto descargado de banco
- [ ] Archivo convertido a CSV/XLSX si necesario
- [ ] Columnas verificadas
- [ ] Importación sin errores
- [ ] Movimientos visibles en Odoo
- [ ] Auto-match ejecutado
- [ ] Discrepancias revisadas
- [ ] Reconciliación manual completada
- [ ] Totales verificados
- [ ] Extracto marcado como Done
- [ ] Reportes generados

## 📞 Próximos Pasos

Después reconciliar:

1. [Crear Orden de Pago](create-payment-order.md)
2. [Reportes Contables](../../api/models-fields.md)
3. [Cierre Mensual](../workflow-bank-reconciliation.md)
