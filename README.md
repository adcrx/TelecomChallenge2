# Telecom Challenge 2 – Predicción de Cancelación de Clientes (Churn)

Repositorio: **TelecomChallenge2**  
Autor: **adcrx**  
Notebook principal: `TelecomX2.ipynb`

---

## 🎯 Propósito del Proyecto

El objetivo de este desafío es **predecir la cancelación (churn) de clientes** de la empresa ficticia **Telecom X**, utilizando técnicas de Machine Learning.  
A partir de los datos tratados en la Parte 1 del challenge, buscamos identificar qué clientes tienen mayor riesgo de cancelar, qué variables influyen más en su decisión y cómo la empresa puede implementar estrategias de retención.

---

## 📂 Estructura del Proyecto

- `TelecomX2.ipynb` → Notebook principal con todo el flujo del análisis y modelado.  
- `telecomx_tratado.csv` → Archivo CSV con los datos ya tratados en la Parte 1 (entrada principal del análisis).  
- `visualizaciones/` → Carpeta opcional para guardar gráficos relevantes (heatmaps, boxplots, scatterplots, matrices de confusión, etc.).  
- `README.md` → Este documento con descripción completa del proyecto.  

---

## 🔎 Preparación de Datos

1. **Carga del dataset tratado** (`telecomx_tratado.csv`).  
2. **Eliminación de columnas irrelevantes**: se descartaron identificadores como `customerID` y variables redundantes.  
3. **Clasificación de variables**:
   - **Categóricas**: `gender`, `InternetService`, `Contract`, `PaymentMethod`, `PaperlessBilling`, `MultipleLines`, entre otras.  
   - **Numéricas**: `tenure`, `Monthly`, `Total`, `Cuentas_Diarias`, `SeniorCitizen`, etc.  
4. **Codificación de variables categóricas**:  
   - Se aplicó **OneHotEncoder** (con `drop="first"`) para transformar variables categóricas en variables numéricas binarias.  
5. **Balanceo de clases**:  
   - La proporción de churn fue de aproximadamente **73% “No” y 27% “Sí”**.  
   - Se concluyó que no era un desbalance severo, por lo que no se aplicaron técnicas de oversampling/undersampling.  
6. **Normalización / estandarización**:  
   - Se aplicó **StandardScaler** únicamente en modelos sensibles a la escala (Regresión Logística y KNN).  
   - No se utilizó en modelos de árboles (Decision Tree, Random Forest).  
7. **Separación de datos**:  
   - Train/Test con proporción **80/20**, manteniendo la proporción de clases (stratify).  

---

## 📊 Análisis Exploratorio (EDA)

Durante la etapa de exploración se aplicaron diversas visualizaciones:

- **Heatmap de correlación**: identificamos variables con mayor relación con churn, como `InternetService_fiber optic`, `PaymentMethod_Electronic check`, `tenure` y `Contract_Two year`.  
- **Boxplots y scatterplots**:  
  - Clientes con **menor tiempo de permanencia (tenure bajo)** mostraron mayor tasa de cancelación.  
  - Contratos de **dos años** presentaron la menor tasa de churn.  
  - **Pagos electrónicos y facturación sin papel** estuvieron asociados a mayor cancelación.  
- **Top 10 correlaciones con churn**: permitió visualizar qué variables aumentaban o reducían la probabilidad de cancelación.  

Estos análisis dieron una base sólida para la construcción de modelos.

---

## 🤖 Modelado Predictivo

Se desarrollaron **cuatro modelos**:

1. **Regresión Logística** (con escalado).  
2. **KNN (K-Nearest Neighbors)** (con escalado).  
3. **Árbol de Decisión** (sin escalado).  
4. **Random Forest** (sin escalado).  

Justificación:  
- Modelos basados en distancia y optimización (Logística y KNN) requieren normalización.  
- Modelos basados en árboles no requieren este paso.  
- Se compararon modelos para encontrar el mejor equilibrio entre exactitud, precisión, recall y F1-score.

---

## 📈 Resultados y Evaluación

Métricas principales en el set de prueba:

- **Regresión Logística**: buen recall para la clase churn (~0.79), útil para identificar clientes que podrían cancelar.  
- **KNN**: desempeño balanceado, aunque menor recall que la regresión.  
- **Árbol de Decisión**: resultados similares a la regresión logística, con cierta tendencia a overfitting.  
- **Random Forest**: desempeño robusto, buen balance entre precisión y recall, aunque con ligera pérdida de generalización.  

Se concluyó que **Logística y Random Forest** fueron los modelos más útiles para la empresa, dependiendo de si la prioridad es **maximizar recall** (detectar la mayor cantidad posible de clientes en riesgo) o **equilibrar precisión y recall** (minimizar falsos positivos).  

---

## 🌟 Principales Factores que Influyen en el Churn

- **Aumentan el riesgo de cancelación**:  
  - Internet de fibra óptica.  
  - Método de pago: cheque electrónico.  
  - Bajo tiempo de permanencia (tenure bajo).  
  - Planes mensuales y facturación sin papel.  
  - Altos gastos mensuales y totales.  

- **Reducen el riesgo de cancelación**:  
  - Contratos de 1 y 2 años.  
  - Soporte técnico activo.  
  - Seguridad online incluida.  
  - Tener dependientes o pareja registrada.  

---

## 🚀 Instrucciones de Ejecución

1. Clonar el repositorio:  
   ```bash
   git clone https://github.com/adcrx/TelecomChallenge2.git
   cd TelecomChallenge2

 ##  📌 Conclusión Final

El análisis permitió a Telecom X entender los principales motivos de la cancelación de clientes y predecir con buena precisión quiénes están en mayor riesgo.
Esto abre la puerta a estrategias de retención personalizadas, enfocándose en clientes con contratos mensuales, facturación sin papel, pagos electrónicos y bajo tiempo de permanencia, que representan los segmentos más críticos para la empresa.

## ✍️ Autora

Este proyecto fue desarrollado por **Alejandra Cotroneo** como parte del programa **Oracle Next Education – Alura Latam.**

Forma parte de la Parte 2 del Challenge de Machine Learning (Telecom X), enfocado en el análisis y predicción de churn de clientes.
