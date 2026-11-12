---
title: "Ejercicio 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## Qué son los agentes personalizados

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes de IA especializados para determinadas tareas o dominios del flujo de desarrollo. Se definen en archivos Markdown dentro de `.github/agents` y proporcionan a Copilot instrucciones, buenas prácticas, patrones de código y conocimientos específicos. Por ejemplo, un equipo puede crear un agente de accesibilidad que aplique las [directrices de accesibilidad para el contenido web (WCAG)][wcag], uno de seguridad o uno que mantenga patrones de pruebas coherentes.

Los agentes personalizados se definen en archivos Markdown dentro de `.github/agents` o, para uso global, de `~/.copilot/agents`. Cada archivo tiene frontmatter YAML con al menos `name` y `description`, seguido de instrucciones que describen el comportamiento, la experiencia y las responsabilidades del agente.

### Agentes personalizados y habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] se definen principalmente mediante Markdown y explican a la IA cómo realizar tareas. Una forma sencilla de distinguirlos: el **agente personalizado** es quien trabaja y las **habilidades** son las herramientas.

Los agentes tienen su propia ventana de contexto y pueden coordinar habilidades e incluso otros agentes. En este ejercicio, el agente de accesibilidad revisará el sitio según las directrices de accesibilidad y podría invocar habilidades para gestionar una solicitud de incorporación de cambios (PR) o ejecutar pruebas.

> [!NOTE]
> No hay una única forma correcta de crear un agente personalizado. Prueba e itera para encontrar lo que funciona en cada entorno y escenario.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas. Algunos usuarios han señalado que el tema oscuro actual es difícil de leer por el bajo contraste entre el texto y el fondo. El equipo de diseño ha solicitado un modo de alto contraste que se pueda activar y desactivar.

En este ejercicio, vas a:

- revisar un agente personalizado de accesibilidad existente;
- usar el agente en Copilot Chat para implementar un modo de alto contraste.

## Revisar el agente personalizado de accesibilidad

Ya hay un agente personalizado de accesibilidad en el proyecto. Revisa sus instrucciones para comprender cómo orientará a Copilot.

1. Vuelve al codespace y, en un terminal, crea una rama desde `main` para mantener separada la tarea de accesibilidad de la PR de filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. Abre `.github/agents/accessibility.md`.
3. Observa los campos `name` y `description` del frontmatter YAML.

> [!CAUTION]
> El frontmatter con `name` y `description` es obligatorio para los agentes personalizados.

4. Revisa las secciones de responsabilidades para generar un sitio accesible, buenas prácticas, ejemplos de HTML, CSS y JavaScript, y errores habituales.

## Usar el agente personalizado en Copilot Chat

VS Code muestra los agentes personalizados definidos en `.github/agents` en el menú desplegable de agentes de Copilot Chat. Seleccionar uno aplica sus instrucciones y herramientas a la conversación.

> [!TIP]
> **Abrir Copilot Chat**
>
> Vuelve al codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo pueden variar; se indicarán cuando sean relevantes.

1. En el menú desplegable de agentes de la vista Chat, selecciona **Agent**, si aún no está seleccionado.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Abre el menú de agentes situado en la parte inferior de la vista Chat. De forma predeterminada muestra **default**.
3. Selecciona **Accessibility agent** en la lista.
4. Envía este prompt:

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot explorará el código, propondrá cambios y editará los archivos del proyecto. Cada edición aparecerá en el chat con la ruta del archivo y las diferencias para revisar.
6. Observa el indicador **Files changed**, que se actualiza con los archivos modificados por el agente.

> [!NOTE]
> El proceso puede tardar varios minutos. Copilot puede editar componentes Astro, CSS y pruebas relacionadas.

En el siguiente ejercicio revisarás y dirigirás el trabajo mientras sigue en curso.

## Resumen y siguientes pasos

En este ejercicio, has:

- revisado un agente personalizado de accesibilidad existente;
- usado el agente en Copilot Chat para implementar el modo de alto contraste.

A continuación, [supervisarás y dirigirás el trabajo del agente][next-lesson], revisarás los cambios y pedirás un modo claro en la misma sesión.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]
- [Agentes personalizados en awesome-copilot][awesome-copilot-agents]

---

| [← Lección anterior: Probar la funcionalidad con Playwright MCP][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
