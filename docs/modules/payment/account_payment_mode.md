# account_payment_mode

Configuración de modos de pago (transferencia, domiciliación, cheque, etc).

## ¿Qué es?

Define **cómo se pagan** las facturas:

- Transferencia bancaria
- Domiciliación SEPA
- Cheque
- Pago manual
- Descuento pronto pago

## Instalación

```
Aplicaciones → Buscar "Payment Mode"
Instalar: account_payment_mode
```

## Configuración

### 1. Crear Modo de Pago

```
Contabilidad → Configuración → Modos de Pago
→ Nuevo
```

**Campos principales:**

| Campo | Ejemplo |
|-------|---------|
| **Name** | Transferencia SEPA |
| **Code** | transfer_sepa |
| **Payment Type** | Electronic |
| **Bank Account** | ES91 2100 0418 4502 0005 1332 |

### 2. Asignar a Empresas

```
Pestaña: Empresa
→ Seleccionar empresa
→ Guardar
```

### 3. Vincular a Métodos de Pago

```
Pestaña: Payment Method
→ Agregar línea
→ Seleccionar método (SEPA Transfer, etc)
→ Guardar
```

## Uso

### En Factura de Proveedor

1. Abrir factura
2. Campo "Payment Mode" → Seleccionar
3. Al crear pago → usa este modo

### En Factura de Cliente

1. Abrir factura
2. "Expected Payment Mode" → Seleccionar
3. Cliente paga por ese medio

## Ejemplo Real

```
Modo: "Transferencia SEPA"
├─ Banco: BBVA
├─ Cuenta: ES91 2100 0418 4502 0005 1332
├─ Empresa: Mi Empresa S.L.
└─ Método: SEPA Credit Transfer
```

Cuando creas orden de pago con este modo:
- Genera archivo PAIN
- Incluye datos banco correctos
- IBAN precompletado

## Campos Avanzados

### Instruction Priority

```
Normal     → Pago en 3-5 días
High       → Pago en 1 día
Very High  → Pago mismo día
```

### Applicable for

```
- B2B: pago empresa a empresa
- B2C: pago empresa a consumidor
- Ambos
```

## Relaciones

```
account_payment_mode
    ├─ account_payment_order
    ├─ account_move_line
    └─ res_partner_bank
```

## Troubleshooting

**P: Modo no aparece en factura**
- R: Asegurar está asignado a empresa

**P: Error "No payment method"**
- R: Agregar payment method a la pestaña

**P: IBAN no valida**
- R: Verificar formato IBAN (ES + 22 dígitos)

## Ver También

- [account_payment_order](account_payment_order.md)
- [account_banking_mandate](account_banking_mandate.md)
