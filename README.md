# 📈 Quantitative Analysis: Trading Bots vs. Long-Term ETF Investing

## 🎯 Propósito del Proyecto

Como economista y científico de datos especializado en analítica, y con la responsabilidad de gestionar portafolios como Popular Investor Champion para 32 copiadores activos, he desarrollado este repositorio para auditar estadísticamente el rendimiento del trading algorítmico de corto plazo frente a una estrategia de inversión estructural a largo plazo basada en Dollar-Cost Averaging.

Utilizando librerías de Python como `pandas` y `yfinance`, este proyecto somete a prueba una estrategia técnica (Cruce EMA 9/21 en Oro) y la enfrenta a la realidad de los costos transaccionales, comparándola finalmente contra un portafolio diversificado de ETFs.

## 🧠 Conclusiones del Análisis Quant
Tras simular múltiples escenarios temporales (desde el intradía hasta el largo plazo en 2018), la evidencia extraída de los datos concluye que:

1. **La inversión estructural vence a la especulación:** Invertir en bolsa a largo plazo supera con creces la especulación con bots de trading. El mercado recompensa la paciencia y el crecimiento productivo de las empresas, mientras que penaliza la sobre-operatividad.

2. **El impacto letal del "ruido" y los costos:** En temporalidades cortas (15 minutos), el bot de medias móviles asume riesgos asimétricos. El alto volumen de operaciones genera una fricción enorme (spreads y comisiones) y el bot sufre severas pérdidas en mercados laterales (*whipsaw*), estancando el crecimiento del capital.

3. **Diversificación y Preservación de Capital:** Al comparar el bot contra un portafolio equilibrado (SPYG 35%, SMH 20%, BRK-B 20%, IEMG 15%, VTI 10%), la línea de crecimiento del portafolio es infinitamente más suave y menos volátil. Diversificar entre diferentes sectores y regiones minimiza el riesgo de ruina y prioriza la preservación del capital invertido, logrando retornos compuestos muy superiores a largo plazo.

---

## 📘 Apéndice laboratorio — la misma idea, explicada para quien arranca

Si eres nuevo en inversiones, el mensaje de este repo se puede resumir así:

> **“Entrar y salir” con una regla automática (medias móviles) suena a protección… pero a menudo te saca del mercado justo cuando más sube.**

### ¿Qué es una media móvil EMA 9/21?

Piensa en dos termómetros del precio:

- La **EMA 9** mira los últimos ~9 días (reacciona rápido).
- La **EMA 21** mira ~21 días (reacciona más lento).

Cuando la rápida queda **por encima** de la lenta, la regla dice “tendencia alcista → quédate invertido”.  
Cuando queda **por debajo**, dice “se enfrió → vete a efectivo”.

Eso es **market timing**: no es “elegir buenos activos”, es **decidir cuándo estar dentro o fuera**.

### Lo que ya vimos con el oro (notebooks de este repo)

En oro, el bot EMA 9/21 pierde contra **comprar y mantener** a plazos largos: operas más, pagas más fricción y te pierdes tramos alcistas.

### Lo que añadimos en el apéndice (core diversificado, 2013–2026)

Aplicamos la **misma lógica de timing** al portafolio core (SPYG / SMH / BRK.B / IEMG / VTI), con el mismo capital el día 1, costos tipográficos y sin mirar el futuro (señal hoy → opera mañana).

**Resultado en una línea:** el buy-and-hold del core terminó cerca de **$300k**; el timing EMA 9/21 cerca de **$91k**. El bot bajó un poco la peor caída, pero pagó ese “colchón” con ~$200k menos al final.

> **Etiqueta:** es un **laboratorio**, no una orden de trading ni un cambio al mix operativo.

📄 Lee el desarrollo completo (glosario, reglas, tablas y limitaciones) aquí:  
**[APPENDIX_LAB_EMA_9_21_VS_CORE.md](./APPENDIX_LAB_EMA_9_21_VS_CORE.md)**

---

## 📂 Contenido del Repositorio

Este repositorio contiene 3 Notebooks de Jupyter evaluando la evolución de la estrategia con distintos horizontes temporales, más el apéndice laboratorio del core:

### 0. `APPENDIX_LAB_EMA_9_21_VS_CORE.md` (nuevo)
Misma pregunta del bot (EMA 9/21) aplicada al **portafolio core** 2013–2026, escrita para lectores novatos. Veredicto: timing falsificado frente a buy-and-hold; **no candidato al mix**.

### 1. `bot trading 15min.ipynb`
Simulación de la estrategia de cruce de medias EMA 9/21 en un entorno intradiario altamente ruidoso (intervalos de 15 minutos) durante los últimos 60 días, aplicando costos de transacción.

```text
----------------------------------------
📊 RESULTADOS DEL BACKTEST (60d en 15m)
----------------------------------------
Operaciones ejecutadas : 199
Rendimiento Buy & Hold : -1.17%
Rendimiento del Bot    : 3.57%
Win Rate estimado      : 43.22%
----------------------------------------
```

A simple vista parece un resultado positivo, pero la alta frecuencia (199 operaciones en dos meses) expone el capital a un desgaste operativo insostenible a largo plazo.

### 2. Bot 1D since 2022.ipynb
Elevamos la temporalidad a gráficos Diarios (1D) desde enero de 2022. Al eliminar el ruido de los 15 minutos, el bot se convierte en un seguidor de tendencias
macroeconómicas.

```text
--------------------------------------------------
📊 RESULTADOS DESDE 2022-01-01 (1d)
--------------------------------------------------
Total de operaciones   : 47
Rendimiento Buy & Hold : 145.26%
Rendimiento de Bot     : 65.86%
Win Rate de la estrategia: 46.81%
--------------------------------------------------
```
Aunque el bot es rentable, mantener el activo base (Oro Físico) sin tocarlo duplicó el rendimiento del algoritmo algorítmico, demostrando que operar en contra de activos alcistas destruye valor.

### 3. Bot 1D vs B&H vs Andalejo since 2018.ipynb (El test definitivo)

En este script se integra mi portafolio de inversión personal estructurado en ETFs frente al Bot y frente a la tenencia pasiva del Oro. Se adjuntan dos simulaciones visuales críticas:

Gráfico desde 2023: Muestra el comportamiento desde el inicio real de mi estrategia de portafolio actual. La línea verde (Portafolio ETF) exhibe un crecimiento robusto y constante frente a la alta volatilidad del oro físico y el rendimiento inferior del algoritmo especulativo.

```text
📊 COMPARATIVA DE RENDIMIENTO (Desde 2023-08-03)
-------------------------------------------------------
Buy & Hold Oro             : 128.75%
Bot EMA 9/21 (Oro)         : 63.08%
Mi Portafolio Estructural  : 112.35%
-------------------------------------------------------
```
#### Gráfico Histórico desde 2018: La prueba ácida. 

Mientras que el algoritmo (línea roja) quedó completamente estancado alrededor del capital inicial ($1000) atrapado por la ineficiencia de los cruces retrasados, el portafolio de inversión estructural multiplicó el capital por cuatro, superando a todas las métricas de trading automatizado.

```text
-------------------------------------------------------
📊 COMPARATIVA DE RENDIMIENTO (Desde 2018-01-01)
-------------------------------------------------------
Buy & Hold Oro             : 232.71%
Bot EMA 9/21 (Oro)         : 8.43%
Mi Portafolio Estructural  : 300.50%
-------------------------------------------------------
```
Imagenes de resultados adjunto en los resultados.

## 🛠️ Requisitos Técnicos

Para ejecutar estos notebooks localmente, asegúrate de tener instaladas las siguientes dependencias en tu entorno de Python:

```bash
pip install pandas yfinance pandas-ta matplotlib numpy
```

## Autor

Andrés Alejandro Rodríguez Lozano — economista y científico de datos.  
[andalejo1109.github.io](https://andalejo1109.github.io/) — eToro [@Andalejo1109](https://etoro.tw/4lkmjxn)

## Licencia

MIT. Educational use. Not investment advice.
