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

## 📂 Contenido del Repositorio

Este repositorio contiene 3 Notebooks de Jupyter evaluando la evolución de la estrategia con distintos horizontes temporales:

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


A simple vista parece un resultado positivo, pero la alta frecuencia (199 operaciones en dos meses) expone el capital a un desgaste operativo insostenible a largo plazo.

2. Bot 1D since 2022.ipynb
Elevamos la temporalidad a gráficos Diarios (1D) desde enero de 2022. Al eliminar el ruido de los 15 minutos, el bot se convierte en un seguidor de tendencias macroeconómicas.

--------------------------------------------------
📊 RESULTADOS DESDE 2022-01-01 (1d)
--------------------------------------------------
Total de operaciones   : 47
Rendimiento Buy & Hold : 145.26%
Rendimiento de Bot     : 65.86%
Win Rate de la estrategia: 46.81%
--------------------------------------------------

Aunque el bot es rentable, mantener el activo base (Oro Físico) sin tocarlo duplicó el rendimiento del algoritmo algorítmico, demostrando que operar en contra de activos alcistas destruye valor.
