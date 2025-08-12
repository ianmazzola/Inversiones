
# Proyecto: Análisis de Inversiones en Acciones

Este proyecto evalúa un conjunto de empresas listadas en bolsa mediante un score propio que integra métricas financieras clave como earnings growth, ROE, debt-to-equity y múltiplos de valuación.
El objetivo es detectar oportunidades de inversión y demostrar un flujo de trabajo de análisis de datos completo: recolección, limpieza, análisis exploratorio, visualización e interpretación.

Los resultados permiten identificar activos con fundamentos sólidos y precios atractivos en un momento dado, y ofrecen un marco replicable para futuros análisis.

## 📈 Insights principales

- **Empresas con alto *earnings growth*** tienden a ocupar las primeras posiciones del ranking, lo que puede resultar atractivo para inversores con mayor tolerancia al riesgo.  
- **Un PEG alto combinado con un PE bajo** indica posibles oportunidades de revalorización, ya que el precio actual no refleja plenamente el potencial de crecimiento de la empresa.  
- **El score se aplica a diferentes sectores**, permitiendo comparar calidad y valuación de forma relativa dentro de cada industria.
- **El enfoque es adaptable al perfil del inversor**, pudiendo ajustar los pesos de las métricas en el score para priorizar crecimiento, estabilidad o valuación según la estrategia deseada.
- **El score, tal como está calculado, es dependiente del periodo de referencia**: estandarizar con datos contemporáneos limita la comparabilidad histórica.
  
## 📌 Objetivo
Aplicar técnicas de análisis de datos para evaluar y comparar empresas del mercado bursátil mediante un **score propio** que integra métricas financieras clave (crecimiento, rentabilidad, apalancamiento y valuación).  
El objetivo es **identificar oportunidades de inversión accionables** y demostrar un flujo de trabajo completo y reproducible que abarca recolección de datos, preprocesamiento, análisis exploratorio, visualización de resultados y comunicación de insights.

## 📊 Descripción del flujo de trabajo
1. **Obtención de datos**  
Para este análisis se desarrolló un dataset propio a partir de datos obtenidos mediante la API de Yahoo Finance (`yfinance`).  
El proceso consistió en:

- **Selección del universo de empresas**: lista de tickers representativos de distintos sectores y tamaños de mercado. (S&P 500, Nasdaq y Dow Jones)
- **Descarga automatizada de datos financieros**: métricas de crecimiento, rentabilidad, apalancamiento y valuación.
- **Estructuración del dataset**: integración en un único `DataFrame` y exportación a `Acciones.csv` para uso en el análisis principal.

El código base para este proceso es:

```python
import yfinance as yf
import pandas as pd

sublistas = [tickers[i:i + 10] for i in range(0, len(tickers), 10)]
for i, bloque in enumerate(sublistas):
    print(i, bloque)

atributos = [
    "marketCap",
    "sector",
    "trailingPE",
    "forwardPE",
    "priceToBook",
    "dividendYield",
    "beta",
    "profitMargins",
    "returnOnEquity",
    "debtToEquity",
    "currentRatio",
    "earningsGrowth",
    "trailingPegRatio",
    "returnOnAssets",
    "epsForward",
]

dfs = []  # Acá guardamos todos los dataframes

for i, bloque in enumerate(sublistas):
    datos = []  # Se crea una nueva lista vacía para cada bloque
    for ticker in bloque:
        info = yf.Ticker(ticker).info
        data = {atributo: info.get(atributo, None) for atributo in atributos}
        data["Ticker"] = ticker
        datos.append(data)
    
    df_bloque = pd.DataFrame(datos).set_index("Ticker")
    dfs.append(df_bloque)  # Guardamos el DataFrame para este bloque

# Creamos un único dataframe con todos los datos
df_final = pd.concat(dfs)

df_final.to_csv("Acciones.csv")



2. **Preprocesamiento**  
   - Limpieza y tratamiento de valores faltantes.
   - Cálculo de métricas derivadas (growth, ratios financieros, etc.).
   - Estandarización de variables con `StandardScaler`.
3. **Cálculo del score**  
   - Score ponderado en base a métricas seleccionadas.
   - Análisis de sensibilidad del score a distintas variables.
4. **EDA y visualizaciones**  
   - Distribuciones, correlaciones y ranking de empresas.
5. **Casos de estudio**  
   - Ejemplo: evolución del score de empresas como NVIDIA o Microsoft en periodos clave.
6. **Conclusiones e insights**  
   - Ejemplo: limitación detectada en la estandarización “contemporánea” del score y alternativas para resolverlo.

## 📈 Insights generados
- El score estandarizado es útil para comparar activos dentro de un mismo periodo, pero su comparabilidad histórica puede verse afectada.
- Identificación de empresas con métricas sólidas en determinados sectores.
- Ejemplos de cómo variaciones en *earnings growth*, *debt-to-equity* u otras métricas impactan el ranking.


## 🛠 Tecnologías y librerías
- Python 3.x
- Pandas, NumPy
- Matplotlib, Seaborn
- scikit-learn
- yfinance

## 🚀 Próximos pasos
- Modularizar cálculo de score y guardar scaler de referencia.
- Añadir pruebas unitarias mínimas para el score.
- Mejorar documentación de cada métrica y su impacto.

---
*Autor: Ian Lautaro Mazzola*  
*Última actualización: Agosto 2025*
