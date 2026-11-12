---
title: "Ejercicio 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## Qué son los agentes personalizados

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes de IA especializados para determinadas tareas o dominios del flujo de desarrollo. Se definen en archivos Markdown dentro de `.github/agents` y proporcionan a Copilot instrucciones, buenas prácticas, patrones de código y conocimientos específicos. Por ejemplo, un equipo puede crear un agente de accesibilidad que aplique las [directrices de accesibilidad para el contenido web (WCAG)][wcag], uno de seguridad o uno que mantenga patrones de pruebas coherentes.

Los agentes personalizados se definen en archivos Markdown dentro de `.github/agents` o, para uso global, de `~/.copilot/agents`. Cada archivo tiene frontmatter YAML con al menos `name` y `description`, seguido de instrucciones Markdown que describen el comportamiento, la experiencia y las responsabilidades del agente.

### Agentes personalizados y habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] se definen principalmente mediante Markdown y explican a la IA cómo realizar tareas. Una forma sencilla de distinguirlos: el **agente personalizado** es quien trabaja y las **habilidades** son las herramientas.

Los agentes personalizados tienen su propia ventana de contexto y pueden coordinar habilidades e incluso otros agentes. En este ejercicio, el agente de accesibilidad revisará el sitio según las directrices de accesibilidad y podría invocar habilidades para gestionar una solicitud de incorporación de cambios (PR) o ejecutar pruebas.

> [!NOTE]
> No hay una única forma correcta de crear un agente personalizado. Prueba e itera para encontrar lo que funciona en cada entorno y escenario.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

En este ejercicio explorarás:

- cómo se definen los agentes personalizados;
- cómo asignar una tarea a un agente personalizado.

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas. Algunos usuarios han señalado que el tema oscuro actual es difícil de leer por el bajo contraste entre el texto y el fondo. El equipo de diseño ha solicitado un modo de alto contraste que se pueda activar y desactivar.

Como la accesibilidad es importante, usarás un agente personalizado para implementar la funcionalidad.

## Revisar el agente de accesibilidad

Ya hay un agente personalizado de accesibilidad en el proyecto. Revisa sus instrucciones para comprender cómo orientará a Copilot.

1. Abre `.github/agents/accessibility.md`.
2. Observa los campos `name` y `description` del frontmatter YAML.

> [!CAUTION]
> El frontmatter con `name` y `description` es obligatorio para los agentes personalizados.

3. Revisa las secciones que describen las responsabilidades principales, las buenas prácticas de accesibilidad, ejemplos de HTML, CSS y JavaScript, y errores habituales.

## Crear y asignar una incidencia

Mission control es el lugar central para gestionar agentes. Puedes asignar tareas, supervisarlas y proporcionar instrucciones adicionales. Crearás una incidencia para el modo de alto contraste y la asignarás al agente de accesibilidad.

1. Abre el repositorio.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** y, después, **Blank issue**.
4. Escribe `Add high contrast mode to website` en **Title**.
5. Escribe lo siguiente en **Description**:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

6. Selecciona **Create** para crear la incidencia.
7. En el panel de la derecha, selecciona **Assign to Copilot**.
8. Selecciona **Accessibility agent** en la lista de agentes personalizados.

   ![Captura del diálogo de asignación del agente en la nube con el agente personalizado y Accessibility resaltados](../../../_images/ex5-select-custom-agent.png)

9. Selecciona **Assign**.

Copilot empezará a trabajar en segundo plano.

## Resumen y siguientes pasos

En este ejercicio, has:

- revisado el agente personalizado de accesibilidad;
- creado una incidencia y se la has asignado para implementar el modo de alto contraste.

A continuación, [supervisarás y dirigirás la sesión del agente desde mission control][next-lesson].

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar agentes personalizados para tu organización][org-custom-agents]
- [Preparar agentes personalizados para tu empresa][enterprise-custom-agents]

---

| [← Lección anterior: Agente en la nube de GitHub Copilot][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
