---
title: "Lección 12 - Desplegar el sitio con GitHub Pages"
description: "Configura con la aplicación GitHub Copilot un flujo de trabajo de Pages, revisa la solicitud de incorporación de cambios (PR) y comprueba el Space Quiz publicado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Dale al Space Quiz un hogar público mediante GitHub Pages. Copilot puede preparar el flujo de trabajo y guiar el despliegue, pero debes revisar los cambios y confirmar que el sitio está disponible.

En esta lección, vas a:

- pedir a Copilot que configure el despliegue en GitHub Pages;
- revisar el flujo de trabajo y la solicitud de incorporación de cambios antes de combinarlos;
- seguir el despliegue y comprobar el sitio publicado.

## Escenario

El Space Quiz ya está en un repositorio de GitHub, pero aún no es fácil probarlo. Publicar el sitio de un solo archivo con GitHub Pages lo hace accesible mediante una URL pública sin añadir un servidor ni una dependencia de ejecución.

## Pedir a Copilot que despliegue el sitio

Envía el prompt siguiente en la sesión de la aplicación Copilot para `space-quiz`.

1. Pide a Copilot que configure Pages, cree un flujo de trabajo y una solicitud de incorporación de cambios (PR), y compruebe el sitio:

   ```plaintext
   Enable GitHub Pages for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and merge it after required checks pass. Monitor the deployment until it succeeds, then report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
   ```

![Diagrama de tres fases: una solicitud de incorporación de cambios de space-quiz combinada; una ejecución correcta de GitHub Actions Deploy website con los pasos Build website, Upload artifact y Deploy to Pages; y el Space Quiz publicado en yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

> [!WARNING]
> Este prompt pide al agente que cree y combine una PR y cambie la configuración de Pages del repositorio. Revisa las diferencias, los permisos de despliegue y las solicitudes de aprobación de GitHub antes de continuar.

## Revisar el flujo de trabajo y comprobar el despliegue

Revisa los cambios antes de combinarlos y espera a que el despliegue termine para verificar el sitio.

1. Confirma que el README solo se ha añadido si el repositorio no tenía uno.
2. Revisa los cambios de la PR, incluidos los pasos de compilación y despliegue del flujo de trabajo.
3. Combina la PR solo cuando se hayan superado las comprobaciones obligatorias.
4. Sigue la ejecución de despliegue de GitHub Actions hasta que finalice correctamente.
5. Abre la URL indicada y confirma que se carga el Space Quiz.

Si el agente no puede habilitar Pages o combinar la PR, sigue las instrucciones específicas que te proporcione. No des por terminada la tarea hasta que el despliegue se complete y el sitio esté disponible.

## Resumen y siguientes pasos

El Space Quiz ya está publicado. En esta lección, has:

- pedido a Copilot que configure el despliegue en GitHub Pages;
- revisado el flujo de trabajo y la solicitud de incorporación de cambios antes de combinarla;
- seguido el despliegue y comprobado el sitio publicado.

Continúa con la [Lección 13: Revisión y próximos pasos][next-lesson].

[next-lesson]: ../13-review/
