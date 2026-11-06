## 1. Resumen del Proyecto

**SmartRisk v2** es una solución de asesoramiento financiero algorítmico (*Robo-Advisor*) y gestión cuantitativa de carteras desarrollada en Python. El sistema automatiza el ciclo completo de inversión: desde la evaluación del perfil de riesgo del inversor y la categorización estructurada de activos, hasta la optimización matemática de asignación de capital mediante la **Frontera Eficiente de Markowitz** y la proyección estocástica de trayectorias mediante **Simulación de Monte Carlo**.

---

## 2. ¿Por qué se desarrolló este proyecto? (Motivación Personal y Racional Financiero)

### Motivación Personal y Académica
El origen de este proyecto coincidió con un período en el que comencé a profundizar de manera autodidacta e influenciado por la materia "Mercado de valores" en la dinámica de esta área, la renta variable y la teoría moderna de inversiones. Al tener que desarrollar el proyecto final para la materia de **Estructuras de Datos**, quise evitar los ejercicios académicos convencionales y desafiarme a construir una aplicación real que fusionara dos mundos: la rigurosidad computacional de la ingeniería de software y la modelación cuantitativa de finanzas de mercado. 

El reto consistió en demostrar cómo conceptos algorítmicos avanzados (árboles n-arios, colas dinámicas, algoritmos de ordenamiento híbridos) son indispensables para procesar, clasificar y simular portafolios de inversión a gran escala sin comprometer el rendimiento computacional.

### Racional Financiero y de Mercado
En la práctica profesional de la gestión de activos (*Asset Allocation*), existen problemas estructurales que la tecnología cuantitativa resuelve:

* **Eliminación de la subjetividad y sesgos de comportamiento:** Vincular de forma matemática el apetito de riesgo de un cliente con la composición de su cartera, evitando decisiones reactivas ante la volatilidad del mercado.
* **Optimización matemática del capital:** Superar las asignaciones heurísticas tradicionales encontrando las ponderaciones que maximizan el retorno por unidad de riesgo asumido (Sharpe Ratio sobre la Frontera Eficiente).
* **Medición estocástica del riesgo de cola (*Tail Risk*):** Los modelos deterministas fallan al proyectar el rendimiento a largo plazo. Era fundamental integrar simulaciones que incorporen la correlación de retornos, aportes periódicos recurrentes (estrategia DCA) y métricas de estrés financiero extremo (VaR 95% y CVaR / Expected Shortfall).

---

## 3. Motores Cuantitativos y Algorítmicos

### A. Motor de Optimización de Markowitz (SciPy SLSQP)
Resuelve numéricamente problemas de programación no lineal (*Sequential Least Squares Programming*):
* **Maximización de Sharpe Ratio:** 
* **Minimización de Varianza:** Halla la cartera de mínima volatilidad para perfiles de riesgo conservadores.
* **Trazado de la Frontera Eficiente:** Realiza un barrido dinámico de retornos objetivo discretizados (e.g., 60 puntos) para mapear el conjunto de carteras óptimas en el espacio riesgo-retorno.

### B. Motor de Simulación de Monte Carlo (Geometric Brownian Motion)
Proyección de escenarios de evolución patrimonial:
* **Ecuación Estocástica:**
* **Proyección a 5,000 Trayectorias:**
* **Modelado de Liquidez y DCA (*Dollar-Cost Averaging*):** Simula inyecciones periódicas mensuales recalculando el crecimiento del capital aportado a lo largo del tiempo.
* **Métricas de Estrés y Riesgo de Pérdida:**
  * **Value at Risk (VaR 95%):** Pérdida máxima probable en el 95% de los escenarios simulados.
  * **Conditional VaR (CVaR 95% / Expected Shortfall):** Promedio de pérdida en el 5% de los peores escenarios del mercado.
  * **Maximum Drawdown (MDD):** Estimación de la caída máxima de valor desde un pico histórico sobre la trayectoria mediana.
  * **CAGR Mediano y Probabilidad de Pérdida de Capital.**

### C. Estructuras de Datos y Algoritmos Implementados
A nivel de ciencias de la computación, el núcleo del sistema prescinde de cajas negras y aplica estructuras implementadas desde cero:
* **Árbol Jerárquico de Activos (`AssetCategoryTree`):** Estructura de árbol n-ario con métodos de recorrido *Pre-order* y *Post-order* para indexar, consultar y organizar clases de activos (Acciones, ETFs, Bonos soberanos/corporativos, Commodities, REITs) con complejidad $O(\log n)$.
* **Cola de Procesamiento de Reportes (`DownloadQueue`):** Implementación de lista enlazada dinámica (FIFO) con punteros *head* y *tail* para administrar exportaciones y solicitudes de descarga de manera asíncrona sin sobrecargar memoria.
* **Algoritmo de Ordenamiento Híbrido (`SimulationSorter`):** Sistema adaptativo que conmuta entre **MergeSort** (ordenamiento estable en memoria) y **QuickSort** (eficiencia temporal promedio $O(n \log n)$) para clasificar miles de trayectorias simuladas según percentiles de capital o riesgo.
* **Sanitización y Validación Expresiva (`StringValidator`):** Validación estricta con expresiones regulares (RegEx) para tickers bursátiles estandarizados y control de entrada en la plataforma.

---

## 4
