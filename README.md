
# Proyecto: Análisis de Inversiones con Score Personalizado

## 📌 Objetivo
Este proyecto aplica técnicas de análisis de datos para evaluar y comparar empresas del mercado bursátil según un **score propio**, basado en métricas financieras estandarizadas.  
El fin es **identificar oportunidades de inversión** y mostrar un flujo de trabajo reproducible de análisis cuantitativo, integrando recolección de datos, preprocesamiento, análisis exploratorio y comunicación de insights.

## 📊 Descripción
1. **Obtención de datos**  
   - Fuente: API de Yahoo Finance (`yfinance`) y otros datos financieros.
   - Generación del archivo `Acciones.csv` (ver sección *Reproducibilidad*).
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
