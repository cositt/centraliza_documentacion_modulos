# Referencia API - Modelos y Campos

Documentación técnica de modelos principales.

## account_payment_order

### Modelo: account.payment.order

**Campos principales:**

```python
name = Char(required=True)               # PO-2026-001
date = Date()                             # Fecha creación
payment_type = Selection()                # electronic, manual, check
journal_id = Many2one('account.journal')  # Diario bancario
mode_id = Many2one('account.payment.mode') # Modo pago
state = Selection()                       # draft, open, done, cancel
```

**Métodos:**

```python
def button_validate()               # Valida orden
def generate_payment_file()         # Genera XML SEPA
def reconciliation_mark_done()      # Marca como hecha
```

### Modelo: account.payment.line

**Campos:**

```python
order_id = Many2one('account.payment.order')
partner_id = Many2one('res.partner')
amount = Float()                    # Importe
partner_bank_id = Many2one('res.partner.bank')
move_line_id = Many2one('account.move.line')
date = Date()                       # Vencimiento
reference = Char()                  # Referencia pago
```

## account_banking_mandate

### Modelo: account.banking.mandate

**Campos:**

```python
name = Char(required=True)          # MANDATE-001
partner_id = Many2one('res.partner', required=True)
partner_bank_id = Many2one('res.partner.bank')
signature_date = Date()             # Fecha firma
type = Selection([('OOF', 'One off'), ('RC', 'Recurrent')])
state = Selection()                 # draft, valid, expired, cancelled
unique_mandate_reference = Char()   # UMR SEPA
```

## account_reconcile_oca

### Modelo: account.reconcile.model

**Campos:**

```python
name = Char(required=True)
rule_type = Selection()             # account_line, invoice
auto_reconcile = Boolean()
matching_fields = Many2many()
```

**Métodos:**

```python
def _reconciliation_matches()       # Calcula matches
```

## account_statement_import_sheet_file

### Wizard: account.statement.import.sheet.mapping

**Campos:**

```python
name = Char()
column_ids = One2many()             # Mapeo columnas
mapping_line_ids = One2many()       # Líneas mapeo
```

**Ejemplo mapeo CSV:**

```python
mapping_lines = [
    {
        'csv_column': 'fecha',
        'odoo_field': 'date'
    },
    {
        'csv_column': 'concepto',
        'odoo_field': 'reference'
    },
    {
        'csv_column': 'debe',
        'odoo_field': 'amount_debit'
    }
]
```

## Flujos XML SEPA

### PAIN-008 (Domiciliación)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Document xmlns="urn:iso:std:iso:20022:tech:xsd:pain.008.003.02">
  <CstmrDrctDbtInitn>
    <GrpHdr>
      <MsgId>MSG-001</MsgId>
      <CreDtTm>2026-06-01T10:00:00</CreDtTm>
      <NbOfTxns>1</NbOfTxns>
      <CtrlSum>500.00</CtrlSum>
    </GrpHdr>
    <PmtInf>
      <PmtInfId>PI-001</PmtInfId>
      <PmtMtd>DD</PmtMtd>
      <Dbtr>
        <Nm>Mi Empresa S.L.</Nm>
      </Dbtr>
      <DbtrAcct>
        <Id>
          <IBAN>ES9121000418450200051332</IBAN>
        </Id>
      </DbtrAcct>
      <DbtrAgt>
        <FinInstnId>
          <BIC>BBVAESMM</BIC>
        </FinInstnId>
      </DbtrAgt>
      <DrctDbtTxnInf>
        <PmtId>
          <InstrId>PROV/2026/001</InstrId>
          <EndToEndId>E2E-001</EndToEndId>
        </PmtId>
        <Cdtr>
          <Nm>Proveedor S.L.</Nm>
        </Cdtr>
        <CdtrAcct>
          <Id>
            <IBAN>ES9100000000000000000001</IBAN>
          </Id>
        </CdtrAcct>
        <Amt>
          <InstdAmt Ccy="EUR">500.00</InstdAmt>
        </Amt>
        <Mndtinfo>
          <MndtId>MANDATE-001</MndtId>
          <DtOfSgntr>2026-06-01</DtOfSgntr>
          <AmdmntInd>false</AmdmntInd>
        </Mndtinfo>
      </DrctDbtTxnInf>
    </PmtInf>
  </CstmrDrctDbtInitn>
</Document>
```

## Eventos/Hooks

### Pre-init Hook

```python
def pre_init_hook(cr):
    """Antes de instalar"""
    pass
```

### Post-init Hook

```python
def post_init_hook(cr, registry):
    """Después de instalar"""
    pass
```

## Transiciones Estado

### Payment Order

```
Draft
  ↓
Open (validación)
  ↓
Done (enviado banco)
  ↓
Cancelled (anulado)
```

### Banking Mandate

```
Draft
  ↓
Valid (autorizado)
  ↓
Expired / Cancelled
```
