---
slug: es-es/real-world-development/cloud
title: "Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

El [agente en la nube de GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent) permite que GitHub Copilot trabaje de forma asíncrona en la nube. Asigna trabajo en GitHub y el agente explora el repositorio, realiza cambios y abre una solicitud de incorporación de cambios (PR) mientras tú te ocupas de otras tareas.

En estos ejercicios añadirás instrucciones personalizadas que seguirá el agente, le asignarás incidencias y revisarás su trabajo. También explorarás agentes personalizados, supervisarás sesiones y dirigirás las iteraciones desde el panel de agentes.

## Ejercicios

| Ejercicio | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea el repositorio y un codespace |
| [1. Instrucciones personalizadas][ex1] | Contexto | Añade instrucciones para el agente en la nube |
| [2. Agente en la nube][ex2] | Agente asíncrono | Asigna incidencias al agente en la nube de Copilot |
| [3. Agentes personalizados][ex3] | Agentes especializados | Revisa y utiliza agentes personalizados |
| [4. Gestionar agentes][ex4] | Supervisión | Supervisa y dirige las sesiones de agente |
| [5. Iterar][ex5] | Revisión | Revisa las PR, itera sobre el trabajo de Copilot y elige los siguientes pasos |

## Requisitos previos

Antes de asistir a este taller, necesitas:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] El agente en la nube de Copilot habilitado para tu cuenta u organización

> [!TIP]
> Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye el agente, MCP, la revisión de código y Copilot CLI que se utilizan en este taller.

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> El agente en la nube está disponible en los planes **Copilot Student, Pro, Pro+, Business y Enterprise**, pero no en Copilot Free. En Copilot Business o Enterprise, un administrador debe habilitarlo para la organización.

> [!NOTE]
> Este recorrido no cubre el Protocolo de contexto de modelo (MCP). Para aprender a usar servidores MCP con Copilot, consulta el [taller de CLI][cli-workshop] o el [taller de VS Code][vscode-workshop].

## Empezar

**[Empieza por los requisitos previos][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
[cli-workshop]: ../cli/
[vscode-workshop]: ../vscode/
