# 📊 Challenge Telecom X – Parte 2: Predicción de Cancelación de Clientes

## 📖 Descripción del Proyecto
Este proyecto corresponde a la **segunda parte** del desafío de la empresa ficticia **Telecom X** (Alura Latam – Data Science).  
En la Parte 1 realizamos la limpieza y el análisis exploratorio del churn (cancelación).  
En esta Parte 2 construimos y comparamos **modelos predictivos** para anticipar qué clientes tienen mayor probabilidad de cancelar.

---

## 🎯 Objetivos
- Preparar los datos tratados en la Parte 1 para modelado.
- Realizar un **análisis de correlación** y un **análisis dirigido** (gráficos puntuales).
- Entrenar y comparar **al menos dos modelos** de ML (se usaron cuatro).
- Evaluar con **Accuracy, Precisión, Recall, F1** y **Matriz de Confusión**.
- Analizar **importancia de variables** e interpretar resultados.
- Proponer **estrategias de retención** basadas en los hallazgos.

---

## ⚙️ Preparación de Datos
- **Fuente**: CSV tratado de la Parte 1 (con columnas corregidas y estandarizadas).
- **Limpieza**: se removieron columnas irrelevantes (`customerID`, columnas índice auxiliares, etc.).
- **Tipos/Nulos**: `Total` se forzó a numérico y se imputó con mediana; `Churn` sin nulos.
- **Target**: `Churn` mapeado a **0 = No** / **1 = Yes**.
- **Encoding**: categóricas con **OneHotEncoder** (dejando `Churn` fuera del encoding).
- **Clase objetivo (desbalance)**: aprox. **73% No vs. 27% Sí** → **no** se aplicó balanceo (no severo).  
  - Mitigaciones: split **estratificado** y `class_weight="balanced"` en modelos adecuados.
- **Escalado**: aplicado **solo** en modelos sensibles a la escala (**Regresión Logística** y **KNN**).  
  Modelos basados en árboles (**Decision Tree**, **Random Forest**) **no** lo requieren.

---

## 🔍 Análisis Exploratorio Breve
- **Correlaciones con Churn**: mayor riesgo en `InternetService_fiber optic`, `PaymentMethod_Electronic check`, y mayor `Monthly`; menor riesgo con mayor **tenure** y **contratos largos**.
- **Análisis dirigido**:
  - **tenure × Churn**: clientes antiguos cancelan menos.
  - **Total × Churn**: menor gasto acumulado se asocia a más churn.
  - **Contract × Churn**: **Month-to-month** concentra la fuga; **Two year** la reduce fuertemente.
  - **PaymentMethod × Churn**: **Electronic check** con mayor churn.
  - **Monthly × Churn**: cuotas mensuales altas → mayor churn.

---

## 🤖 Modelos Implementados
1. **Regresión Logística** *(con StandardScaler + class_weight="balanced")*  
2. **KNN** *(con StandardScaler)*  
3. **Árbol de Decisión** *(sin escalado, class_weight="balanced")*  
4. **Random Forest** *(sin escalado, class_weight="balanced")*

---

## 📈 Resultados (Test)
> Métricas sobre la clase positiva **(Churn = 1)**.

| Modelo                | Accuracy | Precisión | Recall | F1   |
|----------------------|:--------:|:---------:|:------:|:----:|
| Regresión Logística  |  0.742   |   0.509   |  0.791 | 0.620|
| KNN                  |  0.780   |   0.594   |  0.540 | 0.566|
| Árbol de Decisión    |  0.735   |   0.500   |  0.786 | 0.611|
| Random Forest        |  0.773   |   0.556   |  0.719 | 0.627|

**Lectura rápida**  
- **Máximo recall (detectar churn):** Regresión Logística y Árbol (~0.79).  
- **Equilibrio general (Prec/Rec/F1):** Random Forest.  
- **KNN:** aceptable, pero el que menos recall obtiene.

---

## 🌟 Variables Más Influyentes
Hallazgos consistentes entre modelos:
- **Reducen churn**: **tenure** (antigüedad), **contratos de 1–2 años**, soporte/seguridad activos.
- **Aumentan churn**: **Internet de fibra óptica**, **Electronic check**, **cargos mensuales altos**, menor gasto acumulado.

---

## 📝 Conclusiones y Recomendaciones
- Si el objetivo es **no perder clientes en riesgo** (maximizar recall), **Regresión Logística** y **Árbol** son convenientes.  
- Si se busca **equilibrio** entre precisión y recall, **Random Forest** es la opción más estable.  

**Estrategias de retención sugeridas**:
- Incentivar **contratos de mayor plazo** (descuentos/beneficios).
- Acciones específicas para clientes con **fiber + electronic check** (ofertas, acompañamiento).
- Revisar **estructura de precios** para clientes con **Monthly** alto.
- Reforzar **soporte técnico** y servicios de valor (seguridad/backup).

---

## 🚀 Cómo clonar el repo:
1. Clonar el repo:
   ```bash
   git clone https://github.com/adcrx/TelecomChallenge2.git
   cd TelecomChallenge2

👩‍💻 Autora
Proyecto desarrollado por Alejandra Cotroneo como parte del programa Oracle Next Education (ONE) + Alura Latam.
