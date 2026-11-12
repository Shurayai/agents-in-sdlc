---
title: "Lección 2 - Añadir valoraciones por estrellas: una mejora rápida"
description: "Inicia tu primera sesión de agente en la aplicación GitHub Copilot, realiza un pequeño cambio en las tarjetas de los juegos e intégralo como tu primera solicitud de cambios."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Después de recorrer el espacio de trabajo y usar un chat rápido, es hora de iniciar una **sesión de agente** y realizar el primer cambio en el proyecto. Será un cambio pequeño: los juegos ya incluyen una valoración por estrellas en sus datos, pero las tarjetas de la página de inicio todavía no la muestran. Pedirás al agente que la muestre, revisarás el cambio y lo integrarás como tu primera solicitud de cambios.

En esta lección aprenderás a:

- iniciar una sesión de agente y conocer su estructura.
- pedir al agente que realice un cambio pequeño y acotado en el proyecto.
- revisar el cambio en la vista de diferencias del espacio de trabajo.
- ejecutar la aplicación en local para comprobar el cambio en el navegador.
- abrir e integrar tu primera solicitud de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración por estrellas, que ya aparece en la página de detalles. Sin embargo, las tarjetas de la página de inicio solo muestran el título, la categoría, la editorial y la descripción. Como ejercicio inicial, pedirás al agente que muestre en cada tarjeta la valoración existente. Es un cambio pequeño y autocontenido, perfecto para tu primera sesión.

## Anatomía de una sesión

Una **sesión** es una conversación con un agente que se ejecuta en su propio espacio de trabajo aislado. Cada sesión recibe un **árbol de trabajo y una rama de Git dedicados**, lo que permite ejecutar varias sesiones a la vez —una para añadir una funcionalidad y otra para corregir un error, por ejemplo— sin que sus cambios entren en conflicto. Las sesiones aparecen en la barra lateral, agrupadas por repositorio; selecciona una para cambiar a ella.

Dentro de una sesión verás tres elementos: la **conversación** con el agente, la **actividad de las herramientas** mientras el agente explora y edita archivos, y la lista de **archivos modificados** con sus diferencias.

## Iniciar una sesión y pedir el cambio

Inicia una sesión nueva para explorar el proyecto e implementar la funcionalidad. Durante la [configuración de la aplicación][prior-lesson], añadiste el proyecto desde su repositorio de GitHub. Ahora crearás una sesión para ese repositorio y pedirás el cambio.

1. Vuelve a la aplicación GitHub Copilot o ábrela.
2. Selecciona **+** en la parte superior de la barra lateral para iniciar una sesión.
3. Selecciona `tailspin-toys` como repositorio.
4. Elige un **new working tree** y el modo **Interactive** debajo del cuadro de indicaciones. Usa el siguiente prompt para pedir el cambio:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

5. Pulsa <kbd>Enter</kbd> para enviar el prompt a Copilot.

La aplicación Copilot empieza por crear un árbol de trabajo nuevo, una copia aislada del proyecto. Después, explora el proyecto, localiza los archivos que debe actualizar para añadir la funcionalidad y crea el código necesario. Ya has añadido una funcionalidad con la aplicación Copilot.

## Revisar las diferencias

Revisa todos los cambios generados por IA antes de integrarlos, incluso los más pequeños. Examina los cambios directamente en la aplicación Copilot.

1. En la esquina superior derecha de la aplicación, selecciona **Toggle review panel**. En el panel que se abre, selecciona **Changes** para ver los archivos modificados y sus diferencias.

   ![Barra de herramientas superior de la aplicación GitHub Copilot con una flecha que señala el botón Toggle review panel, a la derecha de Create PR](../../../_images/app-2-review-panel.png)

2. Comprueba que se ha añadido código a `GameCard.astro`, el archivo principal que se utiliza para mostrar los detalles de los juegos. Debería parecerse al siguiente bloque: muestra la valoración cuando existe y, si `starRating` es `null`, muestra «No rating yet».

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Como Copilot, al igual que todas las herramientas de IA generativa, es probabilístico y no determinista, el código exacto puede variar respecto al ejemplo. No obstante, debería ser parecido.

## Comprobar los cambios

Antes de abrir el navegador, revisa los resultados automatizados del agente. Esta comprobación confirma que las pruebas cubren la valoración y su alternativa cuando no hay datos, y que no se han omitido pasos necesarios.

1. Revisa los resultados de las comprobaciones automatizadas del agente.
2. Confirma que las pruebas cubren tanto un valor numérico de `starRating` como el caso alternativo `null`.
3. Si falta un requisito previo o se ha omitido una comprobación, no la des por superada; revisa cualquier solicitud de instalación antes de aprobarla.

Leer el código no basta para confirmar que funciona; la comprobación visual en el navegador permite verificar la interfaz actualizada.

> [!TIP]
> Un lienzo es un widget interactivo disponible dentro de la aplicación Copilot. Más adelante explorarás lienzos personalizados e incluso crearás uno, pero por ahora usarás el lienzo de navegador integrado.

1. Usa el siguiente prompt para pedir a Copilot que inicie la aplicación y abra la página en el lienzo del navegador:

   ```plaintext
   Start the app and open it in the browser canvas.
   ```

2. Espera a que se inicie la aplicación y se abra una ventana del navegador dentro de la aplicación Copilot.
3. Confirma que las tarjetas de juegos con valoración muestran su valor sobre cinco.
4. Cuando termines, pide a Copilot que detenga el servidor de desarrollo que ha iniciado para esta sesión:

   ```plaintext
   Stop the dev server and close the browser canvas.
   ```

## Abrir e integrar tu primera solicitud de cambios

Una solicitud de cambios (PR) permite revisar el cambio antes de integrarlo en el código base existente.

1. Selecciona **Create PR** en la esquina superior derecha.
2. Si se te solicita, selecciona **Sign in with your browser** y sigue las indicaciones para autenticarte.
3. Si Copilot explica que la directiva del repositorio requiere una incidencia relacionada antes de crear la PR, confirma que debe seguir ese proceso.
4. Espera a que Copilot cree la PR.
5. Selecciona la burbuja **PR**, situada justo encima del chat, para abrir la solicitud en el panel de revisión. Revísala allí si es necesario.
6. Cuando esté todo listo, selecciona **Ready to merge**.
7. En el nuevo cuadro de diálogo, selecciona **Merge pull request** para integrar la solicitud.

## Resumen y siguientes pasos

¡Enhorabuena! Has publicado tu primer cambio con la aplicación GitHub Copilot. En concreto, has:

- iniciado una sesión de agente y conocido su estructura.
- dirigido al agente para que realice un cambio pequeño y acotado en las tarjetas de los juegos.
- revisado el cambio en la vista de diferencias del espacio de trabajo.
- ejecutado la aplicación en local para confirmar la valoración por estrellas en el navegador.
- abierto la PR 1, revisado sus comprobaciones e integrado explícitamente el cambio.

A continuación, [partirás de la incidencia de filtrado y utilizarás los modos Plan y Autopilot][next-lesson] para desarrollar una funcionalidad más amplia.

## Recursos

- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Gestionar incidencias y solicitudes de cambios con la aplicación GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instalar-y-configurar-la-aplicación-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
