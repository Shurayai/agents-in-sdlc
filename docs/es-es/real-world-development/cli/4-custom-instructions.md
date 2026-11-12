---
title: "Lección 4 - Guiar a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es importante cuando se trabaja con IA generativa. Los archivos de instrucciones describen no solo qué código quieres, sino también cómo debe estructurarse. Ahora que has creado el filtrado, explorarás las instrucciones utilizadas por Copilot, añadirás un estándar de documentación y lo aplicarás al código.

En esta lección, vas a:

- explorar cómo las instrucciones del repositorio y las instrucciones específicas de rutas llegan al agente;
- actualizar el archivo de instrucciones para que se respeten los estándares de código;
- comprobar el efecto de las instrucciones en el código generado.

## Escenario

Tailspin Toys aplica directrices de desarrollo: los comentarios deben explicar la intención y las decisiones no evidentes; las funciones exportadas de `db/` y `src/lib/` deben documentar su propósito, parámetros y valores devueltos con TSDoc/JSDoc; los componentes Astro reutilizables deben documentar sus contratos `Props`; y deben conservarse las directrices de formato y lint.

## Archivos de instrucciones

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot. El repositorio puede tener instrucciones globales y otras específicas para determinados archivos o tareas.

- `.github/copilot-instructions.md` se envía a Copilot en todas las solicitudes del repositorio y contiene directrices generales.
- `.github/instructions/*.instructions.md` contiene instrucciones para lenguajes, tipos de archivo o tareas concretos.

> [!NOTE]
> Los formatos de instrucciones disponibles varían según el entorno. Consulta la [referencia de compatibilidad de instrucciones personalizadas][custom-instructions-support] antes de depender de un formato concreto.

## Explorar las instrucciones existentes

Revisa los archivos incluidos en el proyecto para conocer las directrices que ya recibe Copilot.

1. Vuelve al Codespace y abre `.github/copilot-instructions.md` en el editor.
2. Lee la descripción del proyecto y las directrices aplicables a todas las interacciones con Copilot.
3. Explora los archivos de `.github/instructions`, incluidas las instrucciones de Astro, Drizzle y pruebas.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`, que determina los archivos a los que se aplican las instrucciones.
5. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otras instrucciones y a archivos de ejemplo.

## Añadir un estándar a las instrucciones

Añade una directriz general para que el nuevo código TypeScript incluya documentación.

1. En `.github/copilot-instructions.md`, localiza la sección **Code formatting guidance**.
2. Añade este elemento al final de la sección:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

3. Guarda el archivo.

## Aplicar las instrucciones actualizadas

Copilot CLI carga las instrucciones del repositorio al iniciar una conversación. Reanuda la conversación de filtrado para aplicar la nueva directriz sin perder el contexto.

1. Si la conversación sigue abierta, ejecuta `/exit`.
2. Desde la raíz del repositorio en la rama `game-filters-cli`, reanuda la conversación:

   ```bash
   copilot --resume
   ```

3. Si se te solicita, selecciona la conversación de filtrado y confirma que está activa la rama `game-filters-cli`.
4. Pide a Copilot que aplique las instrucciones:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

5. Ejecuta `/diff`, revisa los archivos TypeScript y confirma que los comentarios TSDoc describen el código.

## Resumen y siguientes pasos

En esta lección, has:

- explorado cómo las instrucciones del repositorio y las instrucciones específicas de rutas llegan al agente;
- actualizado el archivo de instrucciones para que se respeten los estándares de código;
- comprobado el efecto de las instrucciones en el código generado.

A continuación, [personalizarás y ejecutarás la habilidad reutilizable `quality-checks`][next-lesson].

## Recursos

- [Añadir instrucciones personalizadas para Copilot CLI][instruction-files]
- [Compatibilidad con instrucciones personalizadas][custom-instructions-support]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[next-lesson]: ../5-agent-skills/
