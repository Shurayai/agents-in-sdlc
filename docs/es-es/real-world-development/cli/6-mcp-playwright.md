---
title: "Lección 6 - Validar la funcionalidad con Playwright y el Protocolo de contexto de modelo (MCP)"
description: "Configura Playwright MCP en Copilot CLI y úsalo para explorar en el navegador la funcionalidad de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Los servidores Model Context Protocol (MCP) amplían Copilot CLI con herramientas y servicios externos. En esta lección, añadirás el servidor MCP de Playwright si aún no está disponible y pedirás al agente que explore la funcionalidad de filtrado en un navegador.

En esta lección, vas a:

- conocer Model Context Protocol (MCP) y cómo lo usa Copilot CLI;
- añadir el servidor MCP de Playwright si aún no está disponible;
- pedir al agente que controle un navegador para explorar el filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero también conviene interactuar con la interfaz para verificar sus cambios. Playwright MCP permite que Copilot use el sitio web como lo haría una persona.

## Acerca de MCP

[Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de IA se comuniquen con herramientas y servicios externos. Un servidor MCP actúa como puente y proporciona un conjunto de herramientas y recursos.

- **[GitHub MCP Server][github-mcp]** proporciona acceso a las API para gestionar repositorios, incidencias y solicitudes de incorporación de cambios.
- **[Playwright MCP Server][playwright-mcp-server]** proporciona automatización del navegador mediante Playwright.

GitHub mantiene un [registro de MCP][mcp-registry] para facilitar el descubrimiento y las contribuciones.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Antes de usar uno, revisa su código fuente, verifica quién lo publica y valora las implicaciones de seguridad.

## Añadir el servidor MCP de Playwright

Si Playwright MCP ya está configurado en Copilot CLI, omite la configuración y continúa con la prueba.

1. Vuelve al Codespace.
2. En Copilot CLI, ejecuta:

   ```plaintext
   /mcp add
   ```

3. Escribe `playwright` como nombre y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo de servidor **STDIO** con <kbd>Enter</kbd> y pulsa <kbd>Tab</kbd>.
5. Introduce este comando en el diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar.
7. Pulsa <kbd>Esc</kbd> para salir del diálogo.

## Pedir a Copilot que explore la funcionalidad

Pide a Copilot que inicie la aplicación, compruebe el filtrado con Playwright MCP y no haga cambios.

1. Envía este prompt:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

2. Observa los pasos que ejecuta Copilot en el navegador y lee el informe.
3. Confirma que el comportamiento coincide con la incidencia y el plan.

> [!NOTE]
> Copilot suele seleccionar MCP por su cuenta, pero indicar el servidor en el prompt ayuda a que el flujo sea más consistente.

## Resumen y siguientes pasos

En esta lección, has:

- aprendido qué es el Protocolo de contexto de modelo (MCP) y cómo lo usa Copilot CLI;
- añadido el servidor MCP de Playwright si aún no estaba disponible;
- pedido al agente que controlase un navegador para explorar el filtrado.

A continuación, [crearás un agente personalizado de control de calidad][next-lesson] que combinará la habilidad y las herramientas del navegador.

## Recursos

- [¿Qué es MCP y por qué todo el mundo habla de ello?][mcp-blog-post]
- [Servidor MCP de Playwright de Microsoft][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
