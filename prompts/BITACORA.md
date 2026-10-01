# Bitacora de tecnicas avanzadas
Laboratorio 07: Tecnicas Avanzadas de Prompting.
Herramienta de IA usada: (escribe aqui cual usaste)
## Ejercicio 2: Zero-shot, one-shot y few-shot

| Tipo | Aciertos (de 5) | Formato de la respuesta | Todas con el mismo formato (Si/No) |
| :--- | :---: | :--- | :---: |
| Zero-shot | 5 | Libre | Sí |
| One-shot | 5 | Texto-etiqueta | Sí |
| Few-shot | 5 | Texto-etiqueta | Sí |


## Ejercicio 3: Chain of Thought
| Pedido | Respuesta de la IA | Muestra los pasos (Si/No) | Correcta (Si/No) |
|--------|--------------------|---------------------------|------------------|
| Directo |318.6 |No |Si |
| Paso a paso |318.60 |No |Si |

## Ejercicio 4: Role prompting

| Versión | Vocabulario (sencillo/técnico) | ¿Usa ejemplos o código? | ¿A quién le sirve más? |
| :--- | :--- | :--- | :--- |
| A. Sin rol |sencillo |si |a usuarios comunes,estudiantes |
| B. Rol docente |tecnico |si |profesionales que deseen reolver problemas y dudas |
| C. Rol senior |tecnico |si |personas mas capactiadas que necesitan entender o reforzar el tema con mayor rapidez de la manera mas eficaz |


## Ejercicio 5: Descomposicion
1- Me mando los requisitos que se debe cumplir para crear el sistema de inventario

2-Ha creado las clases necesarias para poder crear el proyectoy ha explicado su funcionalidad.

3-Me dio el código de java con todas las clases q ha creado anteriormente.

4-Ha mejorado el codigo 


## Ejercicio 6: Prompt estructurado y autocritica
```text
<rol>Actua como analista de pruebas de software.</rol>
<contexto>Login web con correo y contrasena. La cuenta se bloquea
despues de 3 intentos fallidos.</contexto>
<tarea>Piensa paso a paso que puede fallar y escribe 6 casos de prueba.</tarea>
<formato>Tabla con las columnas: ID, escenario, datos de entrada,
resultado esperado.</formato>
Revisa tu tabla: faltan casos limite como campos vacios, correo sin @
o contrasena con espacios? Agrega los que falten e indica cuales agregaste.
```

- [Bitacora de tecnicas avanzadas](prompts/BITACORA.md)


