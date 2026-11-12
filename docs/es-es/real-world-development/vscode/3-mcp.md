---
title: "Ejercicio 3 - Probar la funcionalidad con el Protocolo de contexto de modelo (MCP) de Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Modo de agente][previous-lesson] · [Siguiente lección: Agentes personalizados →][next-lesson]

Has creado la funcionalidad de filtrado con el modo de agente. Antes de abrir una solicitud de incorporación de cambios (PR), comprobarás que funciona en el navegador. Configurarás el servidor MCP de Playwright para que Copilot controle un navegador real, pruebe la funcionalidad y te ayude a publicar la rama y abrir una PR.

En este ejercicio, vas a:

- aprender qué es Model Context Protocol (MCP) y cómo amplían sus servidores las herramientas de Copilot;
- añadir el servidor MCP de Playwright al espacio de trabajo;
- pedir a Copilot que pruebe el filtrado en un navegador;
- publicar la rama y abrir una PR con los cambios.

## Qué es Model Context Protocol (MCP)

El modo de agente puede usar herramientas ajenas al editor mediante Model Context Protocol (MCP), un estándar que permite al agente comunicarse con herramientas y servicios externos.

![Diagrama del funcionamiento del modo de agente y su interacción con el contexto, el modelo de lenguaje y las herramientas, incluidas las que proporcionan los servidores MCP y las extensiones de VS Code](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) permite que los agentes de IA se comuniquen con herramientas y servicios externos en tiempo real. Así pueden acceder a información actualizada mediante recursos y realizar acciones mediante herramientas.

Los servidores MCP actúan como puente entre el agente y las herramientas y servicios. Cada servidor ofrece un conjunto diferente de herramientas y recursos.

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)** proporciona acceso a interfaces de programación de aplicaciones (API) para gestionar repositorios de GitHub, crear y actualizar repositorios, y gestionar incidencias y solicitudes de incorporación de cambios.
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)** proporciona automatización del navegador mediante Playwright, por ejemplo, para abrir páginas, rellenar formularios y activar controles.

GitHub mantiene un [registro de MCP](https://github.com/mcp) para facilitar el descubrimiento y las contribuciones.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Antes de usar uno, revisa su código fuente, comprueba quién lo publica y valora las implicaciones de seguridad. Usa solo servidores de confianza y ten cuidado al conceder acceso a recursos u operaciones sensibles.

## Revisar la configuración de MCP

El archivo `.vscode/mcp.json` configura los servidores MCP disponibles en este espacio de trabajo.

1. Abre `.vscode/mcp.json` en el codespace.
2. Confirma que ya está configurado el servidor `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

La plantilla incluye esta entrada y por eso Copilot pudo consultar la lista de incidencias en el ejercicio anterior. Usa el servidor remoto de GitHub MCP; VS Code se conecta mediante HTTP y te autentica la primera vez que Copilot utiliza una herramienta.

## Añadir el servidor MCP de Playwright

Añade un segundo servidor para que Copilot pueda controlar un navegador y probar la funcionalidad.

1. En `.vscode/mcp.json`, añade una entrada `playwright` junto a `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Guarda el archivo.

El servidor `playwright` es local: VS Code lo inicia en tu equipo con `npx @playwright/mcp@latest`. La opción `--headless` ejecuta el navegador sin una ventana visible, necesaria en un codespace sin escritorio.

> [!NOTE]
> Tailspin Toys ya usa Playwright para las pruebas de extremo a extremo, por lo que normalmente el navegador ya está instalado. Si Copilot indica que falta, pídele que ejecute `npx playwright install chromium` y vuelve a intentarlo.

## Iniciar y confiar en el servidor

VS Code inicia los servidores MCP cuando se necesitan y pide confirmar que confías en ellos.

1. En `.vscode/mcp.json`, selecciona **Start**, que aparece encima de la entrada `playwright`, para iniciar el servidor y comprobar la configuración.
2. Si VS Code pregunta si confías en el servidor, revisa la configuración y confirma que confías en él.

El inicio manual es opcional. Si lo omites, VS Code iniciará el servidor y pedirá que confirmes la confianza cuando Copilot necesite sus herramientas.

## Probar la funcionalidad de filtrado

Playwright MCP proporciona a Copilot un navegador real. El agente puede abrir el sitio, aplicar filtros y resumir lo que observa. El servidor usa el [árbol de accesibilidad][playwright-mcp-server] de la página en lugar de capturas de pantalla; así, el agente razona sobre elementos etiquetados como botones, enlaces y listas, como hace la tecnología de asistencia.

Con el servidor conectado y la aplicación en ejecución, pide a Copilot que pruebe el filtrado:

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot abrirá el navegador, seguirá los pasos y comunicará los resultados. Compara el informe con los criterios de aceptación de la incidencia. Si algo no funciona como esperabas, pide más información o solicita que corrija el código antes de crear la PR.

> [!NOTE]
> Para esta prueba, la aplicación debe estar en ejecución en `http://localhost:4321`. Si el servidor de desarrollo está detenido, inícialo antes de enviar el prompt. La primera vez que se use Playwright MCP, Copilot puede necesitar descargar un navegador; si indica que falta, pídele que ejecute `npx playwright install chromium`.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publicar la rama y crear una solicitud de incorporación de cambios

Cuando hayas comprobado la funcionalidad, publica la rama `filtering-vscode` para que el equipo pueda revisar los cambios.

1. Abre **Source Control** en el codespace y revisa los cambios de Copilot.
2. Prepara los cambios seleccionando el icono **+**.
3. Genera un mensaje de confirmación con el botón **Sparkle**.

   ![Captura del panel Source Control con los cambios realizados](../../../_images/ex3-source-control-changes.png)

4. Selecciona **Publish** para enviar la rama al repositorio.

## Crear la solicitud de incorporación de cambios

Copilot puede localizar la incidencia y crear una PR asociada a ella.

1. Abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva.
2. Confirma que está seleccionado **Agent** para que Copilot pueda usar las herramientas de GitHub.
3. Envía este prompt:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Si Copilot lo solicita, selecciona **Continue** para permitirle consultar información y realizar acciones. La primera vez que use una herramienta de GitHub, puede pedirte que inicies sesión.
5. Comprueba que Copilot localiza la incidencia correcta y crea la PR.
6. Selecciona el enlace de Copilot para revisar la PR, pero **no la combines todavía**.

## Resumen y siguientes pasos

En este ejercicio, has:

- aprendido qué es Model Context Protocol (MCP) y cómo amplían sus servidores las herramientas de Copilot;
- añadido Playwright MCP al espacio de trabajo;
- usado el servidor para probar manualmente la funcionalidad de filtrado en el navegador;
- publicado la rama y abierto una solicitud de incorporación de cambios.

A continuación, [crearás un agente personalizado][next-lesson] para agilizar tareas concretas como las revisiones de accesibilidad.

## Recursos

- [¿Qué es MCP y por qué todo el mundo habla de ello?][mcp-blog-post]
- [Servidor MCP de Playwright de Microsoft][playwright-mcp-server]
- [Servidor MCP de GitHub][github-mcp-server]
- [Registro de servidores MCP][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
