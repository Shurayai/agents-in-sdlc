---
title: "Ejercicio 4 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los últimos ejercicios has asignado tres tareas al agente en la nube de Copilot para mejorar la experiencia y añadir funcionalidades. Aunque trabaja de forma autónoma y asíncrona, es importante supervisar las tareas.

La [página de agentes][agents-page] de GitHub.com permite consultar las tareas con solicitudes de incorporación de cambios abiertas, revisar las operaciones realizadas y orientar las sesiones que siguen en curso.

En este ejercicio, vas a:

- explorar la página de agentes para supervisar las tareas;
- dirigir una sesión en curso para pedir una funcionalidad adicional.

## Escenario

Después de asignar el modo de alto contraste, el equipo decidió añadir también un modo claro. Como el agente ya está trabajando en los estilos y los controles, le pedirás que incluya esta función en la tarea en curso.

## Revisar las tareas del agente en la nube

Abre la página de agentes y revisa el estado de las tareas asignadas.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Revisa las tareas del panel principal y del panel izquierdo. Deberías encontrar las tareas que asignaste, entre ellas:
   - actualizar la documentación del código;
   - generar API para modificar juegos;
   - añadir un modo de alto contraste al sitio.
3. Selecciona una tarea en curso y revisa las operaciones realizadas. Pueden incluir la obtención del código, la preparación del entorno, la configuración de servidores MCP y los pasos para completar la tarea.

> [!NOTE]
> Los pasos exactos dependen del estado de la tarea y del enfoque que siga Copilot.

4. Revisa el panel de solicitudes de incorporación de cambios (PR) de la derecha para consultar la PR y los archivos modificados.

## Dirigir la sesión del agente en la nube

Ahora que has visto las tareas activas, pedirás al agente que añada el modo claro mientras implementa el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título puede variar según el nombre que Copilot dé a la tarea y su estado.

   ![Sesión de accesibilidad en mission control](../../../_images/ex6-accessibility-session.png)

2. Espera a que termine la configuración y empiece el trabajo. Verás mensajes que indican que la implementación ha comenzado.
3. En el diálogo **Steer active session while Copilot is working**, escribe este prompt:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Captura de la tarea del agente en la página de agentes con el diálogo para dirigir una sesión activa resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Comprueba que Copilot lo reconoce y lo incorpora al trabajo.

## Dejar que Copilot continúe

Copilot incorporará la nueva solicitud cuando termine el paso que estaba ejecutando. El agente seguirá trabajando en la tarea actualizada de forma asíncrona.

## Resumen y siguientes pasos

En este ejercicio, has:

- explorado la página de agentes para supervisar las tareas del agente en la nube;
- dirigido una sesión activa para solicitar otra funcionalidad.

A continuación, [iterarás sobre las solicitudes de incorporación de cambios creadas por Copilot][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
