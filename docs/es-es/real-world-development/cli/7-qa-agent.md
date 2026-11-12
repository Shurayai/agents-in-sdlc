---
title: "Lección 7 - Crear y usar un agente de control de calidad"
description: "Crea un agente personalizado de control de calidad (QA) que combine requisitos, la habilidad quality-checks y el servidor del Protocolo de contexto de modelo (MCP) de Playwright."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has usado la habilidad `quality-checks` para ejecutar comprobaciones automatizadas y el servidor del Protocolo de contexto de modelo (MCP) de Playwright para observar la experiencia de filtrado en el navegador. Ahora reunirás esas capacidades en un agente personalizado con un proceso de control de calidad (QA) definido.

En esta lección, vas a:

- explorar cómo un agente personalizado usa instrucciones, habilidades y herramientas MCP;
- crear y revisar un perfil reutilizable de control de calidad;
- seleccionar el agente y revisar sus conclusiones sobre la incidencia de filtrado.

## Escenario

Tailspin Toys necesita revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador antes de abrir una solicitud de incorporación de cambios (PR).

## Qué es un agente personalizado

Un agente personalizado es una versión especializada de Copilot definida en un perfil Markdown. El perfil describe el propósito, las instrucciones y las herramientas disponibles. Las instrucciones del repositorio establecen los estándares; `quality-checks` agrupa comprobaciones repetibles; Playwright MCP proporciona herramientas de navegador; y el perfil de control de calidad coordina su uso e informa de los resultados.

## Crear el perfil de control de calidad

Pide al agente predeterminado que cree un perfil reutilizable y define con claridad las comprobaciones y los límites.

1. Vuelve al Codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Envía este prompt:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Revisar el perfil

Comprueba que el agente respeta el proceso de control de calidad y no tiene permisos de actuación que no hayas solicitado.

1. Ejecuta `/diff` y abre `.github/agents/qa.agent.md`.
2. Revisa el frontmatter. `description` es obligatorio; `name` es opcional, pero proporciona un nombre visible.
3. Confirma que las instrucciones cubren los requisitos, las instrucciones del repositorio, `quality-checks` y Playwright MCP.
4. Confirma que el agente aporta pruebas, pregunta antes de cambiar código de implementación y no crea commits ni PR.
5. Si falta alguna responsabilidad o límite, pide al agente predeterminado que lo corrija antes de continuar.

## Ejecutar el control de calidad sobre la incidencia

Reanuda la conversación de filtrado y selecciona el nuevo perfil para que pueda usar el contexto de la incidencia y el plan.

1. Activa el agente con:

   ```plaintext
   /agent QA
   ```

2. Pide al agente que revise la funcionalidad:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. Lee el informe y revisa las pruebas que aporta.

> [!NOTE]
> Si el agente recién creado no aparece en la lista, ejecuta `/agent QA` para activarlo.

## Resumen y siguientes pasos

En esta lección, has:

- explorado cómo un agente personalizado usa instrucciones, habilidades y herramientas MCP;
- creado y revisado un perfil reutilizable de control de calidad;
- seleccionado el agente y revisado sus conclusiones sobre la incidencia de filtrado.

Ya tienes la implementación, la actualización de la habilidad, el perfil de control de calidad, las pruebas y el informe de verificación. A continuación, [revisarás el conjunto y crearás la PR de funcionalidad][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
