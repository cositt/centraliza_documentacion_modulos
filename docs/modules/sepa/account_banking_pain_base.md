# account_banking_pain_base

Base para generación de archivos PAIN (ISO 20022).

## ¿Qué es?

Framework para crear archivos SEPA:

- Formato XML estándar ISO 20022
- Validación IBAN/BIC
- Generación ordenada
- Compatible con bancos

## Uso

Transparente - se usa en `account_payment_order` automáticamente.

## Archivo Generado

Formato PAIN:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Document>
  <CstmrCdtTrfInitn>
    <PmtInf>
      <Debtor>...</Debtor>
      <CdtTrfTxInf>
        <PmtId>...</PmtId>
        <Cdtr>...</Cdtr>
      </CdtTrfTxInf>
    </PmtInf>
  </CstmrCdtTrfInitn>
</Document>
```

## Ver También

- [account_banking_sepa_direct_debit](account_banking_sepa_direct_debit.md)
- [account_payment_order](../payment/account_payment_order.md)
