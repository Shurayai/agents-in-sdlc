---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Gestionar agentes][previous-lesson] |
|:--|

## Revisar el trabajo

En este taller has pedido a GitHub Copilot que documente el código, añada juegos relacionados y mejore la accesibilidad con modos de alto contraste y claro. Revisarás los cambios y, si hace falta, pedirás ajustes antes de continuar con el flujo habitual de desarrollo.

### Escenario

Los fundamentos del diseño de software y DevOps no cambian al añadir IA generativa. Revisa el código generado y sigue el proceso habitual antes de habilitar la revisión para el resto del equipo.

## Seguridad y agente en la nube de GitHub Copilot

El agente en la nube trabaja de forma asíncrona y sin supervisión directa. Para mantener la seguridad:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que utiliza para sus cambios.
- El agente se ejecuta en GitHub Actions dentro de un entorno temporal e independiente.
- Una persona debe aprobar los flujos de trabajo de GitHub Actions antes de ejecutarlos.
- De forma predeterminada, el acceso a recursos externos está limitado, incluidos los servidores del Protocolo de contexto de modelo (MCP).

## Revisar la documentación generada

Empieza por la primera solicitud de incorporación de cambios (PR), que añade documentación al código.

> [!NOTE]
> Puede que la PR muestre un aviso de que un firewall bloquea a Copilot. Es lo esperado: el acceso del agente a recursos externos, incluidos los servidores MCP, está limitado de forma predeterminada. Si quieres, puedes [personalizar o deshabilitar el firewall del agente en la nube][agent-firewall].

1. Abre el repositorio en github.com.
2. Selecciona **Pull Requests** y abre la PR titulada, por ejemplo, **Add missing documentation**.

> [!NOTE]
> Si Copilot sigue trabajando, la PR incluirá la etiqueta **[WIP]**. Espera a que termine; puede tardar varios minutos.

3. Cuando la PR esté lista, selecciona **Files changed** y revisa los cambios.

   ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

4. Revisa los comentarios TSDoc y la documentación añadida. Busca también las convenciones de TypeScript y los encabezados de archivo de las instrucciones personalizadas que viste en el Ejercicio 2.
5. Si los cambios son correctos, vuelve a **Conversation** y desplázate hacia abajo.
6. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

   ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

7. Espera a que se ejecuten las comprobaciones en la PR. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían completarse correctamente. Puede tardar varios minutos.

## Pedir cambios a GitHub Copilot

Puedes mencionar a Copilot en comentarios de la PR o en comentarios insertados en el código para pedirle que haga cambios. Como los resultados son probabilísticos, no hay un prompt único. Por ejemplo, puedes pedirle que:

- añada encabezados breves al principio de cada archivo de código;
- añada comentarios TSDoc a archivos TypeScript y Astro;
- cree un README que describa la estructura de la aplicación Astro.

1. Añade un comentario que solicite un cambio en la documentación y menciona a **@copilot**, como harías con otra persona. Usa una de las ideas anteriores o una petición adecuada al código.
2. Selecciona **View Session** para observar cómo Copilot inicia una nueva sesión y realiza los cambios.
3. Selecciona **Back to pull request** para volver a la PR.

   ![Botón Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot termine, confirma que se ha añadido un commit a la PR.
5. Selecciona **Files changed** y revisa las modificaciones.

Puedes seguir iterando hasta que estés conforme. Después, marca la PR como lista para revisión y combínala.

![Opción para marcar la PR como lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisar la funcionalidad de juegos relacionados

Vuelve a la PR que Copilot creó para mostrar juegos relacionados en la página de detalles.

1. Abre el repositorio en GitHub.com y selecciona la pestaña **Pull Requests**.
2. Selecciona la PR titulada, por ejemplo, **Show related games on the game details page**.
3. Selecciona **Files changed** y revisa el código generado.
4. Si los cambios son correctos, vuelve a **Conversation** y desplázate hacia abajo.
5. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

   ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

6. Espera a que terminen las comprobaciones del proyecto para la aplicación Astro.
7. **Opcional:** cambia a la rama de Copilot en tu Codespace para probar manualmente la funcionalidad. Sustituye `<branch-name>` por el nombre de la rama creada por Copilot, por ejemplo, `copilot/fix-8`:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot ha implementado los juegos relacionados. Puedes pedirle cambios con otro comentario en **Conversation**; por ejemplo, ajustar cuántos juegos se muestran o añadir encabezados y comentarios TSDoc. Esta incidencia se asignó antes de actualizar las instrucciones personalizadas.

## Revisar las mejoras de accesibilidad

Por último, revisarás la PR del agente personalizado de accesibilidad. Debe incluir el modo de alto contraste solicitado en el Ejercicio 3 y el modo claro solicitado desde mission control en el Ejercicio 4.

1. Abre el repositorio en GitHub.com, selecciona **Pull Requests** y abre la PR titulada, por ejemplo, **Add high contrast mode to website**.

> [!NOTE]
> Si Copilot sigue trabajando, la PR incluirá la etiqueta **[WIP]**. Espera a que termine; puede tardar varios minutos.

2. Selecciona **Files changed** y revisa la implementación. Comprueba especialmente:
   - los controles para cambiar de modo;
   - el uso de almacenamiento local para conservar las preferencias;
   - los cambios de hojas de estilo en cascada (CSS) para los modos claro y de alto contraste;
   - los atributos de Accessible Rich Internet Applications (ARIA), la navegación con teclado y el código que controla los modos.

3. Si los cambios son correctos, vuelve a **Conversation** y desplázate hacia abajo.
4. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

   ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

5. Espera a que terminen las comprobaciones del proyecto para la aplicación Astro.
6. **Opcional:** cambia a la rama de Copilot en tu Codespace para probar las funciones de accesibilidad:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

7. Inicia la aplicación y prueba los modos de alto contraste y claro. Comprueba que las preferencias se conservan al recargar la página.

Si detectas problemas de accesibilidad, menciona a `@copilot` en un comentario y solicita los cambios necesarios.

## Ejercicio opcional: seguir delegando

El agente en la nube es útil para trabajar en tareas reales de la lista mientras tú haces otra cosa. Para practicar, crea más incidencias en el repositorio y asígnaselas a Copilot. Algunas ideas:

- crear un formulario de interés para patrocinadores en la página de detalles;
- implementar la paginación de la lista de juegos;
- añadir validación de entradas y gestión de errores a los helpers de acceso a datos.

## Resumen

Has completado el recorrido del agente en la nube. En estos ejercicios:

- **Has inspeccionado las instrucciones personalizadas del repositorio** para reconocer su influencia en los resultados.
- **Has asignado incidencias al agente en la nube de Copilot** y has visto cómo prepara el entorno y trabaja de forma asíncrona.
- **Has creado y utilizado un agente personalizado** para implementar modos de alto contraste y claro.
- **Has usado la página de agentes de Copilot como mission control** para supervisar y dirigir la sesión.
- **Has revisado e iterado sobre las PR del agente en la nube**, mencionando a `@copilot` y aprobando los flujos de trabajo.

## Repaso y próximos pasos

Has completado el recorrido del agente en la nube. Para seguir explorando, estos otros entornos complementan lo que has practicado:

- 🖥️ **[Recorrido de VS Code](../../vscode/)**: explora el modo de agente de Copilot Chat y la integración con MCP desde el IDE.
- 💻 **[Recorrido de CLI](../../cli/)**: entrega dos cambios revisados desde el terminal con Plan y Autopilot, habilidades de agente, un agente de control de calidad, Playwright MCP, Agent Merge y la opción `/delegate`.

En tu propio repositorio, prueba a asignar al agente una incidencia de refactorización o cobertura de pruebas, crear un agente personalizado para otro ámbito o configurar `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]
- [Configurar el firewall del agente en la nube][agent-firewall]

---

| [← Lección anterior: Gestionar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
