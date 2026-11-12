---
title: "Ejercicio 2 - Añadir funcionalidad con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso un cambio pequeño puede requerir editar varios archivos, ejecutar pruebas y corregir errores. El modo de agente de Copilot puede explorar el proyecto, hacer cambios coordinados, ejecutar tareas como las pruebas y corregir problemas detectados. En este ejercicio lo usarás para añadir una funcionalidad al sitio.

> [!NOTE]
> El modo de agente y el agente en la nube ofrecen experiencias distintas. El modo de agente trabaja en el IDE para que puedas interactuar y recibir resultados rápidamente. El agente en la nube trabaja de forma asíncrona, como un miembro del equipo, mediante incidencias y solicitudes de incorporación de cambios.

En este ejercicio aprenderás a:

- usar el modo de agente para explorar el proyecto, identificar archivos y hacer cambios coordinados;
- implementar funcionalidades en la interfaz y la capa de datos;
- revisar los cambios y las pruebas antes de combinarlos.

## Escenario

El catálogo de juegos crece y quieres permitir que los usuarios filtren por categoría y editorial. En el ejercicio anterior creaste un helper de editoriales. Ahora completarás el trabajo de la capa de datos, la interfaz y las pruebas con el modo de agente.

## Ejecutar el sitio web de Tailspin Toys

Antes de cambiar el código, explora el sitio para conocer su comportamiento actual. Tailspin Toys es una plataforma de financiación colectiva de juegos de mesa con temática de desarrollo. Es una única aplicación Astro que genera páginas HTML estáticas durante la compilación. Las páginas consultan directamente una base de datos SQLite local mediante Drizzle ORM; no hay una API de backend independiente ni un framework de interfaz del lado del cliente. Los helpers reutilizables de acceso a datos están en `src/lib/`, y la interactividad se implementa con scripts Astro acotados que usan las API estándar del DOM.

### Iniciar el sitio web

Inicia el servidor de desarrollo para examinar el sitio y, después, crea una rama para el filtrado.

1. Vuelve al codespace. Deberías estar en `main` después del ejercicio anterior.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

   Cuando el servidor Astro esté listo, aparecerá una dirección similar a esta:

   ```text
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si aparece un cuadro de diálogo para abrir `http://localhost:4321` en un navegador, ciérralo seleccionando **x**.

5. Abre el sitio manteniendo pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando `http://localhost:4321` en el terminal.

> [!NOTE]
> En Codespaces, al seleccionar el enlace localhost del terminal se abre una URL como `https://<your-codespace-name>-4321.app.github.dev/`. Es un túnel privado al servidor que se ejecuta en el codespace.

### Explorar el sitio web

Con el servidor en ejecución, revisa las páginas principales.

- **Home Page** muestra una lista de juegos con sus títulos, imágenes y descripciones.
- **Game Details Page** muestra más información del juego seleccionado, como el título, la descripción, la editorial y la categoría.

## Explorar la lista de trabajo con Copilot

La plantilla creó automáticamente una lista de incidencias. Pide a Copilot que la muestre y te ayude a priorizarla.

> [!TIP]
> **Abrir Copilot Chat**
>
> Vuelve al codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo pueden variar; se indicarán cuando sean relevantes.

1. En el menú desplegable de agentes de la vista Chat, selecciona **Agent**. El agente puede planificar y modificar varios archivos, ejecutar comandos de terminal y utilizar herramientas.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. En la lista de modelos disponibles, selecciona **Claude Sonnet 4.5**.

> [!CAUTION]
> La selección del modelo no expresa una preferencia de los autores. Se utilizó Claude Sonnet 4.5 al crear el taller para ofrecer resultados relativamente coherentes, pero las sugerencias pueden variar. Es normal.

> [!NOTE]
> Debido a la naturaleza probabilística de los modelos de lenguaje grandes (LLM), Copilot puede usar un comando distinto del Protocolo de contexto de modelo (MCP) y aun así completar la tarea.

3. Envía este prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para permitir que Copilot consulte las incidencias.
5. Revisa la lista y la priorización propuesta.

## Revisar los archivos de instrucciones

Antes de pedir a Copilot que genere código, revisa las instrucciones que orientarán su trabajo.

1. Abre `.github/instructions/ui.instructions.md`.
2. Lee las directrices de arquitectura, diseño de componentes, pruebas y accesibilidad, así como los enlaces a las instrucciones de Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden enlazar a otros archivos de instrucciones y a ejemplos del proyecto. Las rutas son relativas al archivo que contiene el enlace; así se pueden reutilizar directrices y dividir instrucciones complejas.

## Implementar el filtrado

Completar el filtrado requiere actualizar la capa de datos, las pruebas y la página de listado de juegos. Pide al agente que haga estos cambios y ejecute las pruebas antes de terminar.

1. Continúa la conversación actual o selecciona **New Chat** para iniciar otra.
2. Selecciona **Add Context**, **Instructions** y **ui** para añadir el archivo de instrucciones.

   ![Captura de la selección del archivo de instrucciones de interfaz](../../../_images/ex3-select-instructions-file.png)

3. Confirma que está seleccionado **Agent**.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Confirma que sigue seleccionado **Claude Sonnet 4.5**.
5. Envía este prompt para implementar los requisitos de la incidencia relacionada:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot explora el proyecto, localiza los helpers, la interfaz y las pruebas, modifica los archivos y ejecuta las pruebas.

   ![Captura de Copilot explorando archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> La tarea puede tardar varios minutos. Copilot explora, modifica archivos y ejecuta pruebas; durante el proceso pueden aparecer los controles **Keep** y **Undo**. No hace falta seleccionarlos mientras el agente sigue trabajando.

7. Cuando Copilot lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Captura del diálogo de Copilot Chat que pide permiso para ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Puede que Copilot haga pausas o que algunas pruebas fallen durante el proceso. Iterará entre la generación de código y las pruebas hasta completar la tarea sin detectar errores.
9. Revisa el código generado para detectar posibles problemas.

   ![Captura de una sesión completada con el modo de agente de Copilot](../../../_images/ex3-agent-mode-proposed-changes.png)

> [!CAUTION]
> Revisa siempre el código generado por Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador con el sitio en ejecución y prueba la nueva funcionalidad.
11. Cuando hayas revisado el código y confirmado que funciona, selecciona **Keep** en Copilot Chat.

## Resumen y siguientes pasos

En este ejercicio, has aprendido a:

- usar el modo de agente para explorar el proyecto, identificar los archivos pertinentes y hacer cambios coordinados;
- implementar funcionalidades en la interfaz y la capa de datos;
- revisar los cambios y las pruebas antes de combinarlos.

A continuación, [probarás la funcionalidad con el servidor MCP de Playwright][next-lesson] y abrirás una solicitud de incorporación de cambios.

### Ejercicio de exploración adicional: implementar paginación

La lista de juegos puede necesitar paginación a medida que crezca. Usa lo aprendido para pedir a Copilot que la implemente.

- Sigue las buenas prácticas y usa los archivos de instrucciones existentes.
- Decide si el usuario podrá elegir el tamaño de página o si será fijo.
- Incluye en el prompt las directrices necesarias para obtener el comportamiento deseado.
- Itera y aporta más contexto si hace falta; es normal trabajar así con Copilot.

## Recursos

- [Modos ask, edit y agent de Copilot: qué hacen y cuándo se usan][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
