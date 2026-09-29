# Apéndice laboratorio — ¿Sirve “entrar y salir” del portafolio con medias móviles?

> **Etiqueta:** laboratorio, **no** candidato al mix operativo.  
> Material educativo. **No es consejo de inversión.** Los resultados pasados no predicen el futuro.

Este texto amplía la idea de este repositorio: aquí se comparó un bot EMA 9/21 sobre **oro** contra comprar y mantener. En este apéndice hacemos la misma pregunta, pero sobre el **portafolio core** (varios ETFs juntos), entre 2013 y 2026.

---

## 1. La idea en una frase (para quien arranca)

Imagina que tienes un “combo” de inversiones (acciones de crecimiento, semiconductores, Berkshire, mercados emergentes y el mercado total de EE. UU.).  
La pregunta del laboratorio es:

> Si en vez de **quedarme invertido todo el tiempo**, uso una regla automática que me saca a efectivo cuando la tendencia “parece” débil… ¿termino con más dinero?

La regla que probamos se llama **cruce de medias móviles EMA 9 y EMA 21**.

---

## 2. Glosario rápido (sin jerga innecesaria)

| Término | Qué significa en la práctica |
|--------|-------------------------------|
| **Buy & Hold (B&H)** | Compras el portafolio y lo mantienes. Rebalanceas de vez en cuando para volver a los pesos acordados. No intentas “adivinar” el momento. |
| **DCA (aporte mensual)** | Cada mes metes una cantidad fija (aquí, **USD 200**), sin mirar si el mercado subió o bajó. |
| **Market timing** | Entrar y salir según señales (“ahora sí / ahora no”). Es lo que hace el bot EMA. |
| **EMA (media móvil exponencial)** | Un promedio del precio que da más peso a los días recientes. La EMA 9 “reacciona” más rápido; la EMA 21 es más lenta. |
| **Cruce EMA 9/21** | Si la línea rápida queda **por encima** de la lenta → se considera tendencia alcista → **invertido**. Si queda **por debajo** → se va a **efectivo** (cash). |
| **Core / mix** | El portafolio objetivo de la tesis: SPYG, SMH, BRK.B, IEMG, VTI. |
| **Valor terminal** | Cuánto dinero tienes al final del experimento. |
| **CAGR / TWR** | Ritmo de crecimiento anualizado del portafolio, midiendo el rendimiento de lo ya invertido (no confunde “metí más plata” con “la estrategia rindió más”). |
| **Max drawdown** | La peor caída desde un máximo hasta el mínimo siguiente. Sirve para sentir el “dolor” del camino. |
| **bps (basis points)** | 1 bp = 0,01 %. Aquí usamos **5 bps por lado** como costo tipográfico al rotar (aproximación; no es el spread real de eToro). |
| **Laboratorio** | Experimento para aprender. **No** significa “hay que usarlo en la cuenta real”. |

---

## 3. ¿Qué es exactamente la regla EMA 9/21 aquí?

1. Construimos cada día el valor de un “portafolio teórico” con los pesos fijos del core (NAV sintético).  
2. Calculamos dos promedios de ese valor: uno de 9 días y uno de 21.  
3. **Si EMA9 > EMA21** → al día siguiente seguimos (o entramos) **invertidos en el core**.  
4. **Si EMA9 < EMA21** → al día siguiente nos vamos a **efectivo** (el dinero no crece; en este modelo el cash rinde 0 %).  
5. Para no “hacer trampa” con el futuro: la señal se toma al **cierre del día t** y la operación se aplica al **cierre del día t+1**.

En criollo: la regla intenta **estar dentro** cuando la tendencia reciente es alcista y **afuera** cuando se enfría. Eso suena atractivo… pero tiene un costo oculto: en mercados que suben muchos años, pasar tiempo en efectivo te hace **perder el tren**.

---

## 4. Reglas del experimento (para que sea comparable)

| Pieza | Valor usado |
|------|-------------|
| Portafolio | SPYG 31 % · SMH 22 % · BRK.B 20 % · IEMG 20 % · VTI 7 % |
| Periodo | 2013-01-02 → 2026-09-28 |
| Capital inicial (B&H y EMA) | **USD 33,800** el día 1 (mismo monto total que habría aportado un DCA de USD 200/mes + USD 1,000 inicial) |
| Benchmark extra | DCA + B&H del mismo core (USD 1,000 + USD 200/mes) |
| Costos | 5 bps por lado al operar (también probamos 0 y 15) |
| Señal | EMA 9/21 (y una sola sensibilidad: EMA 12/26) |
| Etiqueta | **Laboratorio — no candidato al mix** (la tesis Phase 1 no usa timing) |

¿Por qué mismo capital el día 1 para B&H y EMA? Para no mezclar dos preguntas. Si una estrategia “gana” solo porque metió plata en otro momento, no sabes si ganó la **regla de timing** o el **calendario de aportes**.

---

## 5. Resultados (números reales de la corrida)

### Tabla principal — costos 5 bps

| Estrategia | ¿Qué hace? | Valor al final | Crecimiento anualizado (TWR) | Peor caída | % del tiempo invertido |
|---|---|---:|---:|---:|---:|
| **B&H del core** | Siempre invertido (con rebalance mensual) | **$300,128** | **17.30 %** | −31.21 % | 100 % |
| **EMA 9/21** | Entra/sale según el cruce | **$91,041** | **7.50 %** | −26.25 % | ~71 % |
| **DCA + B&H** | Aportes mensuales, siempre en el core | **$139,683** | **17.29 %** | −31.21 % | 100 % |

Lectura para novatos:

- El **B&H** terminó con **más del triple** de dinero que el timing EMA, partiendo del mismo capital.  
- El EMA **sí** bajó un poco la peor caída (−26 % vs −31 %), pero pagó ese “colchón” carísimo: estuvo ~29 % del tiempo en efectivo durante un mercado que, en conjunto, subió mucho.  
- El **DCA** no compite en la misma liga de “mismo dinero el día 1”: aporta de a poco. Sirve como referencia de la política real de aportes, no como rival directo del timing lump sum.

### ¿Y si cambio un poco la regla? (sensibilidad, no “optimización”)

| Variante | Valor terminal | CAGR | Max DD |
|---|---:|---:|---:|
| EMA 9/21 @ 5 bps | $91,041 | 7.50 % | −26.25 % |
| EMA 12/26 @ 5 bps | $108,955 | 8.91 % | −17.76 % |
| B&H (referencia) | $300,128 | 17.30 % | −31.21 % |

Otra ventana de medias **tampoco** alcanza al B&H. No buscamos “la mejor EMA del universo” (eso sería data-snooping); solo comprobamos que el veredicto no depende de un único número mágico.

### Costos: ¿el bot se come solo por comisiones?

| Costos | Valor final EMA 9/21 | CAGR EMA |
|----:|---:|---:|
| 0 bps | $97,507 | 8.04 % |
| 5 bps | $91,041 | 7.50 % |
| 15 bps | $79,359 | 6.43 % |

Los costos **empeoran** al timing, pero **incluso a costo cero** queda lejos del B&H (~$300k). El problema principal no es la comisión: es **estar fuera** mientras el core sube.

### Cuando el timing “parece” útil (estrés corto)

En ventanas malas (COVID 2020, bear 2022) el EMA a veces termina con **más** valor que el B&H *dentro de esa ventanita*, porque se fue a cash.  
Eso no salva el resultado de **toda** la muestra 2013–2026: el mercado alcista largo se come esa “protección”.

---

## 6. Qué falsamos y qué no

**Hipótesis falsable:** “El timing EMA 9/21 del core supera al B&H del core en valor terminal y en CAGR, con el mismo capital.”

**Veredicto:** **falsificada** en esta muestra. El B&H gana por goleada en riqueza y en ritmo de crecimiento.

**Qué no concluimos:**

- No “demostramos” que *ningún* timing funciona en ningún activo ni en ningún periodo.  
- No recomendamos comprar o vender nada.  
- No usamos este resultado para cambiar el mix operativo: la tesis Phase 1 es **aportes periódicos + buy-and-hold del core**, sin timing.

---

## 7. Por qué esto importa si estás empezando

1. **Una regla que “evita caídas” puede hacerte más pobre** si te saca del mercado en los tramos que más suben.  
2. **Sentir menos drawdown no es lo mismo que ganar más dinero.** El EMA bajó un poco la peor caída y perdió ~$200k de valor terminal frente al B&H.  
3. **Los costos castigan más a quien opera más.** El timing gira; el B&H casi no.  
4. **Laboratorio ≠ producto.** Probar ideas es sano; meterlas a la cuenta real sin tesis es otro oficio.

Si quieres la analogía del experimento de oro en este mismo repo: allí el bot EMA también perdió contra quedarse invertido a largo plazo. Aquí pasa lo mismo, pero midiendo el **core diversificado** — el portafolio que importa para la tesis — no un solo activo.

---

## 8. Limitaciones (léelas antes de compartir el hallazgo)

- Sin impuestos, sin FX COP/USD, sin spread real de eToro.  
- Cash del EMA rinde **0 %** (en la vida real un money-market podría rendir algo; no lo modelamos aquí).  
- Universo “vivo” actual (survivorship).  
- Una muestra alcista larga (2013–2026) favorece al B&H; por eso también miramos estrés 2020/2022 e IS/OOS.  
- El tamaño de muestra es pequeño para afirmar “alpha estadístico”.

---

## Autor

**Andrés Alejandro Rodríguez Lozano** — economista y científico de datos.  
Web: [andalejo1109.github.io](https://andalejo1109.github.io) — eToro [@Andalejo1109](https://www.etoro.com/people/andalejo1109)

## Licencia

MIT — uso educativo. No es recomendación de inversión.
