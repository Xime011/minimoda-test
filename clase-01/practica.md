# Práctica 01 — Testing con Inteligencia Artificial

**Aplicación bajo prueba:** [MiniModa](https://minimoda-navy.vercel.app/)  
**Módulo:** Registro de usuarios  
**URL:** [https://minimoda-navy.vercel.app/registro](https://minimoda-navy.vercel.app/registro)  
**Fecha:** 02/11/2026  
**Herramientas utilizadas:** Gemini, ChatGPT y Qase  
**Tipo de testing:** QA Manual — Testing funcional

---

## 1. Preparación y exploración de MiniModa

MiniModa es una aplicación web de demostración que simula un comercio electrónico de ropa infantil.

Incluye funcionalidades habituales de una tienda online, como catálogo de productos, filtros, carrito de compras, registro de usuarios y proceso de compra.

La aplicación utiliza datos ficticios y no procesa pagos reales.

Para esta práctica seleccioné el módulo de **Registro de usuarios**, que permite evaluar validaciones de formularios mediante diferentes técnicas de diseño de pruebas.

### Restricciones identificadas

| Campo                  | Restricción                                                          |
| ---------------------- | -------------------------------------------------------------------- |
| Edad                   | Número entero entre 13 y 120 años                                    |
| Contraseña             | Longitud mínima de 8 caracteres                                      |
| Confirmar contraseña   | Debe coincidir con la contraseña, según el comportamiento verificado |
| Email                  | Debe cumplir con un formato válido                                   |
| País                   | Selector de países                                                   |
| Términos y condiciones | Checkbox de aceptación                                               |

Las restricciones de edad y longitud de contraseña están expresamente indicadas en el formulario.

Las demás validaciones requieren comprobación mediante pruebas o documentación funcional adicional.

---

## 2. Selección de superficie de IA

Para realizar el ejercicio utilicé la modalidad **Chat**, sin recurrir a herramientas de línea de comandos (CLI).

Trabajé con dos herramientas:

**Gemini:** mediante el asistente integrado en Chrome, que permite realizar consultas sobre la página web abierta sin necesidad de copiar y pegar su URL.

**ChatGPT:** desde su interfaz web, para contrastar, revisar y mejorar los casos de prueba generados inicialmente.

Esta modalidad permitió mantener una interacción mediante lenguaje natural, solicitar modificaciones y analizar los resultados de manera progresiva.

---

## 3. Exploración con Gemini: tres preguntas, aciertos y observaciones

Realicé tres preguntas a Gemini mientras navegaba por MiniModa.

### Pregunta 1: ¿De qué se trata esta web?

Gemini identificó que se trataba de una tienda online de ropa infantil.

**Evaluación:** La respuesta fue correcta y coherente con el propósito de la aplicación.

### Pregunta 2: ¿Cómo supiste que es una demo?

Gemini identificó que la aplicación se presenta como una tienda de demostración, con datos ficticios y sin pagos reales.

**Evaluación:** La respuesta fue correcta y estuvo fundamentada en información disponible en la página.

### Pregunta 3: ¿Qué páginas encontraste?

Gemini describió las diferentes secciones disponibles dentro de la aplicación.

**Evaluación:** No identifiqué inconsistencias en la respuesta obtenida durante la exploración.

### Aciertos identificados

Gemini reconoció correctamente el propósito de MiniModa, su carácter demostrativo y las funcionalidades principales.

Las respuestas fueron pertinentes y me permitieron comprender la aplicación antes de comenzar el diseño de los casos de prueba.

### Errores o posibles invenciones

No detecté errores verificables en las tres respuestas iniciales.

Sin embargo, posteriormente, durante la revisión de los casos de prueba generados por Gemini, identifiqué algunos resultados esperados que incluían comportamientos no confirmados por los requisitos visibles.

Estas inconsistencias se desarrollan en el apartado 4.

### Diferencias observadas entre Gemini y ChatGPT

Ambas herramientas proporcionaron información correcta, aunque con diferentes niveles de detalle.

Gemini respondió específicamente a cada una de las tres preguntas formuladas.

ChatGPT, en cambio, proporcionó una descripción más amplia de la aplicación desde la primera consulta, incluyendo información relacionada con las tres preguntas iniciales.

**Considero que esta diferencia no representa una limitación de Gemini, sino distintas formas de responder y organizar la información.**

---

## 4. Generación y revisión de casos de prueba con IA

### 4.1. Generación inicial con Gemini

Para la actividad debía solicitar una propuesta de **6 casos de prueba** para el módulo de registro.

Al realizar la consulta, Gemini generó una respuesta más extensa que incluía **13 casos de prueba**.

Los casos estaban organizados según las siguientes técnicas:

- Pruebas positivas o Happy Path.
- Análisis de valores límite (Boundary Value Analysis).
- Pruebas negativas (Negative Testing).

Los escenarios contemplaban registro exitoso, validaciones de edad, longitud de contraseña, campos obligatorios, formato de email y confirmación de contraseña.

La propuesta fue adecuada como punto de partida para el diseño de pruebas funcionales.

### 4.2. Contraste con ChatGPT

Posteriormente, compartí los 13 casos con ChatGPT y solicité una revisión desde el rol de QA Manual profesional.

El objetivo fue:

- Contrastar los casos con los requisitos conocidos.
- Identificar posibles inconsistencias.
- Mejorar la precisión de los resultados esperados.
- Evaluar la aplicación de técnicas de testing.
- Detectar escenarios adicionales.
- Seleccionar los casos más representativos.

ChatGPT propuso ampliar la cobertura a 28 escenarios.

Sin embargo, esa ampliación fue utilizada únicamente como análisis complementario, ya que el ejercicio no requería documentar ni ejecutar todos esos casos.

### 4.3. Revisión crítica de 6 casos generados por Gemini

Seleccioné seis casos de los trece originales para evaluar su precisión, detectar posibles inconsistencias y proponer mejoras.

| ID original | Escenario                   | Evaluación QA                    | Hallazgo                                                                   |
| ----------- | --------------------------- | -------------------------------- | -------------------------------------------------------------------------- |
| CP-REG-01   | Registro exitoso            | Inconsistencia                   | Se presupone la creación de una cuenta real sin evidencia de persistencia. |
| CP-REG-03   | Edad inferior al mínimo: 12 | Correcto                         | Aplica adecuadamente análisis de valores límite.                           |
| CP-REG-08   | Campos obligatorios vacíos  | Requiere precisión               | No se confirmó que todos los campos deban mostrar mensajes individuales.   |
| CP-REG-10   | Contraseñas diferentes      | Correcto                         | El comportamiento esperado fue confirmado mediante ejecución manual.       |
| CP-REG-11   | Edad decimal o alfabética   | Mejorable                        | Combina dos condiciones de prueba diferentes.                              |
| CP-REG-12   | País no seleccionado        | Requisito pendiente de confirmar | Se presupone que el campo es obligatorio sin una especificación explícita. |

### Análisis de los hallazgos

#### CP-REG-01 — Registro exitoso

**Resultado esperado propuesto por Gemini:**

> El sistema procesa el registro correctamente, crea la cuenta y redirige o muestra un mensaje de éxito.

**Inconsistencia identificada:**

La aplicación es una demostración y no está confirmada la persistencia de cuentas reales.

El resultado esperado presupone que el sistema crea una cuenta, aunque el comportamiento visible únicamente permite verificar la confirmación del registro.

Además, plantea dos posibles resultados alternativos: redirección o mensaje de éxito.

**Mejora propuesta:**

El sistema valida los datos ingresados y muestra una confirmación de registro exitoso.

**Clasificación:** Supuesto funcional no confirmado.

---

#### CP-REG-03 — Edad inferior al límite mínimo

**Dato de prueba:** Edad = 12.

**Resultado esperado de Gemini:**

El sistema muestra un error indicando que la edad debe ser mayor o igual a 13.

**Evaluación:**

El caso está correctamente diseñado.

Utiliza un valor inmediatamente inferior al límite mínimo permitido.

Durante la ejecución manual, el formulario rechazó el valor y mostró el mensaje:

> La edad debe estar entre 13 y 120.

**Clasificación:** Caso correcto, confirmado mediante prueba manual.

---

#### CP-REG-08 — Campos obligatorios vacíos

**Resultado esperado propuesto por Gemini:**

> El sistema impide el envío del formulario y resalta todos los campos obligatorios con mensajes de error de campo requerido.

**Observación:**

El escenario negativo es válido, pero el resultado esperado presupone que todos los campos son obligatorios y que cada uno debe mostrar un mensaje individual.

Estas condiciones no estaban completamente especificadas en la información disponible.

**Mejora propuesta:**

Identificar previamente qué campos son obligatorios y verificar que el formulario impida el registro cuando alguno de ellos no tenga un valor válido.

**Clasificación:** Resultado esperado con supuestos pendientes de confirmar.

---

#### CP-REG-10 — Confirmación de contraseñas diferentes

**Datos de prueba:**

- Contraseña: `Password123`
- Confirmación: `Password321`

**Resultado esperado de Gemini:**

El sistema muestra un mensaje indicando que las contraseñas no coinciden.

**Evaluación:**

El caso está correctamente planteado.

Durante la ejecución manual, el sistema impidió completar el registro y mostró:

> Las contraseñas no coinciden.

**Clasificación:** Caso correcto, confirmado mediante prueba manual.

---

#### CP-REG-11 — Edad con decimales o caracteres no numéricos

**Datos de prueba propuestos por Gemini:**

- Edad = `25.5`
- Edad = `veinticinco`

**Observación:**

El caso combina dos condiciones de entrada diferentes.

Aunque ambas entradas son inválidas según el requisito de edad, podrían producir comportamientos distintos.

Por ejemplo, el campo podría impedir el ingreso de letras, pero permitir escribir un número decimal y rechazarlo durante la validación.

**Mejora propuesta:**

Separar el escenario en dos casos independientes:

- Verificar rechazo de edades decimales.
- Verificar rechazo de caracteres alfabéticos en el campo Edad.

Esto permite mejorar la trazabilidad y facilitar la identificación de defectos.

**Clasificación:** Oportunidad de mejora en el diseño del caso, no un requisito inventado.

---

#### CP-REG-12 — País no seleccionado

**Resultado esperado propuesto por Gemini:**

El sistema muestra un error indicando que debe seleccionarse un país válido.

**Observación:**

El comportamiento resulta razonable para un formulario de registro, pero la obligatoriedad del selector no estaba expresamente definida en las restricciones consultadas.

**Mejora propuesta:**

Confirmar si el campo País es obligatorio.

En caso afirmativo, verificar que el sistema impida completar el registro cuando permanezca seleccionada la opción predeterminada.

**Clasificación:** Regla funcional pendiente de confirmar.

---

### 4.4. Conclusión de la revisión

De los seis casos analizados:

| Clasificación                              | Cantidad |
| ------------------------------------------ | -------: |
| Correctos y confirmados mediante ejecución |        2 |
| Con supuestos funcionales no confirmados   |        3 |
| Con oportunidades de mejora en el diseño   |        1 |
| **Total**                                  |    **6** |

La revisión permitió identificar que Gemini generó escenarios funcionales adecuados, pero algunos resultados esperados incorporaban comportamientos no respaldados por requisitos explícitos.

**La principal inconsistencia fue el caso CP-REG-01**, que afirmaba la creación de una cuenta sin que se hubiera comprobado su persistencia.

Esto demuestra la importancia de revisar las respuestas generadas por IA y diferenciar los requisitos confirmados de los supuestos funcionales.

---

## 5. Comparación entre herramientas de IA

**Gemini:** permitió explorar MiniModa mediante tres preguntas específicas y generó una primera propuesta de 13 casos de prueba, organizada según técnicas de testing.

**ChatGPT:** proporcionó una descripción más amplia de la aplicación en su respuesta inicial y permitió revisar críticamente los casos de Gemini, detectar inconsistencias y proponer mejoras.

**Conclusión:** ambas herramientas fueron útiles y complementarias; las diferencias observadas correspondieron principalmente al nivel de detalle, la forma de responder y el tipo de tarea solicitada.

---

## 6. Selección de los tres mejores casos y documentación en Qase

A partir de la revisión, seleccioné tres casos representativos y los documenté en **Qase**, dentro del proyecto MiniModa y la suite Registro.

Los casos fueron:

1. Registro exitoso con datos válidos.
2. Registro con edad inferior al mínimo permitido.
3. Confirmación de contraseñas diferentes.

La selección permite evaluar un flujo positivo, una regla de negocio mediante valores límite y una validación negativa de credenciales.

### Documentación en Qase

Los casos incluyen:

- Título y objetivo.
- Precondiciones.
- Datos de prueba.
- Pasos de ejecución.
- Resultados esperados.
- Prioridad.
- Clasificación funcional.

### 6.1. Caso 1 — Registro exitoso

**Qase ID:** 1
**Prioridad:** Alta
**Tipo:** Funcional positivo
**Técnica:** Partición de equivalencia

**Objetivo:** Verificar que el formulario permita completar el proceso de registro utilizando datos válidos.

**Precondiciones:**

- Aplicación accesible.
- Formulario de registro disponible.

**Datos de prueba:**

| Campo                  | Valor                                                |
| ---------------------- | ---------------------------------------------------- |
| Nombre                 | María Gómez                                          |
| Email                  | [maria.gomez@test.com](mailto\:maria.gomez@test.com) |
| Contraseña             | Password123                                          |
| Confirmar contraseña   | Password123                                          |
| Edad                   | 25                                                   |
| País                   | Argentina                                            |
| Términos y condiciones | Aceptados                                            |

**Pasos:**

1. Acceder a `/registro`.
2. Completar los campos con datos válidos.
3. Aceptar los términos y condiciones.
4. Hacer clic en Crear cuenta.

**Resultado esperado:**

El formulario procesa correctamente los datos y muestra una confirmación de registro exitoso.

**Resultado actual observado:**

El sistema mostró una confirmación visual de registro exitoso:

> ¡Registro exitoso! Bienvenida/o a MiniModa, María Gómez. Te enviamos un email de bienvenida (ver Bandeja).

**Evaluación:** Coincide con lo esperado.

**Evidencia:**



**Observación:** La prueba confirma el comportamiento visible del formulario, pero no verifica la creación de una cuenta persistente ni el envío efectivo de un correo electrónico.

---

### 6.2. Caso 2 — Registro con edad inferior al mínimo permitido

**Qase ID:** 2
**Prioridad:** Alta
**Tipo:** Funcional negativo
**Técnica:** Análisis de valores límite

**Objetivo:** Verificar que el formulario rechace edades inferiores a 13 años.

**Precondiciones:**

- Formulario disponible.
- Resto de campos completados con valores válidos.

**Datos de prueba:**

Edad = `12`.

**Pasos:**

1. Acceder a `/registro`.
2. Completar los campos con datos válidos.
3. Ingresar 12 en Edad.
4. Aceptar los términos y condiciones.
5. Hacer clic en Crear cuenta.

**Resultado esperado:**

El sistema impide completar el registro e informa que la edad debe estar entre 13 y 120 años.

**Resultado actual observado:**

El sistema mostró:

> Revisá los campos marcados.

Y debajo del campo Edad:

> La edad debe estar entre 13 y 120.

No se mostró la confirmación de registro exitoso.

**Evaluación:** Coincide con lo esperado.

**Evidencia:**



---

### 6.3. Caso 3 — Confirmación de contraseña diferente

**Qase ID:** 3
**Prioridad:** Alta
**Tipo:** Funcional negativo

**Objetivo:** Verificar que el formulario rechace el registro cuando la contraseña y su confirmación no coincidan.

**Precondiciones:**

- Formulario disponible.
- Resto de campos completados con valores válidos.

**Datos de prueba:**

| Campo                | Valor           |
| -------------------- | --------------- |
| Contraseña           | Password123     |
| Confirmar contraseña | Password321     |
| Edad                 | 25              |
| Resto de campos      | Valores válidos |

**Pasos:**

1. Acceder a `/registro`.
2. Completar los campos con datos válidos.
3. Ingresar `Password123` en Contraseña.
4. Ingresar `Password321` en Confirmar contraseña.
5. Aceptar los términos y condiciones.
6. Hacer clic en Crear cuenta.

**Resultado esperado:**

El sistema impide completar el registro e informa que las contraseñas no coinciden.

**Resultado actual observado:**

El sistema mostró:

> Revisá los campos marcados.

Y debajo de Confirmar contraseña:

> Las contraseñas no coinciden.

No se mostró la confirmación de registro exitoso.

**Evaluación:** Coincide con lo esperado.

**Evidencia:**



---

### 6.4. Resumen de la ejecución manual

| Caso                               | Resultado esperado       | Resultado observado          | Evaluación |
| ---------------------------------- | ------------------------ | ---------------------------- | ---------- |
| Qase ID 1 — Registro exitoso       | Confirmación de registro | Mensaje de éxito             | Correcto   |
| Qase ID 2 — Edad = 12              | Bloqueo del registro     | Error de edad fuera de rango | Correcto   |
| Qase ID 3 — Contraseñas diferentes | Bloqueo del registro     | Error de coincidencia        | Correcto   |

**Resultado general:** Los tres escenarios presentaron comportamientos visibles acordes con sus resultados esperados.

Las evidencias corresponden a capturas obtenidas durante la ejecución manual.

La exportación JSON de Qase permitió verificar la documentación de los casos, pero no incluía los estados del Test Run. Por lo tanto, este resumen no implica que las tres ejecuciones estén registradas formalmente como Passed dentro de Qase.

### 6.5. Observación adicional sobre Qase

Durante la revisión del JSON exportado detecté que el caso de edad inferior al mínimo estaba clasificado como `behavior: positive`.

Sin embargo, corresponde clasificarlo como **Negative**, ya que verifica la respuesta del sistema ante un dato inválido.

Esta observación corresponde a la clasificación del caso dentro de Qase y no a un defecto de MiniModa.

---

## 7. Mapa del harness

Durante la práctica identifiqué los siguientes componentes:

| Componente          | Herramienta utilizada                                 | Función                                                                                                                |
| ------------------- | ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Modelo**          | Gemini y GPT-6                                        | Interpretaron las consultas y generaron o revisaron los casos de prueba.                                               |
| **App**             | Asistente de Gemini integrado en Chrome y ChatGPT web | Interfaces utilizadas para interactuar con los modelos mediante lenguaje natural.                                      |
| **Harness**         | Entornos de ejecución de Gemini y ChatGPT             | Administraron las interacciones, el contexto y las herramientas disponibles. No configuré directamente estos entornos. |
| **MCP**             | No utilizado explícitamente                           | No configuré servidores MCP durante la práctica.                                                                       |
| **Skills o reglas** | Prompts e instrucciones de QA manual                  | Orientaron la generación, revisión y selección de casos. No creé skills personalizadas.                                |

### Diferencias entre los componentes

**Modelo:** Sistema de inteligencia artificial que interpreta las instrucciones y genera las respuestas.

**App:** Interfaz desde la que el usuario interactúa con el modelo.

**Harness:** Entorno encargado de coordinar la ejecución, administrar el contexto y proporcionar herramientas al agente.

**MCP:** Protocolo que permite conectar aplicaciones de IA con herramientas y fuentes externas.

**Skills o reglas:** Instrucciones y procedimientos que orientan el comportamiento del agente.

Durante la práctica utilicé prompts para indicar las tareas y solicitar criterios de revisión profesional, pero no desarrollé skills reutilizables.

Qase se utilizó como herramienta de gestión de pruebas y no como servidor MCP.

---

## 8. Conclusiones

Esta práctica me permitió trabajar con dos herramientas de inteligencia artificial en diferentes etapas del proceso de QA Manual.

**Gemini** facilitó la exploración inicial de MiniModa y la generación de casos de prueba.

**ChatGPT** permitió realizar una revisión crítica de los casos, identificar supuestos no confirmados, mejorar su diseño y proponer escenarios adicionales.

El análisis de seis casos de Gemini permitió distinguir tres situaciones:

- Casos correctamente diseñados.
- Resultados esperados basados en supuestos no confirmados.
- Casos que podían mejorarse mediante una separación más precisa de las condiciones de prueba.

La principal inconsistencia identificada fue asumir que el formulario creaba una cuenta real cuando únicamente se había comprobado una confirmación visual de registro.

También observé que Gemini y ChatGPT respondieron de diferentes maneras, sin que esto representara necesariamente una limitación de alguna de las herramientas.

Posteriormente, seleccioné tres casos y los documenté en Qase.

Durante la ejecución manual, los tres mostraron comportamientos acordes con sus resultados esperados.

### Aprendizajes principales

La IA puede resultar útil para agilizar la exploración de aplicaciones, el diseño de escenarios y la revisión de casos de prueba.

Sin embargo, es fundamental que el QA:

- Verifique los requisitos antes de establecer resultados esperados.
- Distinga los supuestos de los comportamientos confirmados.
- Aplique técnicas de diseño de pruebas.
- Priorice escenarios según su relevancia.
- Contraste las respuestas generadas por IA con el funcionamiento real de la aplicación.

**Conclusión final:**

La IA funciona como una herramienta de apoyo para QA, pero no reemplaza el análisis crítico, la validación de requisitos ni la ejecución de pruebas.
