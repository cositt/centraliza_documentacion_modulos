# Troubleshooting

Soluciones a problemas comunes.

## 🔴 Instalación

### "Module not found"

```
Error: AddonsNotFound: neo_extract_documents_hr_v19
```

**Solución:**
```
1. Verificar módulo existe en /custom-addons/
2. Ejecutar: odoo.py --addons-path=/path/to/addons
3. Recargar módulos: Aplicaciones → Actualizar Lista
```

### "Dependency error"

```
Error: Unmet dependency: account_payment_mode
```

**Solución:**
```
Instalar en orden correcto:
1. account_payment_mode
2. account_payment_order
3. account_banking_mandate
```

## 🔴 Pagos

### "IBAN no válido"

```
Error: Invalid IBAN format
```

**Solución:**
```
IBAN España: ES + 22 dígitos
Ejemplo: ES9121000418450200051332

Verificar:
- No espacios
- No guiones
- 24 caracteres total
```

### "Mandato expirado"

```
Error: Mandate expired or invalid
```

**Solución:**
```
1. Verificar fecha firma mandato
2. Crear nuevo mandato si cliente consiente
3. Usar mandato válido en orden pago
```

### "Factura no aparece en asistente"

```
Problema: Factura no se puede seleccionar
```

**Solución:**
```
Factura debe estar:
- Posted (validada)
- Sin pagar completamente
- Vencida o próxima vencer
- Same company
```

## 🔴 Extractos

### "Archivo no carga"

```
Error: File format not supported
```

**Solución:**
```
Formatos válidos:
✓ CSV (delimitador: coma o punto y coma)
✓ XLSX (Excel 2007+)
✗ PDF
✗ XLS (Excel 97-2003, convertir a XLSX)

Convertir:
Excel → Archivo → Guardar como → XLSX
```

### "Columnas no se mapean"

```
Error: Cannot detect columns
```

**Solución:**
```
Verificar encabezados (primera fila):
- fecha, concepto, debe, haber, saldo
- Sin espacios
- Sin tildes: concepto NOT concepto
- Minúsculas

Si no funciona:
Renombrar columnas A, B, C, D, E
Odoo pedirá mapeo manual
```

### "Importes se multiplican"

```
Problema: 500.00 → 5000.00
```

**Solución:**
```
Excel puede guardar números como:
500,00 (español) vs 500.00 (inglés)

Solución:
1. Exportar como CSV UTF-8
2. Abrir con Notepad
3. Verificar separador decimal
4. Guardar con mismo formato
```

## 🔴 Reconciliación

### "Movimientos no coinciden"

```
Problema: Banco 500€, Odoo 0€
```

**Solución:**
```
Verificar:
1. Extracto importado correctamente
2. Factura registrada en Odoo
3. Conceptos/referencias coinciden
4. Moneda igual
5. Importes exactos (sin comisiones extra)
```

### "Error al reconciliar"

```
Error: Reconciliation error occurred
```

**Solución:**
```
Revisar:
- Movimiento no esté ya reconciliado
- No reconciliar con movimiento de otra BD
- Saldo cuadre exactamente
- No hay movimientos bloqueados
```

## 🔴 Orden de Pago

### "Validación falla"

```
Error: Validation error on Payment Order
```

**Solución:**
```
Revisar:
✓ Al menos 1 línea de pago
✓ IBAN todos válidos
✓ Importes > 0
✓ Modo pago asignado
✓ Diario bancario existe
✓ Empresa activa
```

### "Archivo no descarga"

```
Problema: Botón "Generar archivo" no funciona
```

**Solución:**
```
1. Desactivar pop-up blocker navegador
2. Validar orden primero
3. Comprobar estado: debe estar "Open"
4. Verificar permisos usuario
5. Limpiar caché: Ctrl+F5
```

## 🔴 Domiciliaciones

### "Mandato no aparece en factura"

```
Problema: Campo mandato vacío
```

**Solución:**
```
1. Crear mandato primero
2. Cliente en mandato = Cliente factura
3. Mandato estado: Valid
4. Modo pago = SEPA Direct Debit
```

### "SEPA archivo rechazado"

```
Banco rechaza archivo PAIN
```

**Solución:**
```
Verificar en archivo XML:
- UMR único (no repetido)
- IBAN cliente español (ES + 22 dig)
- Empresa datos correctos
- Mandatos vigentes
- Tipo pago coincida
```

## 📞 Contacto Soporte

Si persiste error:

1. Revisar logs: `/var/log/odoo.log`
2. Copiar traceback completo
3. Mencionar:
   - Versión Odoo
   - Módulos instalados
   - Pasos para reproducir
