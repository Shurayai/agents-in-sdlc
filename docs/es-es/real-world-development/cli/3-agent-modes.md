---
title: "Lección 3 - Modos de agente: Plan y Autopilot"
description: "Define un enfoque con Plan, implementa el filtrado desde una incidencia con Autopilot y revisa el resultado en modo Interactive."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Los cambios más grandes requieren un proceso más completo. En las siguientes lecciones seguirás un flujo habitual de desarrollo con agentes: partirás de una incidencia, planificarás e implementarás una funcionalidad, comprobarás el código y confirmarás su comportamiento antes de combinarlo.

En esta lección, vas a:

- iniciar una conversación de Copilot desde una incidencia de GitHub;
- definir los requisitos en modo Plan;
- implementar la funcionalidad en modo Autopilot;
- revisar el código y probar la funcionalidad manualmente en el navegador.

Usarás la misma conversación y rama para continuar con las instrucciones del repositorio, la habilidad `quality-checks`, la validación con MCP, el agente de control de calidad y la PR de funcionalidad.

## Escenario

El catálogo de Tailspin Toys crece y los visitantes necesitan filtrar los juegos por categoría y editorial. La incidencia describe la funcionalidad, pero algunos detalles, como la combinación de filtros, requieren una decisión antes de empezar a programar. Usa Plan para definir el enfoque y después autoriza una implementación delimitada con Autopilot.

## Contexto

La introducción de agentes de programación con IA no cambia los fundamentos del desarrollo. Un flujo habitual consiste en:

1. Partir de una incidencia que describa el trabajo.
2. Planificar qué se debe implementar.
3. Crear y revisar el código.
4. Ejecutar pruebas para validar el código.
5. Comprobar manualmente la funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Combinar el código cuando se haya revisado y se completen correctamente las comprobaciones de integración continua.

> [!NOTE]
> Los detalles varían según el equipo y la organización, pero la mayoría de los flujos siguen un proceso parecido.

Seguir este enfoque ayuda a comprobar que el código generado por IA cumple los requisitos y pasa por las mismas revisiones que el código escrito manualmente.

## Modos de conversación

El modo de conversación determina cuánta autonomía tiene el agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar de modo.

- **Interactive**: trabajas con el agente y este espera tu intervención antes de continuar.
- **Plan**: el agente prepara un plan y no puede editar los archivos del proyecto.
- **Autopilot**: el agente escribe código, ejecuta pruebas e itera de forma autónoma hasta completar la tarea.

Empieza en Plan, revisa el plan y, después, usa Autopilot para implementarlo.

## Partir de la incidencia

Prepara el Codespace y crea una rama para el trabajo de filtrado.

1. Vuelve al Codespace y, si está detenido, reinícialo.
2. Confirma que la PR de valoraciones por estrellas se ha combinado.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Usa las flechas para seleccionar **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia al prompt y volver a la pestaña **Session**.

## Planificar el filtrado

En modo Plan, Copilot explorará el proyecto y propondrá un enfoque antes de modificar archivos.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> hasta que el indicador muestre **Plan**.
2. Después de la referencia a la incidencia, introduce:

   ```plaintext
   Create a plan for implementing this feature.
   ```

3. Responde a las preguntas sobre el comportamiento de los filtros según las decisiones que quieras tomar.
4. Cuando el plan esté listo, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para ampliarlo y revisarlo.
5. Pide que modifique cualquier parte que no refleje tus decisiones.

## Aprobar Autopilot

Después de revisar el plan, permite que Copilot lo implemente.

1. Selecciona **Accept plan and build on autopilot (recommended)** o la opción equivalente de tu versión.
2. Confirma que el indicador muestra **Autopilot**.
3. Observa cómo Copilot implementa el plan y ejecuta pruebas.

> [!NOTE]
> Al aprobar el plan, la implementación puede empezar de inmediato. Revísalo antes de aprobarlo. Si Copilot indica que faltan dependencias o que hay un conflicto de puerto, resuelve el problema antes de considerar completas las comprobaciones.

## Revisar y comprobar la implementación

Revisa el código generado y los resultados de las comprobaciones antes de probar la funcionalidad.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar a **Interactive**.
2. Ejecuta `/diff` e inspecciona la implementación del filtrado y las pruebas.
3. Compara el resultado con la incidencia y las decisiones del plan.
4. Pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.
5. Revisa las comprobaciones del proyecto y pide a Copilot que resuelva los errores.

## Probar la funcionalidad

Inicia la aplicación y usa el puerto reenviado de Codespaces para probar las combinaciones de filtros acordadas.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba los filtros por categoría y editorial, así como las combinaciones del plan.
4. Comprueba que el restablecimiento y el estado sin resultados coinciden con la incidencia y tus decisiones.
5. Vuelve al Codespace y pide a Copilot que detenga el servidor.

## Resumen y siguientes pasos

En esta lección, has:

- iniciado una conversación de Copilot desde una incidencia de GitHub;
- definido los requisitos en modo Plan;
- implementado la funcionalidad con Autopilot;
- revisado el código y comprobado manualmente la funcionalidad en un navegador reenviado.

A continuación, [guiarás a Copilot con instrucciones personalizadas][next-lesson].

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[next-lesson]: ../4-custom-instructions/
