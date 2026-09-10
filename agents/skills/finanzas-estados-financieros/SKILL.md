---
name: finanzas-estados-financieros
description: Construye, mantiene y audita los tres estados financieros de Sommos — Real P&L, Balance Sheet y Cash Flow — preservando la lógica de devengo, capital de trabajo, caja, patrimonio y checks cruzados del modelo financiero.
---

# Finanzas Sommos — Estados Financieros

## Propósito

Gestionar la capa de estados financieros del workflow financiero de Sommos.

Esta skill opera principalmente sobre:

- `Real P&L`
- `Balance Sheet`
- `Cash Flow`

Su objetivo es asegurar que los tres estados:

- utilicen las fuentes correctas;
- mantengan la lógica contable validada;
- estén conectados entre sí;
- reproduzcan la metodología del Control antiguo;
- cierren mediante checks financieros reales;
- no dependan de plugs arbitrarios;
- puedan actualizarse mes a mes sin romper el modelo.

---

# Archivo principal

Google Sheet:

`Finanzas Sommos — Workflow y Control`

Spreadsheet ID:

`1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`

URL:

`https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

---

# Modelo de referencia histórico

Los estados nuevos fueron construidos tomando como referencia directa las pestañas del antiguo Control financiero:

- `Real P&L`
- `Balance Sheet 2`
- `Cash Flow 2`

La lógica del modelo nuevo fue reconciliada contra esos estados.

Cuando exista una duda sobre una fórmula histórica:

1. revisar primero la fórmula viva del nuevo modelo;
2. revisar sus fuentes;
3. comparar con el Control antiguo;
4. identificar si la diferencia es:
   - económica;
   - contable;
   - de precisión;
   - de motor Excel vs Google Sheets.

No cambiar una fórmula únicamente porque tenga una forma diferente al Excel antiguo si produce correctamente la misma lógica financiera.

---

# Principio fundamental

Los tres estados representan conceptos distintos.

## Real P&L

Responde:

**¿qué ingresos y gastos corresponden al periodo?**

Opera principalmente bajo lógica de devengo.

## Balance Sheet

Responde:

**¿qué posee, debe y ha acumulado Sommos al cierre del periodo?**

Representa saldos.

## Cash Flow

Responde:

**¿cómo cambió la caja durante el periodo?**

Representa movimientos de cash y variaciones de balance.

No mezclar estas tres preguntas.

---

# Arquitectura general

Las principales dependencias son:

`Operative incomes`
→ ingresos devengados

`Real S&A`
→ gastos operativos devengados

`Sueldos 2026`
→ salarios devengados

Luego:

`Operative incomes + Real S&A + Sueldos 2026`
→ `Real P&L`

Mientras que:

`Operative incomes + Transacciones`
→ `CxC Mensual`

`Real S&A + Transacciones`
→ `CxP Mensual`

`Sueldos 2026`
→ `CxP Sueldos`

Y:

`Bancos + CxC + CxP + CxP Sueldos + Real P&L + financiamiento`
→ `Balance Sheet`

Finalmente:

`Real P&L + variaciones de Balance + financiamiento`
→ `Cash Flow`

con control cruzado entre:

`Cash Flow ↔ Balance Sheet`

---

# Evitar circularidad

Balance Sheet y Cash Flow están relacionados, pero no deben crear referencias circulares.

Antes de modificar fórmulas entre ambos:

1. identificar qué estado contiene la fuente económica;
2. identificar qué celda funciona solamente como check;
3. preservar el sentido de dependencia vigente;
4. comprobar que no aparezca una referencia circular.

Nunca arreglar un check creando una fórmula donde Cash Flow dependa de Balance y Balance dependa de la misma celda de Cash Flow.

---

# Real P&L

## Propósito

`Real P&L` presenta el desempeño económico mensual de Sommos.

Distingue:

- ingresos;
- costos;
- margen bruto;
- gastos operativos;
- grants;
- otros ingresos;
- capitalización;
- EBIT;
- resultado financiero;
- impuestos;
- resultado neto;
- EBITDA.

---

# Fuente de ingresos del P&L

Las líneas de ingreso operativo deben provenir principalmente de:

`Operative incomes`

No construir revenue desde:

- cobros de Transacciones;
- saldo de CxC;
- caja bancaria.

Un cobro no determina el periodo de revenue.

---

# Líneas de ingreso conocidas

La estructura validada incluye líneas como:

- Full new integration incomes
- Full Integration monthly maintenance fee
- Proof of concept incomes
- Transactions Fee
- Extra features development income
- Others

Luego:

`Operative incomes`

como subtotal.

La estructura viva prevalece.

---

# Costos y gastos

`Real S&A` alimenta principalmente los gastos operativos correspondientes.

Entre las líneas conocidas se encuentran:

- Platform cost
- Softwares for development
- Sales cost
- Fletes
- RH expenses
- Administrative expenses
- Sales expenses
- Product expenses
- Startup Chile
- Bank fees
- Travel
- Innovatech
- Contingency
- Marketing services
- Outsourced services

No reconstruir estos gastos desde movimientos bancarios.

---

# Salarios

Los salarios deben provenir principalmente de:

`Sueldos 2026`

Entre las líneas conocidas:

- IT salaries
- Operative salaries
- Finance Salary
- RH Salary
- Sales salaries

No reconocer nuevamente el gasto cuando se realiza el pago.

---

# Gross Margin

Conceptualmente:

`Gross Margin = Operative incomes - Costos directos`

El porcentaje:

`Gross Margin % = Gross Margin / Operative incomes`

Respetar la definición vigente del modelo.

No cambiar qué líneas forman parte de costo directo sin una decisión contable explícita.

---

# SG&A

La línea de SG&A debe conservar la composición validada del modelo.

No utilizar automáticamente todos los egresos bancarios como SG&A.

SG&A trabaja sobre gasto devengado.

---

# Grants

Los grants se mantienen separados de los ingresos operativos ordinarios.

En el P&L pueden aparecer como:

`Otros ingresos Grants`

No mezclarlos con:

`Operative incomes`

salvo decisión contable explícita.

---

# Otros ingresos extraordinarios

Mantener separados de revenue operativo y grants.

No utilizar esta línea como plug para conseguir un resultado esperado.

---

# Capitalización de desarrollo IP

`Capitalizacion de desarrollo IP`

es una partida contable específica del modelo.

Puede requerir:

- supuesto;
- input;
- política contable;
- reclasificación desde gasto a activo.

No inventar capitalización automáticamente a partir de movimientos de banco.

Esta partida impacta tanto:

- P&L;
- Balance Sheet.

Por ello cualquier modificación debe revisarse en ambos.

---

# EBIT

Conceptualmente representa el resultado operativo después de la estructura de ingresos y gastos definida por el modelo.

No hardcodear EBIT.

Debe derivarse de sus líneas subyacentes.

---

# Resultado financiero

Mantener diferenciados:

- Financial income
- Financial expense
- Exchange rate differences

No mezclar:

- interés;
- comisión bancaria;
- diferencia cambiaria.

---

# Taxes

Los impuestos del P&L deben seguir la metodología contable validada.

No derivarlos automáticamente del cash fiscal del mes.

---

# Net Revenue / Net Income

El resultado neto es una de las principales conexiones hacia Balance Sheet.

La acumulación de resultados en patrimonio debe reconciliar con el P&L.

No hardcodear retained earnings independientemente del resultado.

---

# EBITDA

Debe mantener la definición vigente del Control.

No asumir que EBITDA es simplemente Net Income + D&A sin revisar otras líneas si el modelo vigente utiliza una estructura distinta.

Preservar la fórmula validada.

---

# Checks del P&L

El P&L mantiene controles internos para validar sus fuentes.

Entre los checks existentes:

- Check Operative incomes normal
- Check Operative incomes Grants
- Check Budget TH
- Check S&A

La expectativa es:

`Check = 0`

o dentro de una tolerancia técnica conocida cuando corresponda.

No eliminar un check porque muestre una diferencia.

Investigar la fuente.

---

# Balance Sheet

## Propósito

`Balance Sheet` representa la posición financiera de Sommos al cierre de cada mes.

La ecuación fundamental es:

`Assets = Liabilities + Equity`

---

# Activos

Pueden incluir principalmente:

- Cash
- Accounts Receivable
- Grants receivable
- Software / IP capitalizado
- otras cuentas según el modelo

La estructura viva prevalece.

---

# Cash

Para meses históricos conciliados:

Cash debe provenir principalmente de:

`Bancos`

La caja debe poder rastrearse hasta los extractos conciliados.

No utilizar el saldo del Cash Flow como sustituto de una conciliación bancaria histórica.

---

# Cash por país

El Balance puede separar cash por país.

Preservar la clasificación validada.

La suma de las líneas de cash debe representar la caja consolidada correspondiente.

---

# Forecast de Cash

Para meses futuros, la caja puede depender del mecanismo de forecast validado del modelo.

El antiguo `Balance Sheet 2` utiliza una lógica particular para hacer cerrar la proyección.

No eliminar ni reemplazar esa metodología sin entender primero:

- Cash Flow;
- activos;
- pasivos;
- patrimonio;
- supuestos futuros.

No crear circularidad.

---

# Accounts Receivable

El saldo debe provenir de:

`CxC Mensual`

No utilizar revenue del P&L directamente como saldo de CxC.

Distinguir:

- devengo;
- cobro;
- saldo.

---

# Grants por cobrar

Mantener separados cuando el modelo así los presenta.

No incluir todo el monto aprobado de un grant como activo.

Utilizar únicamente el saldo que corresponda según la lógica validada de CxC/grants.

---

# Software / IP

El activo relacionado con IP debe estar conectado a la lógica de capitalización.

Conceptualmente:

`Saldo activo nuevo = saldo anterior + capitalización - amortización/depreciación`

según la metodología vigente.

No duplicar el impacto entre P&L y Balance.

---

# Accounts Payable

El Balance debe utilizar los saldos finales correspondientes de:

`CxP Mensual`

No utilizar los gastos del P&L como saldo de pasivo.

---

# CxP Sueldos

Debe provenir de:

`CxP Sueldos`

No crear ajustes paralelos en Balance Sheet cuando la fuente ya contiene el saldo correcto.

---

# Interés del convertible

El modelo histórico presenta el interés del convertible separadamente.

Por lo tanto:

no duplicarlo dentro de CxP general si ya existe una línea específica.

Revisar siempre el tratamiento vigente antes de modificar.

---

# Financing payable

Las obligaciones de financiamiento deben mantenerse separadas de proveedores operativos cuando la estructura del Balance así lo define.

---

# Convertible

El saldo principal del financiamiento convertible debe mantener su propia línea según el modelo validado.

No confundir:

- principal;
- interés;
- equity.

---

# Equity

Puede incluir:

- capital;
- retained earnings;
- resultados acumulados;
- otras cuentas patrimoniales.

La estructura debe mantener continuidad entre periodos.

---

# Retained Earnings

Los resultados acumulados deben reconciliar con la utilidad neta histórica.

Conceptualmente:

`Retained Earnings cierre = Retained Earnings apertura + resultado acumulado`

según la metodología específica del modelo.

No hardcodear retained earnings para cuadrar el Balance.

---

# Check Balance Sheet

El principal check es:

`Total Assets - Total Liabilities - Total Equity`

La expectativa es:

`≈ 0`

Pueden existir residuos históricos inferiores a un centavo derivados de precisión.

No tratar automáticamente cualquier residuo como error material.

Pero siempre identificar su origen antes de aceptar una tolerancia.

---

# Check de resultados acumulados

El Balance debe comprobar que la utilidad acumulada sea consistente con:

`Real P&L`

La expectativa es:

`Check = 0`

No eliminar este control.

---

# Cash Flow

## Propósito

`Cash Flow` explica el cambio de caja de Sommos durante cada periodo.

El modelo utiliza principalmente el método indirecto y mantiene además una sección de apoyo/directa según la estructura heredada del Control.

---

# Cash at the beginning of the term

La caja inicial de un periodo debe corresponder al cierre del periodo anterior según la lógica validada.

Conceptualmente:

`Cash beginning mes N = Cash ending mes N-1`

En el modelo actual existe además conexión con la caja del Balance Sheet del periodo anterior.

Preservar esa conexión.

---

# Net Income

El Cash Flow debe comenzar desde la utilidad neta correspondiente de:

`Real P&L`

No hardcodear Net Income independientemente.

---

# Accounts Receivable en Cash Flow

Cash Flow utiliza la variación de capital de trabajo.

No utilizar simplemente el saldo total de CxC como movimiento.

Debe reflejar el cambio correspondiente según la metodología validada.

La lógica histórica utiliza el neto mensual de clientes:

`Cobros - Facturación`

con la convención de signo utilizada por el Cash Flow.

Preservar la estructura vigente.

---

# Accounts Payable en Cash Flow

Debe representar la variación correspondiente de:

- CxP proveedores;
- CxP Sueldos.

El modelo actual conecta CxP Sueldos mediante la variación del saldo correspondiente del Balance/CxP, evitando excepciones manuales por mes.

No volver a introducir fórmulas especiales para un mes si puede expresarse correctamente mediante el roll-forward.

---

# Grants

Los cobros de grants deben entrar en la sección correspondiente del Cash Flow según la metodología validada.

No confundir:

- grant devengado;
- grant por cobrar;
- grant efectivamente cobrado.

---

# Financing

Los movimientos de financiamiento pueden incluir:

- préstamos;
- convertible;
- aportes;
- otras entradas/salidas financieras.

No mezclarlos con cash operativo.

---

# Other

El antiguo Control puede contener ajustes históricos en líneas como `Other`.

No utilizar `Other` como plug general.

Cuando exista un valor histórico:

- identificar su origen;
- preservar la compatibilidad cuando sea necesario;
- documentar partidas que no tengan correspondencia uno-a-uno en Transacciones.

No inventar nuevos ajustes bajo `Other`.

---

# Cash at the end of the term

Conceptualmente:

`Cash ending = Cash beginning + Net change in cash`

Debe reconciliar con la caja del Balance Sheet.

---

# Check cálculo CF

El Cash Flow puede contener un control interno:

`Caja inicial + variación - caja final`

La expectativa es:

`≈ 0`

Este check valida aritmética interna.

No sustituye el control contra Balance Sheet.

---

# Check BG CASH

Debe comparar realmente:

`Cash Flow ending cash`

contra:

`Balance Sheet cash`

La expectativa es:

`≈ 0`

No convertir este check en una fórmula que compare el Cash Flow consigo mismo.

---

# Sección Cash Flow Directo

El modelo puede mantener una sección directa/de apoyo oculta.

Aunque no sea la presentación principal:

- no eliminarla sin revisar dependencias;
- preservar sus fórmulas si funciona como control;
- comprobar signos de cobros/pagos.

---

# Modelo de tres estados

El modelo debe poder recorrer conceptualmente:

`P&L`
→ resultado económico

`Balance Sheet`
→ saldos

`Cash Flow`
→ cambio de caja

y volver a comprobar:

`Cash Flow Ending Cash ≈ Balance Sheet Cash`

Este cierre cruzado es obligatorio.

---

# Tolerancias

Pueden existir residuos pequeños por:

- Excel vs Google Sheets;
- precisión de TC;
- valores históricos con muchos decimales;
- presentación redondeada.

No utilizar una tolerancia para esconder una diferencia material.

Toda diferencia debe clasificarse como:

- exacta;
- técnica conocida;
- material/error.

---

# Histórico vs Forecast

Distinguir siempre:

## Histórico

Debe poder rastrearse a:

- devengo validado;
- CxC/CxP;
- bancos conciliados;
- Control histórico.

## Forecast

Puede utilizar:

- Operative incomes futuro;
- Real S&A futuro;
- Sueldos;
- grants;
- presupuesto;
- financiamiento;
- otros supuestos aprobados.

No exigir evidencia bancaria para un forecast.

---

# 2025 histórico

Los estados nuevos pueden contener bloques históricos 2025 ocultos para preservar continuidad con el antiguo Control.

No eliminar columnas ocultas sin revisar fórmulas.

Oculto no significa innecesario.

---

# 2026

2026 es el bloque principal vivo del modelo.

Actualmente incluye:

- meses históricos;
- meses forecast.

La frontera real/forecast debe mantenerse clara.

---

# Formato

Los estados financieros fueron alineados visualmente al antiguo Control.

Preservar cuando sea posible:

- encabezados morados;
- periodo actual celeste;
- forecast gris;
- márgenes resaltados;
- negativos entre paréntesis;
- subtotales en negrita;
- checks visibles;
- columnas históricas ocultas cuando corresponda.

No sacrificar la lógica financiera por formato.

---

# No hardcodear

No hardcodear un resultado calculable solo para reproducir el Control.

Excepciones posibles:

- históricos fuente;
- supuestos explícitos;
- partidas que en el propio Control eran inputs manuales.

Todo hardcode debe ser reconocible como:

- histórico;
- supuesto;
- ajuste documentado.

---

# No usar plugs para cuadrar

Nunca crear una línea artificial únicamente para conseguir:

`Assets = Liabilities + Equity`

o:

`Cash Flow = Balance`

Si el modelo no cierra:

investigar la causa.

Una línea de cierre que forme parte explícita de la metodología histórica del forecast debe distinguirse de un ajuste arbitrario.

---

# Orden de investigación cuando los estados no cierran

Revisar:

1. errores de fórmula;
2. referencias corridas;
3. P&L;
4. CxC;
5. CxP;
6. CxP Sueldos;
7. Bancos;
8. grants;
9. capitalización;
10. financiamiento;
11. retained earnings;
12. signos de Cash Flow;
13. precisión/TC;
14. forecast específico.

No empezar introduciendo un ajuste.

---

# QA del Real P&L

Comprobar:

- Operative incomes;
- costos;
- salarios;
- S&A;
- Gross Margin;
- SG&A;
- grants;
- EBIT;
- resultado financiero;
- impuestos;
- utilidad neta;
- EBITDA;
- checks internos.

---

# QA del Balance Sheet

Comprobar:

- cash;
- CxC;
- grants receivable;
- IP/software;
- CxP;
- CxP Sueldos;
- financiamiento;
- convertible;
- interés;
- retained earnings;
- Total Assets;
- Total Liabilities + Equity;
- check.

---

# QA del Cash Flow

Comprobar:

- caja inicial;
- Net Income;
- CxC;
- CxP;
- grants;
- financiamiento;
- Other;
- cambio neto;
- caja final;
- Check cálculo CF;
- Check BG CASH.

---

# QA cruzado

Después de cualquier modificación material:

1. releer las fórmulas modificadas;
2. comprobar resultados calculados;
3. buscar errores;
4. verificar P&L;
5. verificar Balance;
6. verificar Cash Flow;
7. comprobar checks cruzados.

Buscar:

- `#REF!`
- `#VALUE!`
- `#N/A`
- `#DIV/0!`
- `#ERROR!`
- referencias circulares

---

# Regla de finalización

Nunca reportar los estados como correctos únicamente porque:

- visualmente se parecen al Control;
- los totales redondeados coinciden;
- el Balance da cero.

Antes de considerarlos terminados debe comprobarse:

- fórmulas correctas;
- fuentes correctas;
- signos correctos;
- periodos correctos;
- checks internos;
- checks cruzados;
- lectura en vivo después de cualquier escritura.

Un número correcto obtenido mediante una fórmula incorrecta sigue siendo un error.

---

# Guardrails

- No confundir cash con devengo.
- No construir P&L desde pagos/cobros.
- No construir CxC/CxP desde P&L sin respetar sus roll-forwards.
- No hardcodear retained earnings para cuadrar.
- No duplicar interés convertible.
- No inventar capitalización.
- No usar `Other` como plug.
- No modificar TC para cuadrar estados.
- No eliminar checks.
- No aceptar circularidad.
- No modificar históricos reconciliados silenciosamente.
- No aceptar diferencias materiales como redondeo.
- No declarar terminado sin releer el archivo vivo.

---

# Coordinación con otras skills

## `finanzas-config-categorizacion`

Usar para:

- taxonomía;
- categorías;
- catálogos.

## `finanzas-transacciones-tc`

Usar para:

- cash;
- movimientos;
- pagos/cobros;
- TC;
- transferencias.

## `finanzas-devengo-operativo`

Usar para:

- Operative incomes;
- Real S&A;
- Sueldos 2026.

## `finanzas-cxc-cxp`

Usar para:

- CxC;
- CxP;
- CxP Sueldos;
- saldos de capital de trabajo.

## `finanzas-bancos-conciliacion`

Usar para:

- caja histórica;
- conciliación bancaria;
- saldos bancarios.

## `finanzas-presupuesto-vs`

Cuando exista, usar para:

- Budget vs P&L;
- análisis de variaciones.

## `finanzas-runway-dashboard`

Usar para:

- runway;
- escenarios de caja;
- KPIs;
- Dashboard.

## `finanzas-cierre-mensual`

Cuando exista, usar para:

- validar los tres estados como parte del cierre mensual.

---

# Referencias

Consultar cuando corresponda:

- `references/real-pnl.md`
- `references/balance-sheet.md`
- `references/cash-flow.md`
- `references/checks-tres-estados.md`

---

# Alcance final

Esta skill debe poder responder cuatro preguntas:

1. **¿La rentabilidad del periodo está correctamente calculada?**
2. **¿El Balance representa correctamente los saldos de cierre?**
3. **¿El Cash Flow explica correctamente el movimiento de caja?**
4. **¿Los tres estados se conectan y cierran entre sí?**

Solo cuando las cuatro respuestas sean sí, el modelo de tres estados puede considerarse validado.
