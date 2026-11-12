---
slug: es-es/real-world-development/cli
title: "GitHub Copilot CLI"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI](https://docs.github.com/copilot/concepts/agents/about-copilot-cli)** incorpora GitHub Copilot al terminal como asistente de programación con agentes. Explora bases de código, genera código, ejecuta comandos y se conecta a herramientas externas desde la línea de comandos.

El taller sigue un flujo continuo de Tailspin Toys: prepararás el proyecto e instalarás Copilot CLI; implementarás y combinarás las valoraciones por estrellas; planificarás e implementarás el filtrado; actualizarás las instrucciones, la habilidad de comprobaciones y el perfil de control de calidad; y revisarás la funcionalidad con el servidor del Protocolo de contexto de modelo (MCP) de Playwright antes de crear y combinar la segunda solicitud de incorporación de cambios (PR) con Agent Merge. También explorarás comandos de barra para gestionar contexto, modelos, sesiones y delegación opcional. Puedes continuar con la [serie opcional de tres módulos con GitHub Copilot CLI y Foundry][foundry].

## Ejercicios

| Ejercicio | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y tu codespace |
| [1. Instalación de Copilot CLI][ex1] | Instalación | Instala y autentica Copilot CLI |
| [2. Añadir valoraciones por estrellas][ex2] | Primer cambio | Muestra las valoraciones existentes y el estado sin valoración, y combina tu primera PR |
| [3. Modos de agente: Plan y Autopilot][ex3] | Modos de agente | Planifica el filtrado a partir de su incidencia, impleméntalo y revísalo |
| [4. Guiar a Copilot con instrucciones personalizadas][ex4] | Contexto | Actualiza las instrucciones y aplícalas al filtrado |
| [5. Personalizar y usar una habilidad quality-checks][ex5] | Comprobaciones repetibles | Actualiza el formato del informe y ejecuta la habilidad |
| [6. Validar la funcionalidad con Playwright MCP][ex6] | Navegador | Configura MCP y explora el filtrado |
| [7. Crear y usar un agente de control de calidad][ex7] | Requisitos y cobertura | Revisa requisitos, pruebas y evidencias |
| [8. Crear y combinar la PR de funcionalidad][ex8] | Revisión y combinación | Revisa el cambio completo y usa Agent Merge |
| [9. Comandos de barra de GitHub Copilot CLI][ex9] | Funciones de CLI | Explora contexto, modelos, uso compartido y delegación opcional |
| [10. Repaso y próximos pasos][ex10] | Resumen | Repasa el flujo, las personalizaciones y otros recursos |
| [Opcional: incorpora Foundry][foundry] | Agentes hospedados | Prepara un modelo, crea y despliega el concierge y conéctalo al sitio web en tres módulos |

## Requisitos previos

Antes de asistir a este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo de **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Permiso para crear un repositorio y un codespace
- [ ] Conocimientos básicos del terminal o la línea de comandos

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis a través de [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que utiliza este taller, así que puedes completar con él todos los recorridos.

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Si usas Copilot Business o Copilot Enterprise, asegúrate de que tu administrador haya habilitado Copilot CLI.

## Primeros pasos

**[Empieza con el ejercicio 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[foundry]: 8-foundry-agent/
[ex10]: 10-review/
