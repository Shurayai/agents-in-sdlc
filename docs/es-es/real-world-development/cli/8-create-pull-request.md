---
title: "Lección 8 - Crear y combinar la solicitud de incorporación de cambios de funcionalidad"
description: "Revisa el filtrado, las instrucciones, la habilidad, el perfil de control de calidad y las pruebas; después crea la solicitud de incorporación de cambios (PR) y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las actualizaciones de instrucciones y de la habilidad, el perfil de control de calidad y las pruebas están en una sola rama. Revisarás los cambios en conjunto y abrirás una solicitud de incorporación de cambios. Esta vez, Agent Merge gestionará el proceso de combinación.

En esta lección, vas a:

- conocer Agent Merge y cómo automatiza el ciclo de vida de una solicitud de incorporación de cambios (PR);
- revisar el cambio completo y las pruebas de verificación;
- crear la solicitud de incorporación de cambios (PR) de filtrado;
- activar Agent Merge solo después de la revisión y confirmar que la PR se ha combinado.

## Escenario

Durante el flujo de filtrado, has usado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere automatizar el trabajo restante de la PR sin quitar al desarrollador el control para autorizar la combinación.

> [!NOTE]
> En un proyecto habitual, dividirías la funcionalidad, las instrucciones, la habilidad y el agente de control de calidad en varias PR. En este taller, se agrupan en una sola conversación y rama para centrarse en el flujo.

## Acerca de Agent Merge

**Agent Merge** automatiza el trabajo que falta para combinar una PR. Copilot aborda los bloqueos, como las comprobaciones de integración continua (CI) que fallan, los comentarios de revisión y las actualizaciones de la rama; después, activa la combinación automática de GitHub si la configuración del repositorio lo permite.

Revisa el trabajo y confirma que está listo antes de activar Agent Merge.

## Usar Agent Merge para gestionar la PR

Revisa el código, crea la PR y autoriza a Agent Merge a gestionar el proceso restante.

1. Vuelve al Codespace.
2. Ejecuta `/agent` para abrir el diálogo de agentes.
3. Selecciona **Default** y pulsa <kbd>Enter</kbd>.
4. Crea una PR con `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará las comprobaciones de CI de la PR y la combinará cuando se completen correctamente.
7. Confirma que Copilot informa de que la PR se ha combinado correctamente.

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si se bloquea, revisa el motivo y completa manualmente la combinación revisada cuando el repositorio lo permita.

## Resumen y siguientes pasos

En esta lección, has:

- aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una solicitud de incorporación de cambios;
- revisado el cambio completo y las pruebas de verificación;
- creado la PR de filtrado;
- activado Agent Merge después de la revisión y confirmado que la PR se ha combinado.

A continuación, [explorarás otros comandos de barra de Copilot CLI][next-lesson].

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
