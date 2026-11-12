---
title: "Ejercicio 5 - Personalizar y usar una habilidad de comprobaciones de calidad"
description: "Explora la habilidad de comprobaciones de calidad existente, personaliza el formato de sus resultados y úsala para validar el filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Programar no consiste solo en escribir código. Hemos podido validar manualmente que el código funciona y hemos usado archivos de instrucciones para asegurarnos de que sigue nuestros estándares. Pero ¿qué ocurre con las pruebas, el lint y las demás tareas de integración continua (CI)?

Para este tipo de tareas, las **habilidades de agente** son la mejor opción. Las habilidades ayudan a Copilot a entender cómo ejecutar operaciones como estas.

En este ejercicio aprenderás a:

- explorar la habilidad `quality-checks` existente.
- personalizar el formato de los resultados.
- volver a cargar la habilidad y ejecutarla.

## Escenario

Tailspin Toys usa la habilidad `quality-checks` para ejecutar pruebas unitarias, lint y comprobaciones de tipos. El equipo quiere mejorar el informe para que los resultados sean más fáciles de leer.

## Instrucciones, scripts y recursos

Las habilidades de agente agrupan instrucciones de tareas reutilizables, scripts ejecutables y recursos auxiliares que un agente carga cuando los necesita. En esencia, son una carpeta con el nombre de la habilidad que contiene un archivo Markdown llamado `SKILL.md`. El archivo Markdown incluye metadatos de frontmatter con un nombre y una descripción para definir la habilidad, una introducción sobre su función y directrices sobre cuándo debe invocarse. La carpeta también puede incluir subcarpetas con scripts y otros recursos que la habilidad puede usar.

> [!NOTE]
> Las subcarpetas y los archivos adicionales no son obligatorios. La habilidad `quality-checks` de Tailspin Toys solo contiene `SKILL.md` porque usa los comandos que ya existen en el proyecto.

Las habilidades pueden estar en la carpeta `.github/skills` de un proyecto, como recurso del repositorio que el equipo puede compartir y reutilizar, o en la carpeta de habilidades del usuario, `~/.copilot/skills`.

## Explorar la habilidad

Vamos a explorar la habilidad `quality-checks` que ha creado el equipo de Tailspin Toys para ejecutar pruebas unitarias, lint y comprobaciones de tipos.

1. Vuelve a tu Codespace. En el editor de Codespaces, abre `.github/skills/quality-checks/SKILL.md`.
2. Lee el `name` y la `description` de la parte superior. La descripción ayuda a Copilot a decidir cuándo invocar la habilidad.
3. Lee las instrucciones y fíjate en cómo guían a Copilot durante las pruebas y el lint.
4. Observa que todavía no hay una sección **Results output formatting** en la habilidad.

## Ejecutar la habilidad antes de hacer un cambio

Puedes invocar las habilidades directamente desde Copilot CLI o usando lenguaje natural. Pidámosle a Copilot que ejecute las tres comprobaciones de la habilidad.

1. Vuelve a la conversación sobre el filtrado en modo interactivo.
2. Usa el siguiente prompt:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Lee el informe que aparece al final.

## Personalizar el informe

Vamos a mejorar el informe para que indique qué se ha ejecutado, si ha terminado correctamente y qué resultados han devuelto las herramientas. Añadiremos esa información a la habilidad.

1. Vuelve a `.github/skills/quality-checks/SKILL.md`.
2. Añade la siguiente sección al final del archivo:

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. El archivo se guarda automáticamente.

## Ejecutar la habilidad actualizada

Después de hacer el cambio, comprobaremos cómo funciona. Copilot CLI puede volver a cargar las habilidades editadas sin reiniciar la conversación.

1. Escribe:

   ```plaintext
   /skills reload
   ```

2. Usa el mismo prompt que antes:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Lee el informe final y compáralo con el primero.

## Resumen y siguientes pasos

Has personalizado y usado una habilidad de agente existente. En este ejercicio has:

- explorado la habilidad `quality-checks` para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- personalizado el formato de sus resultados.
- vuelto a cargar la habilidad y la has ejecutado.

Ese cambio se incluirá junto con el filtrado en la solicitud de cambios de la funcionalidad. A continuación, permitirás que Copilot interactúe directamente con el sitio mediante el [servidor del Protocolo de contexto de modelo (MCP) de Playwright][next-lesson].

## Más ejemplos de habilidades

Estos ejemplos de la comunidad son referencias, no tareas adicionales:

- [Especificación de Agent Skills][skill-spec]
- [Flujo de contribución: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas y un script de exportación incluido: `drawio`][drawio-example]
- [Pruebas en el navegador: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
