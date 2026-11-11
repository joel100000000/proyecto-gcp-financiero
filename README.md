# PLANIFICACIÓN FINANCIERA CON GRADIENTES CONJUGADOS PRECONDICIONADOS

## Información del proyecto

**Estudiante:** Joel Choque Yujra  
**Universidad:** Universidad Mayor de San Andrés (UMSA)  
**Facultad:** Ciencias Puras y Naturales  
**Carrera:** Informática  
**Mención / Área:** Ingeniería de Sistemas  
**Asignatura:** Métodos Numéricos  

---

## 1. Descripción del proyecto

Este proyecto consiste en el desarrollo de una aplicación web interactiva para la resolución y análisis de un problema de planificación financiera mediante métodos numéricos.

El sistema plantea un modelo matemático de la forma:

**Ax = b**

donde:

- **A** representa la matriz de coeficientes y relaciones entre las unidades organizacionales.
- **x** representa las variables desconocidas asociadas a la asignación de recursos.
- **b** representa las necesidades o requerimientos de cada unidad.

El proyecto permite comparar diferentes métodos numéricos para resolver el sistema, principalmente:

- Método de Gauss.
- Factorización LU.
- Factorización de Cholesky.
- Gradientes Conjugados (GC).
- Gradientes Conjugados Precondicionados (GCP).

Además, se analizan los errores numéricos, el residuo, el condicionamiento de la matriz y el efecto del precondicionador de Jacobi.

---

## 2. Objetivo general

Desarrollar una aplicación web interactiva capaz de modelar, resolver y analizar un sistema financiero mediante métodos numéricos, permitiendo comparar la solución directa con los métodos iterativos de Gradientes Conjugados y Gradientes Conjugados Precondicionados.

---

## 3. Objetivos específicos

- Formular un sistema lineal **Ax = b** con cuatro variables.
- Justificar matemáticamente las variables utilizadas.
- Verificar que la matriz A sea simétrica.
- Verificar que la matriz A sea definida positiva.
- Implementar métodos directos para obtener una solución numérica de referencia.
- Implementar el método de Gradientes Conjugados.
- Implementar el método de Gradientes Conjugados Precondicionados.
- Utilizar el precondicionador de Jacobi.
- Comparar GC y GCP.
- Calcular el residuo relativo.
- Calcular el error absoluto, relativo y porcentual por variable.
- Calcular el número de condición de la matriz.
- Analizar el efecto del precondicionamiento.
- Construir los escenarios Ideal, Bajo Estrés y Mal Condicionado.
- Incorporar un módulo de pruebas QA.
- Presentar los resultados mediante una interfaz web intuitiva.

---

# 4. Caso financiero

## 4.1 Contexto

Se considera una organización que debe realizar una planificación de recursos entre cuatro unidades:

1. Infraestructura tecnológica.
2. Ciberseguridad.
3. Capacitación.
4. Innovación y desarrollo.

El sistema utiliza un modelo matemático para representar las necesidades de recursos y las relaciones entre estas unidades.

El propósito del modelo es obtener una asignación compatible con las restricciones representadas mediante el sistema lineal:

**Ax = b**

---

## 4.2 Variables

Las cuatro variables del modelo son:

- **x₁:** asignación de recursos para Infraestructura Tecnológica.
- **x₂:** asignación de recursos para Ciberseguridad.
- **x₃:** asignación de recursos para Capacitación.
- **x₄:** asignación de recursos para Innovación y Desarrollo.

Las variables se expresan en **Unidades Presupuestarias Normalizadas (UPN)**.

Una UPN es una unidad didáctica utilizada para representar capacidad o asignación de recursos dentro del modelo.

Esto significa que los resultados del programa no deben interpretarse automáticamente como bolivianos.

---

# 5. Modelo matemático

El modelo tiene la siguiente estructura:

**Ax = b**

donde:

### Matriz A

La matriz A representa las ponderaciones y relaciones entre las cuatro unidades.

Los elementos diagonales representan la intensidad del requerimiento propio de cada unidad.

Los elementos fuera de la diagonal representan acoplamientos entre unidades.

La matriz se construye simétrica:

**aᵢⱼ = aⱼᵢ**

Esto permite aplicar los métodos de Gradientes Conjugados.

### Vector x

El vector x contiene las cuatro asignaciones desconocidas:

**x = [x₁, x₂, x₃, x₄]ᵀ**

### Vector b

El vector b contiene las necesidades netas priorizadas de cada unidad.

---

# 6. Verificación de la matriz

Para utilizar correctamente Gradientes Conjugados, la matriz A debe ser:

- Simétrica.
- Definida positiva.

El programa realiza estas verificaciones automáticamente.

## Simetría

Se verifica que:

**aᵢⱼ = aⱼᵢ**

para todos los elementos de la matriz.

## Definición positiva

Para una matriz simétrica, se utiliza el criterio de Sylvester.

Los menores principales líderes deben ser positivos:

**D₁ > 0**

**D₂ > 0**

**D₃ > 0**

**D₄ > 0**

Además, el programa intenta realizar la factorización de Cholesky.

Si Cholesky es exitosa, se obtiene una evidencia adicional de que la matriz es definida positiva.

---

# 7. Escenarios

El programa incorpora tres escenarios.

## 7.1 Escenario Ideal

Representa una situación estable.

Las relaciones entre las unidades son moderadas y las escalas de los recursos son relativamente equilibradas.

Este escenario sirve como referencia para observar el comportamiento normal de los métodos numéricos.

---

## 7.2 Escenario Bajo Estrés

Representa una situación donde aumentan las necesidades de las unidades.

Se modifican tanto las necesidades del vector b como algunos coeficientes de la matriz A.

Esto permite analizar cómo responde el sistema ante una mayor presión operativa y financiera.

---

## 7.3 Escenario Mal Condicionado

Este escenario busca estudiar el efecto del mal escalamiento.

Se utiliza una transformación de la forma:

**A = DTD**

donde:

**D = diag(1, 10, 100, 1000)**

y T es una matriz simétrica definida positiva.

Debido a que D es no singular y T es definida positiva, A también conserva la definición positiva.

El objetivo es crear diferencias importantes de escala entre las variables y observar cómo esto afecta al número de condición y a la convergencia de los métodos iterativos.

---

# 8. Métodos numéricos implementados

## 8.1 Método de Gauss

Se utiliza eliminación con pivoteo parcial para resolver el sistema:

**Ax = b**

La solución obtenida sirve como referencia numérica.

---

## 8.2 Factorización LU

La matriz A se descompone como:

**A = LU**

donde:

- L es una matriz triangular inferior.
- U es una matriz triangular superior.

Posteriormente se resuelven los sistemas triangulares correspondientes.

---

## 8.3 Método de Cholesky

Debido a que A es simétrica definida positiva, se puede utilizar:

**A = LLᵀ**

donde L es triangular inferior.

Cholesky también se utiliza como una verificación adicional de la definición positiva de A.

---

# 9. Gradientes Conjugados

El método de Gradientes Conjugados permite resolver sistemas lineales simétricos definidos positivos.

El algoritmo comienza con una aproximación inicial:

**x₀**

y calcula el residuo:

**r₀ = b - Ax₀**

Posteriormente genera direcciones conjugadas para aproximarse progresivamente a la solución.

El proceso continúa hasta cumplir la tolerancia establecida o alcanzar el número máximo de iteraciones.

---

# 10. Gradientes Conjugados Precondicionados

El proyecto implementa el método GCP utilizando un precondicionador de Jacobi.

Se define:

**M = diag(A)**

En cada iteración se resuelve:

**Mzₖ = rₖ**

Como M es diagonal, esta operación se realiza de forma sencilla dividiendo cada componente del residuo entre el elemento correspondiente de la diagonal de A.

El precondicionamiento busca mejorar el comportamiento numérico del sistema y reducir el efecto del mal escalamiento.

---

# 11. Comparación GC vs GCP

El sistema compara:

- Número de iteraciones.
- Residuo relativo.
- Convergencia.
- Solución obtenida.
- Condicionamiento.

El objetivo no es afirmar que GCP siempre es superior a GC.

La aplicación muestra los resultados obtenidos para cada escenario y permite realizar una interpretación basada en evidencia numérica.

---

# 12. Análisis de errores

El sistema calcula los errores de cada variable tomando como referencia la solución obtenida mediante el método directo.

## Error absoluto

Se calcula mediante:

**Ea = |xref - xGCP|**

---

## Error relativo

Se calcula mediante:

**Er = Ea / |xref|**

Cuando la solución de referencia es cero, el error relativo no se define mediante esta expresión.

---

## Error porcentual

Se calcula mediante:

**Ep = Er × 100**

---

# 13. Residuo relativo

Después de obtener la solución aproximada, se calcula nuevamente el residuo:

**r = b - Ax**

y posteriormente:

**Residuo relativo = ||b - Ax||₂ / ||b||₂**

Esto permite comprobar qué tan bien satisface la solución aproximada el sistema original.

---

# 14. Número de condición

Para una matriz simétrica definida positiva se calcula:

**κ₂(A) = λmax / λmin**

donde:

- λmax es el mayor autovalor.
- λmin es el menor autovalor.

Un número de condición elevado indica que el sistema puede ser sensible a pequeñas perturbaciones de los datos.

---

# 15. Condicionamiento con Jacobi

Para el precondicionamiento Jacobi se utiliza:

**M = diag(A)**

El programa analiza la matriz simétrica equivalente:

**M⁻¹/² A M⁻¹/²**

y calcula su condición espectral.

Esto permite observar el efecto del escalamiento producido por el precondicionador.

---

# 16. Interfaz web

La aplicación está dividida en módulos:

1. Inicio.
2. Cómo utilizar el programa.
3. Caso financiero.
4. Modelo matemático.
5. Datos y ejecución.
6. Escenarios.
7. Solución directa.
8. Comparación GC vs GCP.
9. Errores y condicionamiento.
10. Comparación global.
11. Pruebas QA.
12. Conclusiones y referencias.

La interfaz está diseñada para que el usuario pueda realizar el análisis sin conocimientos avanzados de programación.

---

# 17. Funcionamiento de la aplicación

Para utilizar el programa:

### Paso 1

Abrir:

`finanzas_numericas_gcp_mejorado.html`

con Google Chrome, Microsoft Edge, Firefox u otro navegador moderno.

### Paso 2

Seleccionar uno de los escenarios:

- Ideal.
- Bajo Estrés.
- Mal Condicionado.

### Paso 3

Revisar la matriz A y el vector b.

### Paso 4

Seleccionar el método directo:

- Cholesky.
- LU.
- Gauss.

### Paso 5

Seleccionar el precondicionador:

- Jacobi.
- Sin precondicionador.

### Paso 6

Mantener inicialmente:

**Tolerancia = 0.000001**

**Máximo de iteraciones = 1000**

### Paso 7

Presionar:

**Ejecutar análisis**

### Paso 8

Revisar:

- Solución de referencia.
- Solución GC.
- Solución GCP.
- Iteraciones.
- Residuo.
- Errores.
- Número de condición.

### Paso 9

Generar la comparación de los tres escenarios.

### Paso 10

Ejecutar todas las pruebas QA.

---

# 18. Pruebas QA

La aplicación incorpora pruebas funcionales para comprobar el comportamiento del sistema.

## Prueba 1: Carga de escenarios

Comprueba que los tres escenarios sean:

- Simétricos.
- Definidos positivos.
- Aptos para los métodos de Gradientes Conjugados.

## Prueba 2: Matrices inválidas

Comprueba que el sistema rechace:

- Matrices no simétricas.
- Matrices simétricas que no sean definidas positivas.

## Prueba 3: Edición dinámica

Se modifica un coeficiente de la matriz desde la interfaz.

El sistema debe:

1. Detectar el cambio.
2. Recalcular la solución.
3. Actualizar los resultados.
4. Permitir restaurar el valor original.

## Prueba 4: Comparación GC/GCP

Se utiliza el escenario mal condicionado para comparar:

- GC.
- GCP con Jacobi.

Se revisa si ambos métodos convergen y cuántas iteraciones necesitan.

---

# 19. Arquitectura del sistema

El proyecto utiliza una arquitectura sencilla de aplicación web cliente.

## Capa de presentación

Está formada por:

- HTML.
- CSS.
- JavaScript.
- Formularios.
- Tablas.
- Gráficos.
- Navegación.

## Capa de lógica numérica

Contiene:

- Gauss.
- LU.
- Cholesky.
- GC.
- GCP.
- Jacobi.
- Cálculo de residuos.
- Cálculo de errores.
- Condicionamiento.

## Capa de datos

Contiene los tres escenarios:

- Ideal.
- Bajo Estrés