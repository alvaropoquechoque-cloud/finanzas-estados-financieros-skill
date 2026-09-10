# Finanzas Sommos — Real P&L

## Propósito

Documentar la lógica del estado de resultados de Sommos.

Esta referencia pertenece a:

`finanzas-estados-financieros`

La pestaña principal es:

`Real P&L`

---

# Pregunta que responde

`Real P&L` debe responder:

**¿qué ingresos y gastos corresponden económicamente a cada periodo?**

Trabaja principalmente bajo lógica de devengo.

No debe confundirse con:

- cash recibido;
- pagos realizados;
- saldos bancarios.

---

# Fuentes principales

## Ingresos

Fuente:

`Operative incomes`

## Gastos operativos

Fuente:

`Real S&A`

## Salarios

Fuente:

`Sueldos 2026`

## Partidas financieras y contables

Pueden provenir de:

- fuentes específicas del modelo;
- históricos validados;
- inputs explícitos;
- reglas del antiguo Control.

No utilizar `Transacciones` como sustituto general del devengo.

---

# Arquitectura

Conceptualmente:

`Operative incomes`
+
`Real S&A`
+
`Sueldos 2026`
+
partidas contables/financieras

→ `Real P&L`

---

# Ingresos operativos

Entre las líneas conocidas se encuentran:

- Full new integration incomes
- Full Integration monthly maintenance fee
- Proof of concept incomes
- Transactions Fee
- Extra features development income
- Others
- Operative incomes

Los importes deben venir de `Operative incomes`.

No utilizar cobros bancarios como revenue del mes.

---

# Costos directos

Pueden incluir:

- IT salaries
- Platform cost
- Softwares for development
- Sales cost
- Fletes

La composición exacta debe conservar la metodología validada del modelo.

No reclasificar automáticamente un gasto entre costo directo y SG&A.

---

# Gross Margin

Conceptualmente:

`Gross Margin = Operative incomes - costos directos`

El margen:

`Gross Margin % = Gross Margin / Operative incomes`

No hardcodear Gross Margin.

Debe derivarse de las líneas anteriores.

---

# Gastos operativos

Entre las líneas conocidas pueden aparecer:

- RH expenses
- Administrative expenses
- Sales expenses
- Product expenses
- Startup Chile
- Bank fees
- Travel
- Innovatech
- Contingency
- Operative salaries
- Marketing services
- Outsourced services
- Finance Salary
- RH Salary
- Sales salaries
- Operative expenses

La fuente principal es:

- `Real S&A`
- `Sueldos 2026`

según el concepto.

---

# SG&A

El modelo mantiene una línea:

`SG&A (%)`

Debe conservar la definición utilizada por el Control.

No redefinirla únicamente porque otra metodología sea más estándar.

Primero preservar la lógica validada del modelo.

---

# Grants

Los grants se presentan separadamente de los ingresos operativos.

Línea conocida:

`Otros ingresos Grants`

No mezclar grants con:

`Operative incomes`

sin una decisión explícita.

---

# Otros ingresos extraordinarios

Mantener separados de:

- revenue operativo;
- grants;
- financiamiento.

No utilizar esta línea como plug para llegar a una utilidad objetivo.

---

# Capitalización de desarrollo IP

Existe una línea:

`Capitalizacion de desarrollo IP`

Esta puede ser:

- input;
- supuesto contable;
- reclasificación.

No calcularla automáticamente desde cash.

Tiene impacto simultáneo en:

- Real P&L;
- Balance Sheet.

Toda modificación debe revisarse en ambos.

---

# EBIT

Debe derivarse de la estructura operacional del P&L.

No hardcodear.

---

# Margen operativo

La línea:

`Margen Operativo %`

debe calcularse con la metodología vigente.

Preservar la misma base de cálculo utilizada por el Control.

---

# Financial income

Puede incluir conceptos como:

`Bank interest earned`

No mezclar con revenue operativo.

---

# Financial expense

Debe mantenerse separado de:

- Bank fees;
- Taxes;
- Exchange rate differences.

---

# Exchange rate differences

Puede ser una partida contable que no corresponda a un único movimiento bancario.

No exigir una relación cash uno-a-uno.

---

# Utilidad antes de impuestos

Línea conocida:

`Ut. Antes de IR`

Debe derivarse de:

- EBIT;
- resultado financiero;
- diferencias de cambio;
- otros elementos de la metodología vigente.

---

# Taxes

No utilizar únicamente pagos bancarios de impuestos para definir el gasto fiscal del mes.

El tratamiento debe respetar el devengo validado.

---

# Net Revenue Con Grant

Debe incluir los elementos definidos por el Control antiguo.

No modificar la fórmula sin revisar:

- grants;
- ingresos extraordinarios;
- impuestos;
- resultado financiero.

---

# Net Revenue Sin Grant

Debe permitir observar el resultado excluyendo grants según la metodología del modelo.

Es especialmente útil para evaluar la sostenibilidad operativa.

---

# D&A

La depreciación/amortización debe respetar la política contable vigente.

No inventar D&A a partir de la caja.

---

# EBITDA

Mantener la definición exacta utilizada por el modelo.

No asumir una fórmula estándar si el Control utiliza una construcción específica.

---

# Checks internos

Existen checks como:

- Check Operative incomes normal
- Check Operative incomes Grants
- Check Budget TH
- Check S&A

La expectativa es:

`0`

o una diferencia técnica conocida y documentada.

No esconder ni borrar checks que fallen.

---

# Histórico

Los valores históricos deben preservar la conciliación contra el antiguo `Real P&L`.

No reemplazar históricos validados con nuevas fórmulas si cambia el resultado sin justificación.

---

# Forecast

Los meses futuros se alimentan de:

- Operative incomes forecast;
- Real S&A forecast;
- Sueldos;
- grants;
- supuestos explícitos.

No inventar forecast para completar celdas vacías.

---

# Formato

Preservar el lenguaje visual del Control antiguo:

- encabezado morado;
- actual celeste;
- forecast gris;
- filas de margen resaltadas;
- negativos entre paréntesis;
- subtotales en negrita;
- checks visibles;
- columnas históricas ocultas cuando corresponda.

El formato no debe alterar las fórmulas.

---

# QA

Después de modificar P&L revisar:

- ingresos;
- costos;
- Gross Margin;
- salarios;
- S&A;
- SG&A;
- grants;
- capitalización;
- EBIT;
- resultado financiero;
- impuestos;
- Net Revenue;
- EBITDA;
- checks.

Buscar:

- `#REF!`
- `#VALUE!`
- `#DIV/0!`
- `#N/A`
- `#ERROR!`

---

# Regla final

Un P&L correcto debe mostrar:

**el resultado económico del periodo**

independientemente de cuándo se haya cobrado o pagado el cash.
