---
title: "Lección 9 - Comandos de barra de GitHub Copilot CLI"
description: "Explora comandos para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar tareas opcionalmente."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

GitHub Copilot CLI incluye comandos de barra para acceder a funciones avanzadas y opciones de configuración. Ya has usado `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. En esta lección explorarás otros comandos útiles.

En esta lección, vas a:

- usar `/context` y `/compact` para explorar cómo gestiona Copilot el contexto;
- usar `/model` para ver los modelos disponibles;
- aprender a exportar o compartir una sesión con `/share`;
- explorar comandos opcionales para trabajar en paralelo, usar worktrees y delegar tareas al agente en la nube.

## Escenario

El flujo principal de CLI ha terminado. Ahora explorarás la gestión del contexto, el cambio de modelo, el uso compartido de sesiones y la delegación opcional al [agente en la nube de Copilot][about-cloud-agent].

## Explorar el contexto de Copilot CLI

Copilot CLI compacta automáticamente la conversación cuando se acerca al límite de contexto. Puedes consultar el uso y compactarla manualmente.

1. Vuelve al Codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Ejecuta:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y la distribución del contexto.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Ejecuta `/context` otra vez y compara el resultado. Si la conversación ya es pequeña, puede que el cambio no sea importante.

> [!NOTE]
> Copilot CLI compacta el contexto automáticamente a medida que se llena la ventana. Usa `/compact` para elegir cuándo hacerlo. Usa `/clear` o `/new` si vas a cambiar a una tarea no relacionada y quieres iniciar otra conversación.

## Elegir un modelo

Los modelos tienen distintas capacidades. Copilot CLI permite consultar y seleccionar el que quieras usar.

1. Ejecuta:

   ```plaintext
   /model
   ```

2. Explora los modelos y la información de uso disponible.
3. Conserva el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Compartir una sesión

El comando `/share` puede exportar una sesión a un archivo Markdown o HTML, crear un enlace para compartir o publicar un gist de GitHub.

1. Ejecuta `/help` y revisa las opciones de `/share` disponibles en tu versión.
2. Si quieres compartir la sesión, elige un destino adecuado, como `/share file` para exportar un archivo Markdown local.
3. Revisa el contenido antes de enviarlo o publicarlo. Las exportaciones pueden incluir prompts, respuestas y detalles del proyecto.

Publicar un enlace o un gist es opcional. No compartas contenido del repositorio o de una conversación que el equipo no tenga previsto divulgar.

## Opcional: ampliar el trabajo o delegarlo

Copilot CLI también ofrece comandos para tareas más grandes:

- `/fleet` puede dividir tareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un worktree de Git aislado para otra tarea.
- `/delegate` puede enviar una tarea al agente en la nube de Copilot, que trabaja de forma asíncrona y puede abrir una solicitud de incorporación de cambios (PR).

Estos comandos son opcionales, ya que pueden crear worktrees o trabajo remoto. Empieza con una tarea nueva y bien delimitada, y revisa el resultado con el flujo habitual. Para profundizar en el trabajo asíncrono, continúa con el [taller del agente en la nube][cloud-workshop].

## Resumen y siguientes pasos

En esta lección, has:

- usado `/context` y `/compact` para explorar cómo gestiona Copilot el contexto;
- usado `/model` para explorar los modelos disponibles;
- aprendido a exportar o compartir una sesión con `/share`;
- explorado comandos opcionales para trabajar en paralelo, usar worktrees y delegar tareas al agente en la nube.

A continuación, [repasarás el flujo y los próximos pasos][next-lesson].

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca del agente en la nube de Copilot][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
