---
title: "Ejercicio 1 - Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Modo de agente →][next-lesson]

El contexto es fundamental cuando se trabaja con IA generativa. Los [archivos de instrucciones][instruction-files] proporcionan directrices para que Copilot entienda cómo generar código y qué contexto del proyecto debe tener en cuenta.

En este ejercicio, vas a:

- explorar cómo las instrucciones personalizadas del repositorio y las instrucciones específicas de rutas proporcionan a Copilot contexto del proyecto, directrices de código y estándares de documentación;
- generar una primera parte de los datos de filtrado —un helper de editoriales— con las instrucciones actuales;
- añadir un estándar general al archivo `.github/copilot-instructions.md`;
- repetir el mismo prompt y observar cómo el código adopta el nuevo estándar;
- confirmar los cambios de instrucciones y del helper en `main` para que Copilot pueda usarlos en el siguiente ejercicio.

> [!CAUTION]
> El código generado puede no seguir todos los estándares en cada ejecución. Copilot no es determinista. El objetivo es observar la tendencia tras actualizar las instrucciones, no obtener siempre el mismo resultado.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene directrices de desarrollo que incluyen:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz debe estar en modo oscuro y tener un aspecto moderno.
- El código debe incluir comentarios de documentación TSDoc.
- Cada archivo debe comenzar con un bloque de comentarios que describa su propósito.

Usarás archivos de instrucciones para proporcionar a Copilot la información necesaria para seguir estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias sobre el estilo de desarrollo y los requisitos del proyecto. Puedes especificar convenciones, bibliotecas y los comentarios que debe incluir el código. Las instrucciones pueden aplicarse a todo el repositorio o a determinados tipos de archivo.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` se envía a Copilot en **todas** las solicitudes del repositorio y contiene información general, como la pila tecnológica, una descripción del proyecto, buenas prácticas y directrices globales.
- Los archivos `.github/instructions/*.instructions.md` proporcionan directrices para tareas o tipos de archivo concretos, como TypeScript, Astro, componentes de interfaz o pruebas unitarias.

> [!NOTE]
> En un IDE, los archivos de instrucciones solo se usan para generar código en Copilot Chat, no para las finalizaciones de código ni las sugerencias de siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot usan las instrucciones del repositorio y los archivos `*.instructions.md` con frontmatter `applyTo`.
>
> Copilot también [admite otros formatos de instrucciones][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Buenas prácticas para gestionar archivos de instrucciones

Los ejemplos del proyecto muestran una forma de organizar las instrucciones:

- Mantén `copilot-instructions.md` centrado en directrices generales del proyecto, como su descripción, estructura y estándares globales de código.
- Usa `*.instructions.md` para tipos de archivo —pruebas unitarias, componentes Astro o capa de datos— y tareas concretas.
- Escribe en lenguaje natural, con directrices claras y ejemplos de código correctos e incorrectos.

No hay una única forma de crear instrucciones o de usar IA. La experimentación te ayudará a encontrar lo que funciona para el proyecto.

> [!TIP]
> Los proyectos con GitHub Copilot deberían tener un conjunto sólido de instrucciones. En este proyecto encontrarás directrices para [actualizaciones de la interfaz][ui-instructions] y [Astro][astro-instructions].
>
> Copilot también puede ayudar a generar instrucciones. Cada entorno ofrece esta opción de una forma distinta (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI). El ejercicio de cada entorno indicará cuándo usarla.
>
> Para encontrar plantillas, consulta [awesome-copilot][awesome-copilot], que reúne archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explorar los archivos de instrucciones del proyecto

Revisa los archivos de instrucciones incluidos en el repositorio para identificar el contexto que Copilot recibirá.

1. Abre `.github/copilot-instructions.md`.
2. Lee la descripción del proyecto y las secciones **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, fíjate en las directrices de **GitHub Actions Workflows**, que se aplican a las interacciones con Copilot.
3. Explora los archivos de `.github/instructions`, incluidas las instrucciones de Astro, Drizzle y pruebas.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`. El glob es relativo a la raíz del repositorio y puede coincidir con pruebas TypeScript como `**/*.test.ts`.
5. Revisa las instrucciones específicas para crear pruebas unitarias.
6. Abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Observa los enlaces a otras instrucciones y a archivos de ejemplo. Las rutas son relativas al archivo de instrucciones.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` describe los estándares del proyecto, pero aún no exige documentación dentro del código. A continuación, añadirás directrices para comentarios TSDoc y encabezados de archivo.

## Crear una rama para los cambios

Crea una rama para separar el helper de editoriales y las instrucciones del trabajo posterior.

1. Vuelve al codespace del ejercicio anterior.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions
   ```

## Usar Copilot Chat antes de actualizar las instrucciones

Primero generarás el helper con las instrucciones actuales. Después, actualizarás las instrucciones y enviarás el mismo prompt para comparar el resultado.

> [!TIP]
> **Abrir Copilot Chat**
>
> Antes de continuar, vuelve al codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo pueden variar según el ejercicio; se indicarán cuando sean relevantes.

1. Cierra las pestañas del editor que no necesites para que Copilot use solo el contexto pertinente.
2. Abre `src/lib/publishers.ts` para indicar dónde debe estar el helper.
3. En el menú desplegable de agentes de la vista Chat, selecciona **Agent** para que Copilot pueda modificar archivos.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Envía este prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot explorará el proyecto y aplicará los cambios, posiblemente también a las pruebas del helper.
6. Comprueba que el helper es una función tipada que recibe un cliente `db` como primer argumento y devuelve una matriz tipada de editoriales. Esta convención procede de `.github/instructions/drizzle.instructions.md`, que se aplica a `src/lib/*.ts`.
7. Observa que al código propuesto le faltan comentarios TSDoc y un encabezado de archivo.

> [!CAUTION]
> Como Copilot no es determinista, puede añadir comentarios aunque aún no estén en las instrucciones. Si ocurre, no pasa nada: el objetivo es observar la mejora de coherencia después de actualizar las instrucciones.

## Añadir un estándar general al repositorio

Añade una directriz a `.github/copilot-instructions.md` para que Copilot genere documentación dentro del código.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Localiza **Code formatting requirements**, cerca de la línea 27, y observa que todavía no contiene una regla para la documentación del código.
3. Añade estas líneas debajo de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda el archivo.

> [!TIP]
> Las instrucciones globales pertenecen a `.github/copilot-instructions.md`; las instrucciones específicas para lenguajes, tipos de archivo y tareas pueden ir en archivos `*.instructions.md`.

## Repetir el prompt y observar el cambio

Vuelve a enviar el prompt original para que Copilot aplique las directrices actualizadas al helper.

1. En Copilot Chat, selecciona **New Chat** para iniciar una conversación limpia.
2. Vuelve a seleccionar `src/lib/publishers.ts` para que Copilot se centre en el archivo.
3. Envía exactamente el mismo prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Observa que el archivo propuesto incluye un bloque de comentarios similar al siguiente:

   ```typescript
   /**
    * Helpers de acceso a datos de editoriales para la plataforma de financiación colectiva de Tailspin Toys.
    * Proporciona funciones para recuperar información de editoriales de la base de datos.
    */
   ```

5. Comprueba que la función propuesta incluye un comentario TSDoc similar a este:

   ```typescript
   /**
    * Devuelve una lista de todas las editoriales con su id y su nombre.
    *
    * @param db - El cliente de base de datos de Drizzle.
    * @returns Una promesa que se resuelve en una matriz de objetos de editoriales.
    */
   ```

Copilot ya tiene una directriz nueva y la ha aplicado al código que usarás en el siguiente ejercicio.

## Confirmar las instrucciones y enviar la rama

Confirma la actualización de instrucciones y el helper para que el siguiente ejercicio pueda partir de este trabajo.

1. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Comprueba que aparecen los cambios:

   ```bash
   git status
   ```

3. Prepara y confirma las instrucciones y el helper:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Si git status muestra otras actualizaciones complementarias (por ejemplo, pruebas), añade también esos archivos.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envía la rama:

   ```bash
   git push -u origin custom-instructions
   ```

## Crear y combinar una solicitud de incorporación de cambios

Usa Copilot para relacionar la rama con la incidencia correspondiente y crear la solicitud de incorporación de cambios (PR).

> [!NOTE]
> Este es el primer ejercicio en el que Copilot actuará en GitHub. La plantilla ya conecta las herramientas de GitHub con el proyecto. Puede que VS Code te pida iniciar sesión la primera vez que Copilot use una herramienta; sigue las indicaciones. En un ejercicio posterior conocerás la conexión mediante Model Context Protocol (MCP).

1. Abre Copilot Chat en el codespace.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir la vista y confirma que está seleccionado **Agent**.
3. Pide a Copilot que encuentre la incidencia sobre las instrucciones y cree una PR desde la rama actual:

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Cuando Copilot solicite permiso para realizar acciones de GitHub, revisa el comando y selecciona **Allow** si corresponde.
5. Cuando se cree la PR, pídele que la combine y vuelva a `main`:

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

6. Cuando Copilot solicite permiso para realizar acciones de GitHub o ejecutar comandos de shell, revisa el comando y selecciona **Allow** si corresponde.

Has creado y combinado una PR con ayuda de GitHub Copilot.

## Resumen y siguientes pasos

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones y has usado Copilot Chat en VS Code para:

- enviar un prompt de generación de código y observar el resultado con las instrucciones existentes;
- añadir un estándar general a `.github/copilot-instructions.md`;
- repetir el prompt y observar el efecto del nuevo estándar;
- confirmar en `main` las instrucciones y el helper para el siguiente ejercicio.

A continuación, aplicarás las instrucciones en [modo de agente][next-lesson] para añadir una funcionalidad en varios archivos.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Instrucciones personalizadas para GitHub Copilot][personal-instructions]
- [Awesome Copilot: archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
