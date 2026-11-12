---
title: "Lección 10 - Repaso y próximos pasos"
description: "Repasa el flujo de Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has usado GitHub Copilot CLI en un flujo continuo de Tailspin Toys. Has preparado un Codespace e instalado Copilot CLI; añadido y combinado las valoraciones por estrellas; planificado e implementado el filtrado; actualizado las instrucciones; personalizado `quality-checks`; usado Playwright MCP; creado un agente de control de calidad; autorizado Agent Merge; y explorado comandos de barra para el contexto, los modelos, el uso compartido y la delegación opcional.

## Lo que has entregado

El taller incluye dos hitos de solicitudes de incorporación de cambios (PR), cada uno en una rama creada desde `main` actualizado:

1. **Valoraciones por estrellas:** muestra `starRating` y un estado explícito para los juegos sin valorar.
2. **Filtrado y flujo de calidad:** implementa el filtrado, actualiza y aplica las instrucciones, personaliza el informe `quality-checks`, crea un perfil de control de calidad e incluye las pruebas correspondientes.

Desde la planificación del filtrado hasta la creación de su PR, has trabajado en la misma conversación y rama para agilizar el taller.

## Diferentes formas de verificar

Has comprobado el código con pruebas automatizadas, mediante tu propia inspección en el navegador y con la exploración del navegador de Copilot a través de MCP. La habilidad `quality-checks` ejecutó las pruebas unitarias, lint y las comprobaciones de tipos, y comunicó los resultados en el nuevo formato. El agente de control de calidad reunió esa información con la revisión de los requisitos y la cobertura de pruebas antes de la PR.

Las pruebas nuevas deben cubrir carencias reales; puede ser correcto que una ejecución de control de calidad no necesite añadir pruebas. Revisa el código y las pruebas, y vuelve a comprobar cualquier evidencia afectada por cambios posteriores.

## Buenas prácticas

El contexto y las herramientas influyen en el trabajo de Copilot. En este taller actualizaste instrucciones, personalizaste una habilidad, creaste un perfil de control de calidad y configuraste un servidor MCP. Reutiliza estas personalizaciones y ajústalas a las necesidades del equipo. Las instrucciones establecen estándares, las habilidades describen tareas repetibles, los agentes personalizados definen roles especializados y los servidores MCP conectan herramientas externas. Revisa los cambios y los resultados de las herramientas, no solo el resumen del agente.

Adapta el **modo y el modelo** a la tarea. Usa **Plan** para definir un enfoque antes de construir, **Interactive** para seguir de cerca los cambios y **Autopilot** para tareas bien delimitadas. Elige un modelo más rápido para ediciones rutinarias y uno más capaz para tareas complejas.

El contexto sigue siendo importante. Explicar claramente qué quieres construir, por qué y cómo influye de forma significativa en el resultado.

## Más opciones para explorar

- `/review` para pedir al agente de revisión de código que analice los cambios.
- `/rubber-duck` para explicar un problema y obtener otra perspectiva.
- `/fleet` para coordinar tareas independientes en paralelo.
- `/worktree` para aislar otra tarea.
- `/delegate` para enviar una tarea al agente en la nube de Copilot.

## Próximos pasos

La mejor forma de mejorar con una herramienta es seguir usándola. Aplícala al código de producción, a proyectos personales o a una aplicación que tengas pendiente. Comparte lo que aprendas con el equipo y consulta la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Incorporar Foundry][foundry]. Para comparar otros entornos, explora los talleres de [VS Code][vscode], la [aplicación GitHub Copilot][app] o el [agente en la nube de Copilot][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
