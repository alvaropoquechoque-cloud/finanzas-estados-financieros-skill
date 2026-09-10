# Finanzas Sommos — Cash Flow

## Propósito

Documentar la lógica del Cash Flow de Sommos.

Esta referencia pertenece a:

`finanzas-estados-financieros`

La pestaña principal es:

`Cash Flow`

La referencia histórica es:

`Cash Flow 2`

del antiguo Control.

---

# Pregunta que responde

Cash Flow debe responder:

**¿por qué cambió la caja entre el inicio y el cierre del periodo?**

---

# Método

El modelo utiliza principalmente una lógica de Cash Flow indirecto.

Puede mantener además una sección directa/de apoyo oculta.

No eliminar esa sección sin revisar dependencias.

---

# Fuente inicial

El Cash Flow parte principalmente de:

`Net Income`

de:

`Real P&L`

No hardcodear la utilidad de forma independiente.

---

# Cash at the beginning of the term

La caja inicial debe corresponder al cierre del periodo anterior.

En el modelo validado existe conexión con el Balance Sheet del mes anterior.

Conceptualmente:

`Cash beginning mes N = Cash Balance Sheet mes N-1`

Esto evita arrastrar diferencias internas de un Cash Flow incorrecto.

---

# Accounts Receivable

Cash Flow debe reconocer la variación del capital de trabajo.

No utilizar el saldo absoluto de CxC como flujo.

La lógica histórica utiliza el neto mensual correspondiente de clientes.

Conceptualmente:

`Cobros - Facturación`

con la convención de signo utilizada por el modelo.

Revisar siempre el signo.

---

# Accounts Payable

Debe incorporar correctamente la variación de:

- `CxP Mensual`
- `CxP Sueldos`

No utilizar únicamente pagos bancarios como ajuste de CxP.

La variación de saldo es la conexión correcta del método indirecto.

---

# CxP Sueldos

El modelo actual debe utilizar la variación del saldo de CxP Sueldos.

Evitar fórmulas especiales por mes cuando puede usarse el roll-forward correctamente.

---

# Grants

Los cobros de grants deben registrarse en la sección correspondiente según la metodología histórica.

Distinguir:

- devengo;
- saldo por cobrar;
- cobro real/forecast.

---

# Operating Cash Flow

Debe explicar el cash generado o consumido por la operación después de:

- Net Income;
- ajustes no cash;
- cambios de capital de trabajo.

No utilizar cash bancario bruto como sustituto de esta lógica.

---

# Investing Cash Flow

Cuando existan movimientos de inversión/capitalización, deben mantenerse separados de operación.

No inventar inversión únicamente porque exista capitalización contable.

---

# Financing Cash Flow

Puede contener:

- convertible;
- aportes;
- préstamos;
- financiamiento;
- otros movimientos financieros.

No mezclar financiamiento con revenue.

---

# Other

La línea `Other` puede conservar ajustes históricos documentados.

No utilizarla como plug.

Todo valor nuevo debe tener una explicación económica.

---

# Net change in cash

Conceptualmente:

`Net change = Operating CF + Investing CF + Financing CF`

según la estructura vigente.

---

# Cash at the end of the term

Conceptualmente:

`Cash ending = Cash beginning + Net change`

Debe reconciliar con:

`Balance Sheet Cash`

---

# Check cálculo CF

Debe verificar la propia aritmética del Cash Flow:

`Cash beginning + Net change - Cash ending`

Resultado esperado:

`≈ 0`

Este check no sustituye el check contra Balance.

---

# Check BG CASH

Debe comparar:

`Ending Cash Cash Flow`

vs:

`Cash Balance Sheet`

Resultado esperado:

`≈ 0`

Nunca construir este check comparando una celda del Cash Flow contra otra celda derivada del propio Cash Flow si la intención es validar Balance Sheet.

---

# Cash Flow directo

La sección directa puede utilizarse como control complementario.

Puede mostrar:

- cobros;
- pagos;
- grants;
- otros cash flows.

Aunque esté oculta:

no eliminarla automáticamente.

---

# Signos

Los signos del Cash Flow son críticos.

Antes de corregir una fórmula revisar:

- si un aumento de CxC consume cash;
- si un aumento de CxP genera cash;
- si el modelo ya incorpora el signo dentro de la fuente;
- si la fórmula vuelve a invertirlo.

No “corregir” un signo solo por intuición sin revisar el resultado completo.

---

# Forecast

Para forecast:

Cash Flow puede utilizar:

- cobros esperados;
- pagos esperados;
- CxC/CxP proyectados;
- grants;
- financiamiento;
- P&L forecast.

No exigir movimientos bancarios realizados.

---

# Histórico

Para histórico:

el cash final debe poder reconciliarse contra:

- Balance Sheet;
- Bancos.

No aceptar un Cash Flow que cierre internamente pero no coincida con caja real.

---

# Precisión

Pequeñas diferencias pueden surgir por:

- TC;
- históricos con muchos decimales;
- motores de cálculo.

No redondear prematuramente.

---

# QA

Después de modificar Cash Flow revisar:

- Cash beginning;
- Net Income;
- CxC;
- CxP;
- CxP Sueldos;
- grants;
- investing;
- financing;
- Other;
- Net Change;
- Cash Ending;
- Check cálculo CF;
- Check BG CASH.

---

# Regla final

Un Cash Flow correcto debe cumplir dos cosas:

1. explicar matemáticamente el cambio de caja;
2. terminar en la misma caja que muestra el Balance Sheet.
