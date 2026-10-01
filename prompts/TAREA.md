# Tarea: Mi prompt avanzado

## Tarea elegida
La tarea seleccionada es la **generación automatizada de casos de prueba unitarios para un módulo de registro de usuarios**. 

---

## Version 1: prompt basico
```text
Crea casos de prueba para una función de registro de usuarios que recibe nombre, email y contraseña.
```
* **Qué técnica se agregó:** Ninguna. Es la instrucción base e inicial.
* **Por qué:** Se diseñó de esta forma para evaluar el comportamiento por defecto de la inteligencia artificial sin restricciones ni contexto técnico.
* **Qué mejoró en la respuesta:** La respuesta es una lista sumamente genérica y desordenada. Se enfoca en flujos visuales de interfaz en lugar de lógica de código, omitiendo por completo validaciones de seguridad, excepciones de infraestructura y límites de caracteres.

---

## Version 2
```text
Actúa como un QA Engineer y genera una lista de casos de prueba unitarios para una función de registro de usuarios que recibe nombre, email y contraseña. Divide los casos en escenarios exitosos y fallidos, y especifica datos de ejemplo para las entradas.
```
* **Qué técnica se agregó:** **Role Prompting** ("QA Engineer") y **Descomposición** (dividir los requerimientos en flujos de éxito y flujos de fallo).
* **Por qué:** Para guiar al modelo a adoptar una perspectiva profesional enfocada en la calidad y organizar el resultado final de forma lógica.
* **Qué mejoró en la respuesta:** Los casos de prueba ganaron una estructura mucho más limpia. Al exigir datos de ejemplo, se eliminó gran parte de la ambigüedad conceptual, permitiendo visualizar qué valores exactos causarían rechazos o aceptaciones en la función de registro.

---

## Version 3: prompt final
```text
[ROL Y CONTEXTO]
Actúa como un SDET (Software Development Engineer in Test) de Backend experto en ciberseguridad y APIs REST. Tu objetivo es diseñar una matriz de casos de prueba unitarios exhaustiva y técnica para una función crítica de registro de usuarios.

[ESPECIFICACIÓN DEL COMPONENTE]
La función bajo prueba procesa una solicitud HTTP POST con un payload JSON que contiene:
- `nombre`: string (Longitud: 2 a 50 caracteres. Restricción: solo letras alfabéticas y espacios).
- `email`: string (Restricción: formato válido según la especificación RFC 5322).
- `contrasena`: string (Longitud: mínimo 8 caracteres. Restricción: debe incluir al menos 1 mayúscula, 1 minúscula, 1 número y 1 carácter especial).

[ANÁLISIS SECUENCIAL (CHAIN OF THOUGHT)]
Antes de generar la matriz final, debes ejecutar un proceso de pensamiento analítico paso a paso estructurado de la siguiente manera:
1. Identifica las clases de equivalencia (valores válidos e inválidos) para cada uno de los tres campos de entrada.
2. Aplica la técnica de Análisis de Valores Límite (BVA) detallando los valores exactos en las fronteras de los rangos de longitud (ej. 1, 2, 50 y 51 caracteres).
3. Evalúa vectores de riesgo de inyección de código (SQL Injection y XSS) dentro de los campos de texto.
4. Identifica estados lógicos de dependencias externas (ej. el correo electrónico ya existe en la base de datos).

[EJEMPLO DE REFERENCIA (FEW-SHOT)]
Sigue este estándar técnico para documentar las entradas y los resultados esperados:
- ID: TC_REG_004
- Componente: Validación de Nombre
- Descripción: Registro fallido cuando el nombre tiene una longitud inferior al límite mínimo permitido (1 carácter).
- Entradas JSON: { "nombre": "A", "email": "usuario.valido@test.com", "contrasena": "Secr3t.P@ss!" }
- Resultado Esperado: Código HTTP 400 Bad Request. Cuerpo: { "error": "ValidationError", "message": "El nombre debe tener al menos 2 caracteres" }

[FORMATO DE RESPUESTA]
Genera tu salida estructurada estrictamente en las siguientes dos secciones markdown:
### 1. Pensamiento Analítico Previo (Análisis de límites, riesgos y equivalencias según las instrucciones de CoT)
### 2. Matriz de Casos de Prueba Unitarios (Tabla Markdown obligatoria con las columnas exactas: ID | Componente | Descripción | Entradas JSON | Resultado Esperado)

[AUTOCRÍTICA]
Una vez generada la tabla, realiza una breve revisión al final bajo el título "### 3. Reporte de Cobertura" donde verifiques explícitamente si omitiste algún escenario de borde de seguridad o de formato de correo. Si detectas alguna ausencia, agrega el caso de prueba correspondiente inmediatamente debajo de tu revisión.
```
* **Qué técnica se agregó:** **Few-Shot Prompting**, **Chain of Thought**, **Prompt Estructurado** y **Autocrítica**.
* **Por qué:** Se requería forzar un razonamiento lógico y de seguridad informática exhaustivo antes de emitir los resultados, garantizando un formato de salida rígido que no requiera reajustes manuales.
* **Qué mejoró en la respuesta:** La precisión de la IA se vuelve absoluta. Los objetos JSON generados son sintácticamente perfectos, las pruebas cubren con exactitud matemática los límites del negocio y la sección de autocrítica reduce drásticamente las omisiones de escenarios de seguridad comunes.

---

## Tecnicas usadas en el prompt final

La siguiente tabla describe de qué manera se distribuyen e implementan las técnicas avanzadas dentro de las etiquetas del prompt final:

| Componente del Prompt v3 | Técnica Aplicada | Propósito y Utilidad Técnica |
| :--- | :--- | :--- |
| `[ROL Y CONTEXTO]` | **Role Prompting** | Configura el comportamiento especializado. Usar "SDET de Backend" en lugar de un "experto" general inclina al modelo hacia un análisis riguroso de código, bases de datos y seguridad de APIs en lugar de pruebas visuales. |
| `[ANÁLISIS SECUENCIAL]` | **Chain of Thought** | Fuerza al modelo a realizar un desglose analítico y matemático en una secuencia ordenada antes de redactar la tabla, evitando omisiones conceptuales severas. |
| `[EJEMPLO DE REFERENCIA]` | **Few-Shot Prompting** | Proporciona un patrón inequívoco del nivel de detalle esperado, la sintaxis de las entradas JSON y la semántica de la respuesta esperada del servidor (códigos HTTP). |
| `[FORMATO DE RESPUESTA]` | **Prompt Estructurado** | Delimita las secciones mediante etiquetas claras (`[...]`) y define los títulos exactos de Markdown, eliminando introducciones conversacionales innecesarias. |
| `[AUTOCRÍTICA]` | **Autocrítica** | Obliga al modelo a evaluar su propio rendimiento en una segunda pasada, asegurando que se auto-audite antes de dar por finalizada la tarea. |

---

## Evaluacion del resultado

Esta matriz se utiliza para validar de forma binaria (Sí / No) si los resultados generados por el prompt final cumplen satisfactoriamente con los estándares profesionales:

| Criterio de Evaluación | Cumple (Sí / No) | Indicador de Éxito y Calidad |
| :--- | :--- | :--- |
| **¿La salida carece de texto conversacional introductorio?** | Sí | El modelo inicia directamente en el encabezado de la sección 1 sin saludar ni justificar su respuesta ("Claro, aquí tienes..."). |
| **¿Se incluyen casos específicos de inyección de código (SQL/XSS)?** | Sí | La matriz contiene escenarios de borde enfocados en neutralizar cargas maliciosas o scripts maliciosos en los campos de texto. |
| **¿Todos los ejemplos JSON son sintácticamente válidos?** | Sí | Los payloads no tienen errores sintácticos de comillas o llaves, estando listos para ser consumidos por herramientas de testing. |
| **¿El análisis cubre los límites exactos (BVA) especificados?** | Sí | La tabla evalúa de manera explícita las fronteras de los strings del requerimiento (longitud exacta de 1, 2, 50 y 51 caracteres). |

---

## Por que elegi estas tecnicas
Para la tarea de diseñar casos de prueba unitarios, la combinación de **Role Prompting **, **Chain of Thought**, **Few-Shot** y **Autocrítica** es la más idónea por encima de otras estrategias.


- [Tarea: mi prompt avanzado](prompts/TAREA.md)
