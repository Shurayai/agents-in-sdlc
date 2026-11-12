---
title: "Ejercicio 5 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

En el modo de agente, GitHub Copilot explora el proyecto, propone cambios, edita archivos y ejecuta comandos. Copilot Chat en VS Code muestra en tiempo real las llamadas a herramientas y las ediciones. Puedes revisar las diferencias, aceptar o rechazar cambios y dirigir la conversación con prompts de seguimiento.

En este ejercicio, vas a:

- supervisar en tiempo real el trabajo del agente de accesibilidad;
- revisar y aceptar las ediciones de archivos propuestas;
- pedir al agente que añada un modo claro además del modo de alto contraste.

## Escenario

El agente personalizado de accesibilidad del [Ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño solicita además un modo claro. En lugar de empezar una conversación nueva, ampliarás el trabajo en la sesión existente.

## Supervisar el progreso de Copilot

La vista Copilot Chat muestra los archivos que explora el agente, los comandos que ejecuta y las ediciones que propone. Cada edición aparece en el chat con las diferencias y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del Ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para ver las llamadas a herramientas, las lecturas y ediciones de archivos y los comandos de terminal.
3. Cuando proponga una edición, revisa las diferencias:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para revertirlo y permitir que el agente lo intente de nuevo.
4. Abre el indicador **Files changed** de la parte superior del chat para revisar el conjunto completo de archivos modificados.

> [!NOTE]
> Si una llamada a una herramienta solicita permiso (por ejemplo, para ejecutar un comando de terminal), el agente se detendrá y mostrará **Allow**. Aprueba solo los comandos que te parezcan adecuados.

5. Espera a que el agente termine de implementar el modo de alto contraste. Verás un mensaje final con un resumen de los cambios.

## Pedir al agente que añada el modo claro

Añade el modo claro en la misma conversación para que el agente conserve el contexto de los componentes, los estilos y el uso de almacenamiento local.

1. Envía este prompt en la entrada de Copilot Chat:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. Revisa cómo el agente examina los cambios existentes y propone añadir el modo claro.
3. Revisa cada cambio nuevo y usa **Keep** o **Undo** según corresponda.
4. Si el agente toma un rumbo que no quieres —por ejemplo, refactoriza los controles de una forma que no te convence—, detenlo con **Stop** junto a la entrada del chat y envía una aclaración.

> [!TIP]
> Dirigir una sesión en curso es más rápido que empezar de nuevo. Usa prompts de seguimiento para ajustar el enfoque, por ejemplo, simplificar el CSS con variables, integrar el modo claro en el panel existente o añadir atajos de teclado.

## Revisar el conjunto de cambios

Antes de confirmar el trabajo, revisa todo lo que ha modificado el agente.

1. Abre la vista **Source Control** en VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver componentes Astro, estilos y posiblemente pruebas relacionadas.
3. Abre algunos archivos y revisa las diferencias. Confirma que se respetan los patrones de accesibilidad del agente: atributos de Accessible Rich Internet Applications (ARIA), navegación con teclado, HTML semántico y persistencia mediante almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios desde **Source Control**. Publicarás el trabajo en la [siguiente lección][next-lesson].

## Resumen y siguientes pasos

En este ejercicio, has:

- supervisado en tiempo real el trabajo del agente de accesibilidad;
- revisado y aceptado las ediciones de archivos propuestas;
- dirigido al agente en la misma sesión para añadir el modo claro junto al modo de alto contraste.

A continuación, [publicarás el trabajo de accesibilidad como una solicitud de incorporación de cambios][next-lesson] y revisarás los cambios del agente local.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Usar el modo de agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
