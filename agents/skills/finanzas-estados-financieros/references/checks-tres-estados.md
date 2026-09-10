# Finanzas Sommos — Checks del modelo de tres estados

## Propósito

Documentar los controles obligatorios para validar:

- Real P&L;
- Balance Sheet;
- Cash Flow;

como un modelo financiero integrado.

Esta referencia pertenece a:

`finanzas-estados-financieros`

---

# Principio

Un modelo financiero no se considera correcto solo porque:

- el P&L tenga números;
- el Balance cierre;
- el Cash Flow termine con una caja.

Los estados deben:

- utilizar fuentes correctas;
- relacionarse correctamente;
- tener checks internos;
- cerrar entre sí.

---

# Check 1 — Fuentes del P&L

Validar que el P&L coincida con:

- `Operative incomes`
- `Real S&A`
- `Sueldos 2026`

Los checks internos deben ser:

`≈ 0`

Entre los controles conocidos:

- Operative incomes normal
- Operative incomes Grants
- Budget TH
- S&A

---

# Check 2 — Balance Sheet

Debe cumplirse:

`Total Assets = Total Liabilities + Equity`

Por lo tanto:

`Assets - Liabilities - Equity ≈ 0`

---

# Check 3 — Resultado acumulado

El resultado acumulado reflejado en patrimonio debe ser consistente con:

`Real P&L`

Resultado esperado:

`≈ 0`

---

# Check 4 — Cash Flow interno

Debe cumplirse:

`Beginning Cash + Net Change = Ending Cash`

Por lo tanto:

`Check cálculo CF ≈ 0`

---

# Check 5 — Cash Flow vs Balance Sheet

Debe cumplirse:

`Ending Cash Cash Flow = Cash Balance Sheet`

Resultado esperado:

`≈ 0`

Este es uno de los checks más importantes.

---

# Check 6 — Bancos vs Balance Sheet

Para periodos históricos conciliados:

`Cash Bancos ≈ Cash Balance Sheet`

Si no coincide:

investigar antes de cerrar.

---

# Check 7 — CxC

El saldo de CxC del Balance debe coincidir con:

`CxC Mensual`

No con revenue del P&L.

---

# Check 8 — CxP

El saldo de CxP del Balance debe coincidir con:

`CxP Mensual`

considerando las exclusiones específicas del modelo.

---

# Check 9 — CxP Sueldos

El saldo de nómina en Balance debe coincidir con:

`CxP Sueldos`

No utilizar ajustes adicionales si la fuente ya es correcta.

---

# Check 10 — Capitalización

La evolución del activo de software/IP debe reconciliar con:

- capitalización del P&L;
- amortización/depreciación;
- saldo anterior.

No duplicar la capitalización.

---

# Check 11 — Financiamiento

Revisar continuidad de:

- principal convertible;
- interés;
- financing payable;
- aportes/préstamos.

No duplicar un saldo financiero entre CxP y línea específica.

---

# Checks históricos vs forecast

## Histórico

Debe validar contra:

- Bancos;
- devengos;
- CxC/CxP;
- Control antiguo.

## Forecast

Debe validar principalmente:

- ecuaciones;
- dependencias;
- continuidad;
- supuestos.

No se requiere extracto bancario futuro.

---

# Tolerancias

Clasificar diferencias en tres niveles:

## Exacta

`0`

## Técnica

Diferencia mínima explicada por:

- precisión;
- TC;
- Excel vs Google Sheets.

## Material

Diferencia que requiere investigación.

Nunca llamar “redondeo” a una diferencia material sin analizarla.

---

# Señales de error estructural

Investigar inmediatamente si aparece:

- diferencia que crece mes a mes;
- diferencia exactamente igual a una partida;
- cambio abrupto tras modificar una fórmula;
- Cash Flow y Balance divergen;
- retained earnings no sigue P&L;
- CxC/CxP del Balance no coincide con sus schedules.

---

# Errores de fórmula

Buscar siempre:

- `#REF!`
- `#VALUE!`
- `#N/A`
- `#DIV/0!`
- `#ERROR!`
- referencia circular

---

# Orden de QA de tres estados

Revisar en este orden:

1. fuentes de devengo;
2. Real P&L;
3. CxC;
4. CxP;
5. CxP Sueldos;
6. Bancos;
7. Balance Sheet;
8. Cash Flow;
9. checks cruzados.

Este orden ayuda a corregir la causa en la fuente correcta.

---

# Nunca corregir downstream primero

Ejemplo:

Si Balance Sheet muestra CxP incorrecta:

no modificar Balance Sheet primero.

Revisar:

`CxP Mensual`

Si Cash Flow muestra cash incorrecto:

no modificar Ending Cash primero.

Revisar:

- capital de trabajo;
- financiamiento;
- Balance;
- Bancos.

---

# Regla de cero artificial

Un check en cero obtenido mediante:

- plug;
- hardcode;
- referencia circular;
- fórmula que compara una celda consigo misma;

no es un check válido.

---

# Validación después de una corrección

Después de corregir una fórmula o fuente:

1. releer la celda;
2. revisar el mes anterior;
3. revisar el mes siguiente;
4. revisar totales;
5. revisar estado dependiente;
6. ejecutar todos los checks nuevamente.

No validar solo el mes modificado.

---

# Checklist final

Antes de declarar el modelo correcto:

- [ ] P&L conectado a fuentes de devengo.
- [ ] Checks P&L en tolerancia.
- [ ] Balance Sheet cierra.
- [ ] Utilidad acumulada coincide con P&L.
- [ ] Cash Flow calcula correctamente.
- [ ] Ending Cash coincide con Balance.
- [ ] Bancos coincide con Balance para histórico.
- [ ] CxC coincide con schedule.
- [ ] CxP coincide con schedule.
- [ ] CxP Sueldos coincide con schedule.
- [ ] No existen errores de fórmula.
- [ ] No existen circularidades.
- [ ] No existen plugs no documentados.
- [ ] Las celdas modificadas fueron releídas.

---

# Estado final

Solo cuando todos los controles aplicables estén correctos puede afirmarse:

`Modelo de 3 estados = OK`

Ese estado debe representar una validación real, no simplemente una etiqueta visual.

---

# Regla final

El mejor check no es el que siempre da cero.

Es el que **puede fallar cuando algo está realmente mal**.
