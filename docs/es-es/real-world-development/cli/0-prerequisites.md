---
title: "Ejercicio 0 - Requisitos previos"
description: "Crea tu propia copia de Tailspin Toys y prepara un Codespace de GitHub para el taller de Copilot CLI."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Antes de empezar los ejercicios de Copilot CLI, tienes que dejarlo todo preparado. Crearás tu propia copia del repositorio Tailspin Toys y pondrás en marcha un [Codespace][codespaces], cuyo terminal integrado usarás para instalar y ejecutar Copilot CLI en el siguiente ejercicio.

En este ejercicio aprenderás a:

- crear tu propia copia del proyecto Tailspin Toys a partir de la plantilla.
- crear un Codespace y confirmar que el proyecto está listo.

## Configurar el repositorio del taller

Para trabajar con Tailspin Toys, necesitarás tu propia copia del proyecto creada a partir del [repositorio de plantilla][tailspin-template]. El nuevo repositorio contiene todos los archivos que necesita el taller.

1. En una nueva ventana del navegador, ve a la [plantilla de Tailspin Toys][tailspin-template].
2. Crea tu propia copia del repositorio seleccionando **Use this template** y, a continuación, **Create a new repository**.
3. Si estás realizando el taller en un evento organizado por GitHub o Microsoft, sigue las instrucciones de los mentores. En caso contrario, crea el repositorio en una organización donde tengas acceso a GitHub Copilot.
4. Anota la ruta del repositorio que has creado (`organization-or-user-name/repository-name`), ya que la consultarás más adelante durante el taller.

> [!NOTE]
> Al crear el repositorio a partir de la plantilla, se crea automáticamente un backlog de incidencias de GitHub. Trabajarás con ellas durante todo el taller; no tienes que crear ninguna.

Para evitar problemas de configuración, comprueba que utilizas una copia nueva de la plantilla y que incluye los componentes necesarios:

5. Confirma que el repositorio contiene las instrucciones, el código de la aplicación, las pruebas, una habilidad `quality-checks` y el backlog que usarás.
6. Si utilizas una copia anterior, confirma con la persona que facilita el taller que contiene los archivos necesarios.

## Crear un Codespace

A continuación, usarás un Codespace para completar el taller.

[GitHub Codespaces][codespaces] es un entorno de desarrollo en la nube que te permite escribir, ejecutar y depurar código directamente en el navegador. Proporciona un editor completo con compatibilidad con varios lenguajes de programación, extensiones y herramientas.

1. Ve al repositorio que acabas de crear.
2. Selecciona **Code**.
3. Selecciona la pestaña **Codespaces** y, a continuación, **Create codespace on main**.
4. Espera a que termine la configuración del Codespace. La plantilla instala las dependencias del proyecto, Chromium de Playwright y la base de datos local.
5. Si aparece el mensaje **Do you trust the authors of the files in this folder?**, selecciona **Trust Folder & Continue**.
6. Abre un terminal en la raíz del repositorio e inicia la aplicación:

   ```bash
   npm run dev
   ```

7. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser** y comprueba que se carga el sitio de Tailspin Toys.
8. Vuelve al terminal y detén el servidor de desarrollo con <kbd>Ctrl</kbd>+<kbd>C</kbd>.

## Resumen y siguientes pasos

Ya tienes todo listo. En este ejercicio has:

- creado tu propia copia del proyecto Tailspin Toys a partir de la plantilla.
- creado un Codespace y confirmado que el proyecto estaba listo.

A continuación, [instalarás GitHub Copilot CLI][next-lesson] en tu Codespace y te autenticarás con tu cuenta de GitHub.

## Recursos

- [Información general de GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-install-copilot-cli/
[codespaces]: https://github.com/features/codespaces
