---
title: "Lección 1 - Instalar la aplicación GitHub Copilot"
description: "Instala la aplicación GitHub Copilot, conecta el repositorio que has creado a partir de la plantilla, familiarízate con el espacio de trabajo y prueba un chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La [aplicación GitHub Copilot][about-copilot-app] es una aplicación de escritorio para el desarrollo dirigido por agentes. Se basa en GitHub Copilot CLI y se integra de forma nativa con GitHub, por lo que tus repositorios, ramas y procesos de integración continua (CI) funcionan sin configuración adicional. Está diseñada para flujos de trabajo en los que diriges varios agentes de inteligencia artificial (IA) en paralelo, cada uno en su propio espacio de trabajo aislado, automatizas tareas repetitivas y no tienes que hacerlo todo por tu cuenta. Con Node.js instalado y tu copia del proyecto preparada, el siguiente paso es instalar la aplicación y conectar ese repositorio.

En esta lección aprenderás a:

- instalar la aplicación GitHub Copilot e iniciar sesión.
- añadir el proyecto a la aplicación desde su repositorio de GitHub.
- familiarizarte con el espacio de trabajo y el backlog que ha preparado la plantilla.
- probar un chat rápido para conocer mejor la aplicación.

## Escenario

Tu equipo está adoptando agentes de IA para abordar un backlog cada vez mayor. La aplicación Copilot ofrece un único lugar desde el que dirigir ese trabajo: seleccionar incidencias, ejecutar agentes, revisar cambios e integrar solicitudes de cambios. En esta lección instalarás y conectarás la aplicación, y aprenderás a iniciar una conversación sobre el proyecto.

> [!NOTE]
> Se requiere un plan de Copilot válido: Copilot Free, Copilot Student o cualquier plan de pago (Pro, Pro+, Business o Enterprise). Si utilizas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva **GitHub Copilot app**.

## Instalar y configurar la aplicación GitHub Copilot

El primer paso para utilizar la aplicación GitHub Copilot es instalarla. Hay versiones disponibles para Windows, macOS y Linux. Instala la aplicación, autentícate y añade el repositorio de Tailspin Toys.

1. En un navegador, abre la [página de la aplicación GitHub Copilot][download-app].
2. Descarga la aplicación para tu plataforma e instálala siguiendo las instrucciones de la página.
3. Abre la aplicación una vez instalada.
4. Selecciona **Sign in to GitHub** y sigue las indicaciones para autenticarte. Si utilizas GitHub Enterprise Cloud con residencia de datos, selecciona **Use GitHub Enterprise** cuando se solicite e introduce tu nombre de host `*.ghe.com`. GitHub Enterprise Server no es compatible.
5. Si el asistente de configuración inicial te ofrece seleccionar un repositorio, selecciona el repositorio de Tailspin Toys que has creado a partir de la plantilla. También puedes omitir este paso y añadir el proyecto después.
6. Elige un tema cuando se te solicite y completa la configuración inicial.
7. Busca el repositorio en **Sessions**, en la barra lateral. Si ya aparece en la lista, no tienes que añadirlo de nuevo.
8. Si todavía no está conectado, selecciona **+** junto a **Sessions** para crear una sesión y, después, selecciona **Add GitHub repository**. Usa el propietario y el nombre del repositorio que anotaste en los requisitos previos.
9. Confirma que el repositorio aparece en la barra lateral. En el diseño que se muestra aquí, las carpetas de repositorio, como `tailspin-toys`, se agrupan en **Sessions** y las sesiones individuales aparecen debajo de cada repositorio.

## Familiarizarse con el espacio de trabajo

Con el proyecto conectado, dedica un momento a conocer el espacio de trabajo. La aplicación organiza todo en varias áreas de la barra lateral:

- **New**: permite iniciar una nueva sesión de chat con Copilot.
- **Pull requests**: muestra tus solicitudes de cambios mediante la integración nativa con GitHub de la aplicación. Desde aquí puedes examinar y filtrar solicitudes, comprobar el estado de CI y revisarlas sin salir de la aplicación.
- **Issues**: muestra tus incidencias de la misma manera. Desde aquí puedes examinarlas, filtrarlas e iniciar una sesión a partir de una incidencia.
- **Automations**: contiene tareas de agente guardadas que se ejecutan según una programación o bajo demanda. Son útiles para gestionar listas de tareas, realizar el mantenimiento periódico del proyecto o delegar otras tareas rutinarias. El resumen enlaza a esta función como siguiente paso, no como otro ejercicio del taller.
- **Customize**: permite añadir funciones a la aplicación Copilot mediante servidores del Protocolo de contexto de modelo (MCP), plugins, habilidades y otros componentes. La usarás para configurar MCP de Playwright.
- **Chats**: contiene conversaciones breves para preguntas e intercambio de ideas que no necesitan una rama ni un espacio de trabajo propios. Esta sección aparece después de iniciar el primer chat. Si no está visible, selecciona **+** junto a **Sessions** para iniciar el primer chat.
- **Sessions**: agrupa las carpetas de repositorio y las sesiones de agente. Selecciona un repositorio, como `tailspin-toys`, para abrir su vista, o selecciona una sesión debajo para volver a esa conversación. Cada sesión se ejecuta en su propio espacio de trabajo aislado, por lo que puedes ejecutar varias a la vez sin que sus cambios entren en conflicto. Iniciarás la primera sesión cuando añadas las valoraciones por estrellas.

A medida que avances en el taller, explorarás el espacio de trabajo.

> [!TIP]
> Si tienes dudas, pregunta a Copilot. Si no sabes cómo hacer algo o si es posible, puedes preguntarle y te ayudará a orientarte.

### Localizar el backlog preparado

Prácticamente todos los proyectos tienen trabajo pendiente, y Tailspin Toys no es una excepción. Vamos a explorar el backlog que se creó al generar el repositorio a partir de la plantilla.

1. En **Sessions**, en la barra lateral, selecciona la carpeta del repositorio Tailspin Toys, no una sesión individual. Después, selecciona **Issues** en la navegación superior del repositorio.
2. Busca estas incidencias por su título, sin dar por hecho cuáles son sus números:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecciona una incidencia para leer los detalles. Cada incidencia también sirve como punto de partida para una sesión de agente. Empezarás desde la incidencia de filtrado después de completar un primer cambio rápido.

> [!NOTE]
> Las listas de **Issues** y **Pull requests** se filtran automáticamente para mostrar solo los elementos de los repositorios que has añadido a la aplicación Copilot. Para ver elementos de trabajo de otros repositorios, añádelos a la aplicación.

## Probar un chat rápido

Una buena forma de familiarizarte con la aplicación es utilizarla para conocer la propia aplicación. Un **chat rápido** es una herramienta adecuada para ello: permite formular preguntas o intercambiar ideas sin crear una rama ni un árbol de trabajo, por lo que resulta útil para una consulta breve y puntual que no requiere una sesión.

1. En la barra lateral, selecciona **+** junto a **Chats** para abrir un chat nuevo. Si **Chats** todavía no está visible, selecciona **+** junto a **Sessions** para iniciar tu primer chat; después aparecerá **Chats**.
2. Pregunta a la aplicación cómo funcionan sus sesiones:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. Lee la respuesta en la vista de conversación. Verás que cada sesión se ejecuta en su propio árbol de trabajo de Git aislado, lo que permite ejecutar varios agentes en paralelo sin que sus cambios entren en conflicto. Puedes continuar la conversación o iniciar un chat nuevo cuando quieras.

## Resumen y siguientes pasos

¡Enhorabuena! Has instalado la aplicación GitHub Copilot, conectado el proyecto y explorado el espacio de trabajo. Has aprendido a:

- instalar la aplicación e iniciar sesión en GitHub.
- añadir un proyecto desde su repositorio de GitHub.
- familiarizarte con el espacio de trabajo y localizar el backlog preparado en **Issues**.
- usar un chat rápido para formular una pregunta breve y puntual.

A continuación, [iniciarás tu primera sesión de agente][next-lesson] y la utilizarás para mostrar una valoración por estrellas en las tarjetas de los juegos.

## Recursos

- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Introducción a la aplicación GitHub Copilot][getting-started]
- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
