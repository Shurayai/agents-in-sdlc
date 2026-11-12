---
title: "Ejercicio 2 - Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Muchas organizaciones tienen deuda técnica: problemas de seguridad sin resolver, código heredado que necesita actualizarse o solicitudes de funcionalidad que llevan tiempo en la lista de trabajo. El agente en la nube de GitHub Copilot puede actualizar código y añadir funcionalidades de forma autónoma. Al terminar, crea una solicitud de incorporación de cambios (PR) en borrador para que la revise un desarrollador. Así, los desarrolladores pueden delegar tareas y centrarse en trabajo de mayor alcance.

En este ejercicio explorarás cómo el agente en la nube:

- personaliza su entorno para generar código;
- realiza operaciones de forma segura;
- trabaja con incidencias bien delimitadas;
- recibe incidencias asignadas.

## Escenarios

Tailspin Toys quiere mejorar la documentación del código. Como primer paso, el equipo quiere añadir comentarios de documentación de TypeScript (TSDoc) a las funciones exportadas.

Además, el equipo de diseño quiere mejorar el descubrimiento de juegos. Quiere mostrar juegos relacionados —otros títulos de la misma categoría— en la página de detalles. Por ahora necesita una implementación sencilla para probar la experiencia. Este trabajo puede posponerse porque hay otras incidencias con mayor prioridad.

Son tareas que el agente en la nube puede realizar de forma asíncrona, mientras los desarrolladores se centran en otro trabajo y vuelven después a revisar el resultado.

## Acerca del agente en la nube de GitHub Copilot

El [agente en la nube de GitHub Copilot][copilot-agents] puede trabajar en segundo plano de forma parecida a un desarrollador. Puedes, por ejemplo, [asignarle una incidencia de GitHub][assign-issue]. Después, Copilot crea una PR en borrador para registrar el progreso, configura el entorno y empieza a trabajar. Puedes consultar la sesión mientras está activa o cuando haya terminado. Cuando la solución esté lista para revisión, Copilot te mencionará en la PR.

## La importancia de delimitar bien el trabajo

GitHub Copilot no elimina la necesidad de pensar en la tarea. Incluso una solicitud sencilla puede tener aspectos complejos, así que [delimita con cuidado el trabajo del agente en la nube][cloud-agent-best-practices]. Trátalo como a un compañero de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque.

## Instrucciones personalizadas del repositorio

Antes de asignar trabajo, revisa las instrucciones incluidas en el repositorio para reconocer su influencia en los resultados.

1. Abre `.github/copilot-instructions.md` en la interfaz web de GitHub o en un codespace.
2. Revisa **Code standards**, en especial las convenciones de TypeScript y los comentarios TSDoc.
3. Abre `.github/instructions/unit-tests.instructions.md` y observa que el frontmatter `applyTo` aplica estas instrucciones a los archivos `**/*.test.ts`.
4. Cuando asignes la incidencia `Code lacks documentation`, fíjate en los comentarios TSDoc, las convenciones de TypeScript y los encabezados de archivo de la PR. Se derivan de estos archivos de instrucciones.

## Configurar el entorno del agente en la nube

El agente en la nube usa [GitHub Actions][github-actions] para preparar el entorno. Puedes personalizarlo mediante el flujo de trabajo de configuración `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece. El proyecto ya incluye este flujo para instalar Node.js y las dependencias, los navegadores de las pruebas de extremo a extremo y la base de datos SQLite migrada y precargada de la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Configura los permisos mínimos necesarios para *tus pasos*. Copilot recibirá su propio token para sus operaciones.
    permissions:
      # Si quieres clonar el repositorio como parte de la configuración (por ejemplo, para instalar dependencias), necesitarás el permiso `contents: read`. Si no lo clonas en estos pasos, Copilot lo hará automáticamente cuando terminen.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración de la interfaz y la aplicación: Node.js (toda la aplicación usa Astro y Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y carga la base de datos SQLite local para que la compilación y las pruebas dispongan de datos.
      - name: Set up the database
        run: npm run db:setup
```

El flujo tiene dos aspectos importantes:

- Contiene un único trabajo llamado `copilot-setup-steps`, que GitHub Actions ejecuta antes de que Copilot empiece a trabajar en la PR.
- El desencadenador `workflow_dispatch` permite ejecutar el flujo manualmente desde la pestaña **Actions** para comprobarlo sin esperar a que Copilot lo inicie.

## Asignar una incidencia para añadir documentación

Crear documentación es una buena tarea para delegar. Abrirás una incidencia para añadir comentarios TSDoc y la asignarás al agente en la nube.

1. En una pestaña nueva del navegador, abre el repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** y, después, **Blank issue**.
4. Escribe `Code lacks documentation` en el campo **Title**.
5. Escribe lo siguiente en **Description**:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

6. Selecciona **Create** para crear la incidencia.
7. En el panel de la derecha, selecciona **Assign to Copilot** para abrir el diálogo de asignación.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

8. Selecciona **Assign**.
9. Abre la pestaña **Pull Requests** y selecciona la nueva PR, cuyo título será similar a `[WIP]: Code lacks documentation`. Si aún no aparece, espera un momento y actualiza la página.
10. Espera a que Copilot cree una lista de tareas.

> [!NOTE]
> La lista puede tardar varios minutos. Copilot prepara el entorno mediante el flujo de trabajo, analiza el proyecto y determina cómo abordar la tarea.

11. Revisa la lista y las tareas previstas.
12. Desplázate por la cronología de la PR hasta ver que Copilot ha empezado a trabajar en la incidencia.
13. Selecciona **View session**.

   ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la página para ver el indicador actualizado.

14. Recorre la sesión en curso. Verás cómo Copilot explora el código, analiza la situación, decide un plan y crea código.

El trabajo puede tardar varios minutos. Mientras el agente trabaja de forma asíncrona en la documentación, asignarás otra tarea y podrás centrarte en añadir funcionalidades.

## Asignar una sección de juegos relacionados

El agente en la nube permite dividir el trabajo: mientras él implementa una tarea, puedes ocuparte de otra. Ahora asignarás una sección de juegos relacionados.

1. Vuelve al repositorio en github.com.
2. Selecciona la pestaña **Issues** y, después, **New issue**.
3. Selecciona **Blank issue**.
4. Escribe `Show related games on the game details page` en **Title**.
5. Escribe lo siguiente en **Description**:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

6. Selecciona **Create** para crear la incidencia.
7. En el panel de la derecha, selecciona **Assign to Copilot** y, en el diálogo, selecciona **Assign**.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

Poco después, verás el emoji 👀 en el primer comentario de la incidencia para indicar que Copilot está trabajando.

![Copilot usa el emoji de ojos para indicar que está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

Copilot trabajará en esta segunda solicitud en segundo plano. No hace falta supervisar activamente al agente; podrás revisar el resultado cuando termine. Mientras tanto, puedes crear y usar agentes personalizados.

## Resumen y siguientes pasos

En este ejercicio, has:

- explorado cómo se personaliza el entorno del agente para generar código;
- revisado cómo se realizan las operaciones de forma segura;
- examinado la importancia de delimitar bien las incidencias;
- asignado incidencias al agente en la nube de Copilot.

El [agente en la nube de GitHub Copilot][copilot-agents] permite asignar incidencias para que Copilot trabaje de forma asíncrona. Puede ayudar con deuda técnica, funcionalidades nuevas o migraciones entre frameworks.

Mientras el agente en la nube trabaja, puedes [crear y usar agentes personalizados][next-lesson]. El agente en la nube también puede usar [servidores MCP][cloud-agent-mcp] y las instrucciones personalizadas que exploraste en ejercicios anteriores.

## Recursos

- [Acerca del agente de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
