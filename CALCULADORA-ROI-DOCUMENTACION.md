# Calculadora ROI - Adereso AI

## Descripción General

La calculadora ROI de Adereso AI permite a potenciales clientes estimar cuánto dinero podrían ahorrar anualmente al implementar automatización de atención al cliente con Adereso. El usuario ingresa sus datos operativos (industria, volumen de tickets, canales, ejecutivos) y la calculadora proyecta ahorros, retorno de inversión y tiempo de payback.

---

## Flujo del Usuario

1. **Selecciona su industria** (Retail, Servicios Financieros, Servicios Básicos, Otros)
2. **Ingresa su volumen mensual de conversaciones** (número total de tickets al mes)
3. **Presiona "Calcular"** → se muestra el panel de resultados
4. **Puede ajustar parámetros secundarios:**
   - Distribución de tickets por canal (Chats, Correos, Redes Sociales)
   - Nivel de IA (Automatización de Flujo, GenAI Básica, GenAI Plus)
   - Número de ejecutivos (se calcula automáticamente pero se puede sobrescribir)
   - Salario mensual por ejecutivo (USD)
   - Toggle Plan Anual (activado por defecto, aplica descuento del 12%)

---

## Variables de Entrada

| Variable | Descripción | Valor por defecto |
|---|---|---|
| **Industria** | Determina la tasa de automatización esperada | Debe seleccionarse obligatoriamente |
| **Volumen mensual de conversaciones** | Total de tickets que recibe el contact center al mes | El usuario lo ingresa |
| **Distribución por canal** | Porcentaje del volumen asignado a Chats, Correos y Redes Sociales | Chats 30%, Correos 60%, RRSS 10% |
| **Nivel de IA** | Tipo de solución: Flujo, GenAI Básica o GenAI Plus | Automatización de Flujo |
| **Número de ejecutivos** | Cantidad de agentes en el contact center | Se calcula como: tickets totales ÷ 600 (redondeado hacia arriba, mínimo 1) |
| **Salario mensual por ejecutivo** | Sueldo bruto mensual en USD | $1,000 USD |
| **Plan Anual** | Toggle que indica si se contrata plan anual | Activado (checked) |

---

## Tasas de Automatización por Industria

La tasa de automatización determina qué porcentaje de los tickets serán resueltos por la IA. Varía según la industria y el nivel de IA seleccionado:

| Industria | Automatización de Flujo | GenAI Básica | GenAI Plus |
|---|---|---|---|
| **Retail** | 40% | 50% | 60% |
| **Servicios Financieros** | 60% | 70% | 75% |
| **Servicios Básicos** | 70% | 80% | 90% |
| **Otros** | 60% | 70% | 75% |

Servicios Básicos tiene la tasa más alta porque sus consultas suelen ser más repetitivas y estandarizadas. Retail tiene la más baja porque tiende a tener consultas más variadas.

---

## Tabla de Costos por Ticket (Precios Adereso)

El costo por ticket de Adereso tiene dos componentes: **Desk** (plataforma de gestión) y **Studio** (motor de automatización). Los precios bajan a medida que aumenta el volumen de tickets:

| Rango de Tickets | Flujo (Desk + Studio) | GenAI Básica (Desk + Studio) | GenAI Plus (Desk + Studio) |
|---|---|---|---|
| Hasta 4,500 | $0.138 + $0.035 = **$0.173** | $0.138 + $0.084 = **$0.222** | $0.138 + $0.231 = **$0.369** |
| Hasta 13,500 | $0.126 + $0.032 = **$0.158** | $0.126 + $0.077 = **$0.203** | $0.126 + $0.210 = **$0.336** |
| Hasta 40,500 | $0.118 + $0.030 = **$0.148** | $0.118 + $0.072 = **$0.190** | $0.118 + $0.197 = **$0.315** |
| Hasta 121,500 | $0.109 + $0.027 = **$0.136** | $0.109 + $0.066 = **$0.175** | $0.109 + $0.182 = **$0.291** |
| Hasta 364,500 | $0.104 + $0.026 = **$0.130** | $0.104 + $0.064 = **$0.168** | $0.104 + $0.174 = **$0.278** |
| Hasta 1,093,500 | $0.098 + $0.025 = **$0.123** | $0.098 + $0.060 = **$0.158** | $0.098 + $0.164 = **$0.262** |
| Hasta 3,280,500 | $0.095 + $0.024 = **$0.119** | $0.095 + $0.058 = **$0.153** | $0.095 + $0.158 = **$0.253** |

> **Nota:** El componente Desk es igual para los tres niveles de IA dentro del mismo rango de volumen. Lo que cambia es el componente Studio, que es más caro a medida que la IA es más sofisticada.

---

## Fórmulas de Cálculo

### 1. Tickets Totales Mensuales

```
Tickets Totales = Chats + Correos + Redes Sociales
```

La distribución inicial se asigna automáticamente como 30% / 60% / 10% del volumen ingresado, pero el usuario puede mover los sliders para ajustarla.

---

### 2. Cálculo Automático de Ejecutivos

```
Ejecutivos sugeridos = Tickets Totales ÷ 600  (redondeado hacia arriba, mínimo 1)
```

Es decir, se asume que un ejecutivo puede gestionar hasta 600 tickets al mes. Si el usuario ingresa manualmente un número de ejecutivos, se usa ese valor en su lugar.

---

### 3. Costo Anual del Contact Center (sin Adereso)

```
Costo Anual CC = Salario Mensual × Número de Ejecutivos × 12
```

Ejemplo: Si hay 5 ejecutivos ganando $1,000 USD al mes → Costo Anual CC = $1,000 × 5 × 12 = **$60,000 USD**

---

### 4. Costo por Ticket Actual

```
Costo por Ticket = Costo Anual CC ÷ Tickets Anuales Totales
```

Donde:
- Tickets Anuales Totales = Tickets Totales Mensuales × 12

Ejemplo: Si el costo anual es $60,000 y se gestionan 3,000 tickets/mes (36,000/año) → Costo por Ticket = $60,000 ÷ 36,000 = **$1.67 USD**

---

### 5. Tickets Automatizados (Anuales)

```
Tickets Automatizados = Tickets Anuales Totales × Tasa de Automatización
```

La tasa de automatización viene de la tabla de industrias (ver arriba), según la industria y nivel de IA seleccionados.

Ejemplo: 36,000 tickets anuales × 70% (Servicios Financieros + GenAI Básica) = **25,200 tickets automatizados**

---

### 6. Ahorro Bruto Anual

```
Ahorro Bruto = Tickets Automatizados × Costo por Ticket
```

Si está activado el Plan Anual, se aplica un aumento del 12% al ahorro:

```
Ahorro Bruto (Plan Anual) = Ahorro Bruto × 1.12
```

Ejemplo: 25,200 tickets × $1.67 = **$42,084 USD** de ahorro bruto

---

### 7. Inversión en Adereso (Costo de la Plataforma)

```
Costo Mensual Adereso = (Costo por Ticket Adereso × Tickets Totales Mensuales) + $250
```

El $250 es un cargo fijo mensual. El "Costo por Ticket Adereso" se obtiene de la tabla de precios (Desk + Studio) según el rango de volumen y el nivel de IA.

```
Inversión Anual = Costo Mensual × 12
```

Si está activado el Plan Anual, se aplica un descuento del 12%:

```
Inversión Anual (Plan Anual) = Inversión Anual × 0.88
```

Ejemplo: Con 3,000 tickets/mes en GenAI Básica (rango hasta 4,500): Costo Mensual = ($0.222 × 3,000) + $250 = $916 → Inversión Anual = $916 × 12 = $10,992 → Con plan anual: $10,992 × 0.88 = **$9,673 USD**

---

### 8. Ahorro Neto Anual (Retorno)

```
Ahorro Neto = Ahorro Bruto − Inversión Anual en Adereso
```

Este es el dinero que efectivamente se ahorra después de pagar por Adereso.

---

### 9. ROI (Retorno sobre la Inversión)

Se expresa de dos formas:

**Como multiplicador (veces):**
```
ROI (veces) = Ahorro Bruto ÷ Inversión Anual
```

**Como porcentaje:**
```
ROI (%) = (Ahorro Bruto ÷ Inversión Anual) × 100
```

Ejemplo: $42,084 ÷ $9,673 = **4.35x** (es decir, la inversión se paga 4.35 veces)

---

### 10. Payback (Tiempo de Recuperación)

```
Payback (meses) = (Inversión Anual ÷ Costo Anual CC) × 12
```

Indica en cuántos meses la inversión en Adereso se cubre con el costo que ya se tiene en ejecutivos.

Ejemplo: ($9,673 ÷ $60,000) × 12 = **1.93 meses**

---

### 11. Nuevo Costo del Contact Center

```
Nuevo Costo CC = Costo Anual CC − Ahorro Bruto + Inversión Anual en Adereso
```

Representa el nuevo costo operativo del contact center con Adereso implementado.

---

### 12. Incremento de Eficiencia

```
Incremento Eficiencia (%) = (Nuevo Costo CC ÷ Costo Anual CC) × 100
```

> **Nota:** Este valor indica qué porcentaje del costo original representa el nuevo costo. Si da, por ejemplo, 50%, significa que el nuevo costo es la mitad del original (50% de eficiencia ganada).

---

### 13. Reducción Estimada de Ejecutivos

```
Ejecutivos Reducidos = Número de Ejecutivos × Tasa de Automatización
```

Ejemplo: 5 ejecutivos × 70% = **3.5 → ~4 ejecutivos** que podrían reasignarse o reducirse.

---

## Efecto del Toggle "Plan Anual"

Cuando el plan anual está activado (es el estado por defecto), ocurren **dos cosas simultáneamente**:

| Concepto | Sin Plan Anual | Con Plan Anual |
|---|---|---|
| **Inversión en Adereso** | Costo mensual × 12 | Costo mensual × 12 × **0.88** (descuento 12%) |
| **Ahorro Bruto** | Tickets automatizados × costo por ticket | Tickets automatizados × costo por ticket × **1.12** (aumento 12%) |

El efecto combinado es que con plan anual: se paga menos y se muestra un ahorro mayor, lo que mejora significativamente el ROI mostrado.

---

## Resultados que se Muestran al Usuario

Después de calcular, la pantalla principal muestra:

1. **Conversaciones automatizadas por Adereso AI** (tickets automatizados al año)
2. **Ahorro Anual con Adereso AI (USD)** (ahorro bruto anual)

Adicionalmente en el reporte PDF se incluye:

**Datos Operativos:**
- Cantidad de ejecutivos
- Sueldo bruto ejecutivo
- Costo anual de nómina del Contact Center
- Tickets gestionados mensualmente
- Porcentaje de automatización esperado
- Tickets automatizados mensual y anual
- Reducción estimada de ejecutivos
- Multiplicador de inversión y meses de payback

**Análisis Financiero:**
- Ahorro anual generado
- Nuevo costo del Contact Center
- Incremento de eficiencia
- Inversión en Adereso
- Retorno anual
- ROI (%)

---

## Ejemplo Completo Paso a Paso

**Datos de entrada:**
- Industria: Servicios Financieros
- Volumen mensual: 3,000 tickets
- Distribución: Chats 900 (30%), Correos 1,800 (60%), RRSS 300 (10%)
- Nivel de IA: GenAI Básica
- Ejecutivos: 5 (auto-calculado: 3,000 ÷ 600 = 5)
- Salario: $1,000 USD/mes
- Plan Anual: Activado

**Cálculos:**

| Paso | Fórmula | Resultado |
|---|---|---|
| Tickets anuales | 3,000 × 12 | 36,000 |
| Costo anual CC | $1,000 × 5 × 12 | $60,000 |
| Costo por ticket actual | $60,000 ÷ 36,000 | $1.67 |
| Tasa automatización | Financieros + GenAI Básica | 70% |
| Tickets automatizados | 36,000 × 0.70 | 25,200 |
| Ahorro bruto | 25,200 × $1.67 | $42,084 |
| Ahorro bruto (plan anual) | $42,084 × 1.12 | $47,134 |
| Costo ticket Adereso | Desk $0.138 + Studio $0.084 (rango ≤4,500) | $0.222 |
| Costo mensual Adereso | ($0.222 × 3,000) + $250 | $916 |
| Inversión anual | $916 × 12 | $10,992 |
| Inversión anual (plan anual) | $10,992 × 0.88 | $9,673 |
| Ahorro neto | $47,134 − $9,673 | $37,461 |
| ROI (veces) | $47,134 ÷ $9,673 | 4.87x |
| ROI (%) | ($47,134 ÷ $9,673) × 100 | 487% |
| Payback | ($9,673 ÷ $60,000) × 12 | 1.93 meses |
| Nuevo costo CC | $60,000 − $47,134 + $9,673 | $22,539 |
| Ejecutivos reducidos | 5 × 0.70 | ~4 |

---

## Tracking y Datos

- **Firebase:** Cuando el usuario descarga el reporte PDF, se guardan sus datos en la colección `usuarios-reportes` de Firebase (nombre, email, empresa y todos los datos del cálculo).
- **Meta Ads (Facebook Pixel):** Se dispara el evento personalizado `DescargaReporteAdereAI` al descargar el reporte.
- **Redirección post-descarga:** Después de 800ms se redirige a `https://adereso.ai/thank-you-page-roi/` con parámetros UTM.
- **URL compartible:** El botón "Compartir resultado" genera una URL con todos los parámetros del cálculo, permitiendo reconstruir los resultados sin volver a completar el formulario.

---

## Notas Importantes para Futuros Cambios

1. **El cargo fijo de $250/mes** se suma siempre al costo mensual de Adereso, independiente del volumen.
2. **La regla de 600 tickets por ejecutivo** es el benchmark usado para sugerir el número de agentes.
3. **El plan anual afecta doblemente los resultados:** baja la inversión (×0.88) Y sube el ahorro mostrado (×1.12). Esto significa que el impacto en el ROI es significativamente mayor que solo el 12%.
4. **Los rangos de precio escalan por factor ×3:** 4,500 → 13,500 → 40,500 → 121,500 → 364,500 → 1,093,500 → 3,280,500.
5. **El componente Desk es el mismo para todos los niveles de IA** dentro del mismo rango; solo varía Studio.
6. **Si se cambia la tabla de costos**, hay que respetar el formato de rangos porque la función `findCostRange` busca el primer rango que sea mayor o igual al volumen de tickets.
