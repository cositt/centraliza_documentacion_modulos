# l10n_es_account_banking_sepa_fsdd

FSDD (Anticipos de Crédito) - España.

## ¿Qué es?

Modalidad española de SEPA:

- Anticipos de crédito (FSDD)
- Adeudos recurrentes
- Plazos específicos España
- Normativa local

## Instalación

```
Aplicaciones → Buscar "SEPA FSDD Spain"
Instalar: l10n_es_account_banking_sepa_fsdd
```

## Configuración

### Payment Mode FSDD

```
Contabilidad → Modos de Pago
→ Nuevo

Name: FSDD España
Code: fsdd_es
Type: SEPA FSDD
Country: Spain
```

## Diferencias FSDD vs DD Estándar

| Aspecto | DD Estándar | FSDD |
|--------|------------|------|
| **Modalidad** | Adeudo directo | Anticipo crédito |
| **Plazo** | Flexible | 5 días |
| **Frecuencia** | Única/Recurrente | Recurrente |
| **Validación** | SEPA | España |
| **Uso** | Internacional | España |

## Ejemplo

```
Orden FSDD: FSDD-2026-001
├─ Fecha: 01/06/2026
├─ Plazo: 5 días hábiles
├─ Cliente: Empresa Madrid S.L.
├─ IBAN: ES9121000418450200051332
└─ Importe: 1.000€
```

## Troubleshooting

**P: Error validación España**
- R: Verificar país cliente = España

**P: IBAN no acepta**
- R: IBAN debe ser español (ES)

## Ver También

- [account_banking_sepa_direct_debit](account_banking_sepa_direct_debit.md)
- [account_banking_mandate](../payment/account_banking_mandate.md)
