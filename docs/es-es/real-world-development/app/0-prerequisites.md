---
title: "Lección 0 - Requisitos previos"
description: "Prepara el entorno para las lecciones de la aplicación GitHub Copilot: instala Node.js para el proyecto Tailspin Toys y crea tu propia copia del repositorio a partir de la plantilla."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La aplicación de GitHub Copilot es una aplicación de escritorio que sirve como centro de operaciones para Copilot y GitHub. Proporciona acceso rápido a las incidencias y solicitudes de cambios y, por supuesto, te permite desarrollar con GitHub Copilot. Durante este taller trabajarás en local con la aplicación Tailspin Toys, creada con Astro, mediante la aplicación GitHub Copilot. Antes de empezar, comprueba que Node.js esté instalado en local y, después, instala la aplicación Copilot.

En esta lección aprenderás a:

- instalar Node.js para que las pruebas del proyecto se puedan ejecutar en tu equipo.
- crear tu propia copia del proyecto Tailspin Toys a partir de la plantilla.

## Instalar Node.js

En varias lecciones pedirás a un agente que desarrolle funcionalidades y ejecute en local el conjunto de pruebas de Tailspin Toys, para lo que se necesita [Node.js][nodejs], el único entorno de ejecución que requiere el proyecto. Instala la versión actual de soporte a largo plazo (LTS).

La opción más sencilla en todas las plataformas es usar el instalador oficial:

1. Abre una ventana del terminal en tu sistema operativo, por ejemplo, Windows Terminal, Terminal de macOS o el que utilices habitualmente.
2. Ejecuta los comandos siguientes para comprobar las versiones instaladas de Node.js y npm:

   ```shell
   node --version
   npm --version
   ```

3. Si ambos comandos se ejecutan correctamente y Node.js cumple los requisitos del archivo `README` y de `package.json` del proyecto, puedes pasar a la sección siguiente.

> [!TIP]
> Solo tienes que completar estos pasos si no tienes Node.js instalado o necesitas actualizarlo.

4. Abre la [página de descarga de Node.js][node-download].
5. Descarga la versión **LTS** correspondiente a tu sistema operativo.
6. Ejecuta el instalador y acepta las opciones predeterminadas. En Windows, mantén seleccionada la opción **Add to PATH**.
7. Una vez instalado, abre una nueva ventana del terminal.
8. Confirma la instalación en el nuevo terminal con estos comandos:

   ```bash
   node --version
   npm --version
   ```

9. Comprueba que se muestran las versiones instaladas de Node.js y npm.

> [!IMPORTANT]
> El agente de la aplicación Copilot también debe poder ejecutar `node --version` y `npm --version`. Que funcionen en tu terminal habitual no garantiza que estén disponibles en la aplicación.
>
> 1. Después de instalar Node.js o cambiar PATH, cierra la aplicación por completo y vuelve a abrirla.
> 2. Si alguno de los comandos sigue fallando en una sesión, sigue los [pasos para solucionar problemas del entorno de sesión][session-environment] antes de continuar.

> [!IMPORTANT]
> Cada árbol de trabajo también necesita las dependencias del proyecto y Chromium de Playwright para las pruebas de extremo a extremo (E2E).
>
> 1. Sigue las instrucciones del `README` del repositorio de Tailspin Toys al preparar un árbol de trabajo.
> 2. Revisa cualquier solicitud de instalación antes de aprobarla.

## Configurar el repositorio del taller

Trabajarás con tu propia copia del proyecto Tailspin Toys, creada a partir del [repositorio de plantilla][template-repository]. El nuevo repositorio contiene todos los archivos que necesita el taller y lo conectarás cuando instales la aplicación.

1. En una nueva ventana del navegador, ve al [repositorio de GitHub del taller][tailspin-template].
2. Crea tu propia copia del repositorio seleccionando **Use this template** en la página del repositorio del taller. A continuación, selecciona **Create a new repository**.

   ![Botón Use this template con Create a new repository seleccionado en el menú desplegable](../../../_images/app-0-use-template.png)

3. Si estás realizando el taller en un evento organizado por GitHub o Microsoft, sigue las instrucciones de los mentores. En caso contrario, crea el repositorio en una organización donde tengas acceso a GitHub Copilot.

   ![Formulario Create a new repository con github-samples/tailspin-toys seleccionado como plantilla y el nombre del repositorio escrito](../../../_images/app-0-create-repository.png)

4. Anota la ruta del repositorio que has creado (`organization-or-user-name/repository-name`), ya que la consultarás más adelante durante el taller.

> [!NOTE]
> Al crear el repositorio a partir de la plantilla, se crea automáticamente un backlog de incidencias de GitHub. Trabajarás con ellas durante todo el taller; no tienes que crear ninguna.

Para evitar problemas de configuración, comprueba que utilizas una copia nueva de la plantilla y que incluye los componentes necesarios:

5. Confirma que el repositorio contiene las instrucciones, el código de la aplicación, las pruebas, una habilidad `quality-checks` y una extensión de Canvas.
6. Si utilizas una copia anterior, confirma con la persona que facilita el taller que contiene los archivos necesarios. Durante el taller personalizarás la habilidad y crearás un agente de control de calidad.

## Resumen y siguientes pasos

Ya tienes todo listo. En esta lección has:

- instalado Node.js para que el proyecto se pueda compilar y probar en tu equipo.
- creado tu propia copia del repositorio de Tailspin Toys a partir de la plantilla.

A continuación, [instalarás la aplicación GitHub Copilot][next-lesson], conectarás el repositorio que acabas de crear y te familiarizarás con el espacio de trabajo.

## Recursos

- [Descargar Node.js][node-download]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]

[next-lesson]: ../1-install-copilot-app/
[nodejs]: https://nodejs.org/
[node-download]: https://nodejs.org/en/download
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[session-environment]: ../3-agent-modes/#iniciar-una-sesión-desde-la-incidencia
[tailspin-template]: https://github.com/github-samples/tailspin-toys
