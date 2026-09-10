# Finanzas Sommos — Balance Sheet

## Propósito

Documentar la lógica del Balance Sheet de Sommos.

Esta referencia pertenece a:

`finanzas-estados-financieros`

La pestaña principal es:

`Balance Sheet`

La referencia histórica es:

`Balance Sheet 2`

del antiguo Control.

---

# Pregunta que responde

El Balance Sheet debe responder:

**¿qué posee, qué debe y qué patrimonio tiene Sommos al cierre de cada mes?**

Representa saldos.

No movimientos.

---

# Ecuación fundamental

Debe cumplirse:

`Assets = Liabilities + Equity`

El check:

`Assets - Liabilities - Equity`

debe ser:

`≈ 0`

---

# Fuentes principales

El Balance utiliza principalmente:

- `Bancos`
- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`
- `Real P&L`
- información de financiamiento;
- capitalización / IP;
- saldos históricos.

---

# Cash

Para periodos históricos conciliados:

la caja debe poder rastrearse hasta:

`Bancos`

No utilizar Cash Flow como sustituto de una conciliación bancaria.

---

# Cash por país

El modelo puede separar la caja por:

- Bolivia;
- Perú;
- Chile;
- Estados Unidos;
- otros países vigentes.

La suma de cash por país debe representar la caja consolidada correspondiente.

La clasificación depende de dónde está la cuenta, no de dónde ocurrió el gasto.

---

# Cuentas bancarias

No asumir que cada línea del Balance corresponde a una única cuenta bancaria.

Puede existir agrupación por:

- país;
- tipo de cuenta;
- clasificación contable.

Pero el total debe reconciliar con Bancos.

---

# Accounts Receivable

El saldo debe provenir de:

`CxC Mensual`

No utilizar:

- revenue;
- cobros;
- monto facturado del mes;

como saldo directamente.

El saldo ya incorpora:

`Saldo anterior + Devengo - Cobro`

---

# Grants receivable

Mantener separados cuando el modelo así lo presenta.

No reconocer el monto aprobado total como activo.

Utilizar solamente el saldo exigible pendiente.

---

# IP / Software

El activo relacionado con capitalización debe respetar la lógica de:

`Capitalizacion de desarrollo IP`

del P&L.

Conceptualmente puede seguir:

`Saldo inicial + Altas - Amortización`

según el modelo vigente.

No duplicar el efecto.

---

# Accounts Payable

Debe utilizar saldos desde:

`CxP Mensual`

No utilizar gasto devengado del mes como si fuera saldo final.

---

# CxP Sueldos

Debe provenir directamente de:

`CxP Sueldos`

cuando la fuente ya contiene el saldo correcto.

No crear ajustes paralelos en Balance Sheet para compensar diferencias de nómina.

---

# Interés de convertible

Existe una línea específica para el interés del convertible.

Por ello:

no incluir nuevamente ese importe dentro de CxP general cuando genere doble conteo.

---

# Financing payable

Mantener separadas las obligaciones financieras de las obligaciones operativas cuando así lo define el modelo.

---

# Convertible

El principal del convertible debe conservar su línea correspondiente.

No mezclar:

- principal;
- interés;
- capital.

---

# Equity

Puede contener:

- capital aportado;
- retained earnings;
- otras cuentas patrimoniales.

La estructura debe conservar continuidad entre meses.

---

# Retained earnings

Debe estar conectado al resultado acumulado.

No hardcodear retained earnings para hacer cerrar el Balance.

Si existe una diferencia:

revisar primero:

- P&L;
- saldos iniciales;
- patrimonio histórico;
- periodos acumulados.

---

# Resultado acumulado

El Balance debe tener un check contra:

`Real P&L`

La utilidad acumulada debe coincidir con la evolución de patrimonio según la metodología del modelo.

---

# Forecast de caja

En periodos futuros, el antiguo `Balance Sheet 2` utiliza una lógica específica para hacer cerrar el forecast.

Esta metodología debe preservarse mientras sea la política vigente.

Importante:

una línea de cierre explícita del modelo histórico no debe confundirse con un plug arbitrario.

Antes de cambiarla revisar:

- Cash Flow;
- supuestos;
- capital de trabajo;
- financiamiento;
- patrimonio.

---

# Histórico

Los saldos históricos deben estar reconciliados contra:

- Bancos;
- CxC;
- CxP;
- P&L;
- Control antiguo.

No cambiar históricos cerrados silenciosamente.

---

# Check principal

Conceptualmente:

`Check Act-Ps-Pat = Total Assets - Total Liabilities - Equity`

La expectativa es:

`≈ 0`

Pequeños residuos de precisión pueden existir.

Toda diferencia material debe investigarse.

---

# Check de utilidad

Debe comprobar que el resultado acumulado del Balance sea consistente con:

`Real P&L`

La expectativa es:

`0`

---

# No usar plugs

No introducir:

- Other Asset;
- Other Liability;
- Equity adjustment;

solo para cerrar el Balance.

Si existe una cuenta real de esa naturaleza:

debe documentarse.

---

# Orden de investigación

Si el Balance no cierra:

1. revisar fórmula del check;
2. revisar Cash;
3. revisar CxC;
4. revisar CxP;
5. revisar CxP Sueldos;
6. revisar IP;
7. revisar financiamiento;
8. revisar interés convertible;
9. revisar retained earnings;
10. revisar P&L acumulado;
11. revisar saldos iniciales;
12. revisar precisión.

---

# Relación con Cash Flow

Debe cumplirse:

`Cash Balance Sheet ≈ Ending Cash Cash Flow`

Este es uno de los checks principales del modelo.

---

# QA

Después de modificar Balance Sheet revisar:

- Cash;
- CxC;
- grants receivable;
- IP;
- CxP;
- CxP Sueldos;
- financiamiento;
- convertible;
- interés;
- patrimonio;
- retained earnings;
- Total Assets;
- Total Liabilities + Equity;
- check principal;
- check de utilidad;
- Cash Flow.

---

# Regla final

El Balance Sheet no debe cerrar porque se agregó una diferencia.

Debe cerrar porque todos sus activos, pasivos y patrimonio están correctamente calculados.
