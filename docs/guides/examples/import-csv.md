# Guía: Importar CSV/XLSX de Extracto Bancario

Paso a paso para cargar extracto en Odoo.

## 📋 Pre-requisitos

- ✓ Extracto descargado del banco (CSV o XLSX)
- ✓ Módulo `account_statement_import_sheet_file` instalado
- ✓ Diario bancario configurado

## 📄 Formato CSV Esperado

```
fecha,concepto,debe,haber,saldo
01/06/2026,Ingreso cliente,500.00,,500.00
02/06/2026,Pago proveedor,,300.00,200.00
03/06/2026,Comisión banco,,2.00,198.00
```

**Columnas necesarias:**
- `fecha`: DD/MM/YYYY o YYYY-MM-DD
- `concepto`: Referencia movimiento
- `debe`: Ingresos (dejar vacío si no aplica)
- `haber`: Gastos (dejar vacío si no aplica)
- `saldo`: Saldo resultante (opcional)

## 📄 Formato XLSX

Columna A | Columna B | Columna C | Columna D | Columna E
-----------|-----------|-----------|-----------|----------
fecha | concepto | debe | haber | saldo
01/06/2026 | Ingreso | 500,00 | | 500,00
02/06/2026 | Pago | | 300,00 | 200,00

## 🚀 Paso 1: Acceder a Importación

```
Contabilidad → Extractos Bancarios
→ Botón: Importar
```

O:

```
Contabilidad → Configuración → Diarios
→ Seleccionar banco
→ Botón: Importar extracto
```

## 🚀 Paso 2: Subir Archivo

```
Wizard: Import Bank Statement
→ Campo: Archivo
→ Seleccionar archivo CSV o XLSX
→ Siguiente
```

**Archivo aceptado:**

```
✓ CSV (delimitador: coma o punto y coma)
✓ XLSX (Excel 2007+)
✗ PDF
✗ TXT sin estructura
```

## 🚀 Paso 3: Mapear Columnas

El wizard muestra:

```
Columnas detectadas:
├─ Columna 1: fecha → Mapear a: Date
├─ Columna 2: concepto → Mapear a: Reference
├─ Columna 3: debe → Mapear a: Amount (Debit)
├─ Columna 4: haber → Mapear a: Amount (Credit)
└─ Columna 5: saldo → Mapear a: Balance
```

**Mapeo correcto:**

| Archivo | Odoo | Tipo |
|---------|------|------|
| fecha | Date | Obligatorio |
| concepto | Reference | Obligatorio |
| debe | Debit Amount | Optativo |
| haber | Credit Amount | Optativo |
| saldo | Balance | Optativo |

```
Siguiente
```

## 🚀 Paso 4: Revisar Importación

```
Preview:
├─ 01/06/2026 | Ingreso cliente | 500.00 €
├─ 02/06/2026 | Pago proveedor | -300.00 €
└─ 03/06/2026 | Comisión banco | -2.00 €

Total: 3 movimientos
Saldo final: 198.00 €
```

Verificar:
- ✓ Fechas correctas
- ✓ Importes correctos
- ✓ Moneda correcta
- ✓ Saldo cuadra

```
Confirmar
```

## 🚀 Paso 5: Crear Extracto

```
Nuevo extracto creado:
ST/2026/001
├─ Diario: Banco Principal
├─ Fecha: 01/06/2026 - 03/06/2026
├─ Movimientos: 3
└─ Saldo inicial: 0.00
└─ Saldo final: 198.00 €
```

## 🚀 Paso 6: Reconciliar

```
Contabilidad → Extractos
→ Seleccionar ST/2026/001
→ Botón: Reconciliar
```

Interfaz muestra:

**Izquierda (Banco):**
- 01/06: Ingreso 500€
- 02/06: Pago 300€
- 03/06: Comisión 2€

**Derecha (Odoo):**
- Factura cliente: 500€ ✓ Match
- Factura proveedor: 300€ ✓ Match
- Comisión banco: 2€ ✓ Match

```
Todo reconciliado ✓
```

## ✅ Checklist

- [ ] Archivo CSV/XLSX descargado
- [ ] Columnas en formato correcto
- [ ] Archivo subido a Odoo
- [ ] Mapeo de columnas correcto
- [ ] Preview verificado
- [ ] Extracto creado
- [ ] Movimientos visibles
- [ ] Reconciliados

## 🚨 Troubleshooting

**Error: "Archivo no válido"**
```
→ Verificar extensión: .csv o .xlsx
→ Abrir con editor texto (CSV)
→ Comprobar delimitador (coma/punto y coma)
```

**Error: "Columna no reconocida"**
```
→ Verificar headers: fecha, concepto, etc
→ Sin tildes ni caracteres especiales
→ Nombres en minúsculas
```

**Error: "Importe inválido"**
```
→ Usar punto decimal: 500.00
→ No usar €: solo número
→ No usar espacios: 500,00 → 500.00
```

**Importes duplicados/faltantes**
```
→ Revisar rango: no incluya header
→ Verificar celdas vacías
→ Comprobar fórmulas Excel
```

**Saldo no cuadra**
```
→ Verificar saldo inicial
→ Revisar saldo final banco
→ Comprobar ausencia movimientos
```

## 📌 Tips

- Siempre hacer backup CSV
- Crear extracto de prueba primero
- Validar 3-5 movimientos manualmente
- Guardar mapeo para próximas importaciones
