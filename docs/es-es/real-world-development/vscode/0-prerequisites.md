---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de empezar los ejercicios de VS Code, prepara el entorno. Crearás una copia del repositorio Tailspin Toys, iniciarás un [codespace][codespaces] y confirmarás que GitHub Copilot Chat funciona en el editor.

## Configurar el repositorio del taller

Usa la plantilla de Tailspin Toys para crear tu copia del repositorio.

1. Abre una ventana nueva del navegador y visita la [plantilla de Tailspin Toys][tailspin-template].
2. Selecciona **Use this template** y, después, **Create a new repository**.

    ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si participas en un taller dirigido por GitHub o Microsoft, sigue las instrucciones de los mentores. En caso contrario, crea el repositorio en una organización donde tengas acceso a GitHub Copilot.

    ![Configuración del repositorio de plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio con el formato **organization-or-user-name/repository-name**.

> [!NOTE]
> **La lista de trabajo está preparada**
>
> Al crear el repositorio desde la plantilla, también se crea una lista de incidencias de GitHub. Trabajarás con ellas durante el taller; no tienes que crear ninguna.

## Crear un codespace

Usarás un codespace para completar los ejercicios. [GitHub Codespaces][codespaces] es un entorno de desarrollo en la nube que permite escribir, ejecutar y depurar código desde el navegador.

1. Abre el repositorio que acabas de crear.
2. Selecciona el botón verde **Code**.

    ![Botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y, después, el botón **+** para crear un codespace.

    ![Crear un codespace](../../../_images/ex0-create-codespace.png)

La creación puede tardar varios minutos. Deja el codespace abierto en una pestaña del navegador.

> [!NOTE]
> También puedes ejecutar el taller en un contenedor de desarrollo local. Abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se te solicite.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Usar GitHub Copilot Chat y el modo de agente

Para usar el modo de agente de GitHub Copilot Chat, necesitas la extensión GitHub Copilot Chat. Debería estar instalada si utilizas un codespace.

> [!TIP]
> Si no tienes la extensión, [instálala desde Visual Studio Code Marketplace][copilot-chat-extension] o abre la vista **Extensions**, busca **GitHub Copilot Chat** y selecciona **Install**.

Después de instalarla, puede que tengas que iniciar sesión con tu cuenta de GitHub.

1. Vuelve al codespace.
2. Si Copilot Chat no aparece a la derecha del editor, selecciona el icono **Copilot Chat** en la parte superior del codespace.
3. Escribe `Hello world` en Copilot Chat y pulsa <kbd>Enter</kbd>.
4. Si se te solicita, sigue las instrucciones para iniciar sesión en tu cuenta de GitHub.

    ![Ejemplo de solicitud de autenticación de Copilot Chat](../../../_images/ex1-copilot-authentication.png)

5. Después de autenticarte, confirma que aparece la ventana de Copilot Chat.

## Resumen

Has creado una copia del repositorio, iniciado la creación de un codespace y comprobado que Copilot Chat está disponible.

## Siguiente paso

A continuación, [añadirás instrucciones personalizadas para Copilot][next-lesson].

## Recursos

- [Información general sobre GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
