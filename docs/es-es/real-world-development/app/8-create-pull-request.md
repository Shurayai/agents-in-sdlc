---
title: "Lección 8 - Crear e integrar la solicitud de cambios de la funcionalidad"
description: "Revisa conjuntamente el filtrado, las instrucciones, la actualización de la habilidad, el perfil de control de calidad y las pruebas; después, crea una solicitud de cambios (PR) y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La implementación del filtrado, las actualizaciones de instrucciones y de la habilidad, el perfil de control de calidad (QA) y las pruebas están guardados en una sola rama. Es hora de revisarlos juntos y abrir una solicitud de cambios. Ya integraste personalmente la solicitud de cambios (PR) de valoración por estrellas; esta vez permitirás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Normalmente separaríamos la funcionalidad, las actualizaciones de instrucciones y de la habilidad y el agente de control de calidad en varias PR. Para agilizar el taller, has mantenido todo el flujo de filtrado y calidad en una sesión y una rama, y todo ese trabajo se incluirá en esta PR.

En esta lección aprenderás a:

- descubrir qué es Agent Merge y cómo automatiza el ciclo de vida de la integración.
- examinar la PR completa de la funcionalidad y las pruebas de verificación.
- autorizar Agent Merge solo después de la revisión y confirmar que la PR está integrada.

## Escenario

A lo largo del flujo de filtrado, has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Ahora Tailspin Toys quiere automatizar el trabajo restante de la PR y mantener la autorización para integrar bajo el control del desarrollador.

## Introducción a Agent Merge

**Agent Merge** automatiza el trabajo restante necesario para integrar una solicitud de cambios en la aplicación GitHub Copilot. Al habilitarlo, la sesión de la aplicación lee la solicitud y resuelve los bloqueos: corrige las comprobaciones fallidas de integración continua (CI), responde a comentarios de revisión y realiza un rebase cuando es necesario. Después, integra la solicitud en cuanto GitHub lo permite. Se ejecuta en segundo plano, sigue funcionando tras reiniciar la aplicación y se desactiva cuando la solicitud queda integrada.

Hasta ahora has seleccionado **Merge pull request** personalmente. Agent Merge puede asumir esa responsabilidad, pero su capacidad para editar código e integrar la solicitud sigue necesitando tu autorización explícita. Revisa las acciones que tiene permitidas y el trabajo realizado antes de concederle permiso para integrar.

## Usar Agent Merge para gestionar la PR

Ahora configurarás Agent Merge para que gestione la PR en lugar de realizar manualmente el trabajo restante.

1. Usa el selector de agentes para seleccionar **Default agent**.
2. Selecciona el menú desplegable junto a **Create PR**.
3. Selecciona **Agent Merge**. El botón cambia a **Agent Merge**.
4. Selecciona el botón **Agent Merge** para iniciar el proceso. Elegir la opción del menú desplegable por sí sola no lo inicia.

Se iniciará el proceso de Agent Merge, que hará lo siguiente:

- Crear la solicitud de cambios con un título y una descripción.
- Si iniciaste la sesión desde una incidencia, incluir una referencia a ella en el cuerpo de la descripción.
- Realizar un rebase o gestionar posibles conflictos de integración con la rama de destino.
- Supervisar el proceso de CI para asegurarse de que se superen todas las comprobaciones.
- Supervisar la PR para detectar comentarios de otros desarrolladores o de la revisión de código de Copilot y hacer cambios para resolverlos.
- Opcionalmente, integrar la PR automáticamente cuando todo se haya completado correctamente.

Después de que el agente prepare la PR, revisarás los cambios y autorizarás explícitamente la integración.

5. Revisa los cambios de la PR y las evidencias de verificación antes de conceder permiso para integrar.
6. Selecciona el menú desplegable junto a **Agent Merge**.
7. Comprueba que **Merge pull request** está marcado.
8. Pide explícitamente al agente que integre la solicitud:

   ```plaintext
   Merge the PR once all required checks and approvals pass. Do not bypass repository protections.
   ```

9. Sigue el progreso y resuelve los bloqueos que se indiquen. Antes de continuar, confirma que el estado de la PR es **Merged**; tener habilitado el permiso de integración o un agente en ejecución no confirma que la integración haya terminado.

> [!IMPORTANT]
> Agent Merge no elude las protecciones del repositorio ni los permisos que falten. Resuelve esos bloqueos antes de continuar.

## Resumen y siguientes pasos

Has automatizado varias partes del proceso de desarrollo: la generación de código, las pruebas y la validación del código, y ahora también el proceso de la solicitud de cambios. En esta lección has:

- aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de la integración.
- examinado la PR completa de la funcionalidad y las pruebas de verificación.
- autorizado Agent Merge solo después de la revisión y confirmado que la PR se ha integrado.

A continuación, [utilizarás un lienzo existente y crearás uno de clasificación][next-lesson] para explorar una forma más completa de examinar, planificar y visualizar el trabajo con el agente.

## Recursos

- [Gestionar incidencias y solicitudes de cambios con la aplicación GitHub Copilot][managing-issues-prs]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
