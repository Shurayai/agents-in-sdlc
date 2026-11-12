---
title: "Ejercicio 1 - Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Agente en la nube de Copilot →][next-lesson]

El contexto es fundamental cuando se trabaja con IA generativa. Si una tarea debe hacerse de una forma concreta o Copilot necesita información adicional, conviene que ese contexto esté disponible. Los [archivos de instrucciones][instruction-files] aportan directrices para que Copilot entienda no solo qué debe hacer, sino también cómo.

En este ejercicio, vas a:

- explorar cómo las instrucciones personalizadas del repositorio y las instrucciones específicas de rutas proporcionan a Copilot contexto del proyecto, directrices de código y estándares de documentación;
- añadir un estándar general al archivo `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los recorridos de VS Code y CLI, aquí no compararás prompts de antes y después. El agente en la nube de Copilot trabaja de forma asíncrona con incidencias de GitHub, por lo que su influencia es más difícil de mostrar en tiempo real. La verás más adelante, al revisar las solicitudes de incorporación de cambios (PR) que genere.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene directrices de desarrollo que incluyen:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz de usuario (UI) debe estar en modo oscuro y tener un aspecto moderno.
- El código debe incluir comentarios de documentación de TypeScript (TSDoc).
- Cada archivo debe comenzar con un bloque de comentarios que describa su propósito.

Los archivos de instrucciones proporcionan a Copilot la información necesaria para trabajar de acuerdo con estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias sobre el estilo de desarrollo y los requisitos del proyecto. Puedes especificar convenciones, bibliotecas y los comentarios que deben incluirse en el código. Las instrucciones pueden aplicarse a todo el repositorio o a determinados tipos de archivos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` se envía a Copilot en **todas** las solicitudes del repositorio. Debe contener información general del proyecto, como la pila tecnológica, una descripción del trabajo, buenas prácticas y directrices globales.
- Los archivos `.github/instructions/*.instructions.md` proporcionan directrices para tareas o tipos de archivo concretos, como TypeScript, Astro, componentes de interfaz o pruebas unitarias.

> [!NOTE]
> En un IDE, los archivos de instrucciones solo se usan para generar código en Copilot Chat, no para las finalizaciones de código ni las sugerencias de siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot usan tanto las instrucciones del repositorio como los archivos `*.instructions.md` que incluyen frontmatter `applyTo`.
>
> Copilot también [admite otros formatos de instrucciones][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Buenas prácticas para gestionar archivos de instrucciones

Los ejemplos del proyecto muestran un enfoque posible para organizar las instrucciones:

- Mantén `copilot-instructions.md` centrado en directrices del proyecto, como la descripción, la estructura y los estándares globales de código.
- Usa `*.instructions.md` para tipos de archivo —pruebas unitarias, componentes Astro o capa de datos— y tareas concretas.
- Escribe en lenguaje natural, con directrices claras y ejemplos de código correctos e incorrectos.

No hay una única forma de crear archivos de instrucciones o de usar IA; la experimentación te ayudará a encontrar lo que funciona en el proyecto.

> [!TIP]
> Conviene que los proyectos con GitHub Copilot tengan un conjunto sólido de instrucciones. En este proyecto encontrarás directrices para [actualizaciones de la interfaz][ui-instructions] y [Astro][astro-instructions].
>
> Copilot también puede ayudar a generar instrucciones. Cada entorno ofrece esta opción de una forma distinta (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI). El ejercicio de cada entorno indicará cuándo usarla.
>
> Para encontrar plantillas, consulta [awesome-copilot][awesome-copilot], que reúne archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explorar los archivos de instrucciones personalizadas del proyecto

Revisa los archivos de instrucciones del repositorio para identificar el contexto que Copilot recibirá.

1. Abre `.github/copilot-instructions.md`.
2. Lee la descripción del proyecto y las secciones **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, fíjate en las directrices de **GitHub Actions Workflows**, que se aplican a las interacciones con Copilot.
3. Explora los archivos de `.github/instructions`, incluidas las instrucciones de Astro, la capa de datos de Drizzle y las pruebas.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`, que define el glob relativo a la raíz del repositorio. Por ejemplo, coincide con los archivos de prueba TypeScript que siguen el patrón `**/*.test.ts`.
5. Revisa las instrucciones específicas para las pruebas unitarias del proyecto.
6. Abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Observa los enlaces a otros archivos de instrucciones y a archivos existentes del proyecto; las rutas son relativas al archivo de instrucciones.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` describe los estándares del proyecto, pero aún no exige documentación dentro del código. A continuación, añadirás directrices para los comentarios TSDoc y los encabezados de archivo.

## Añadir un estándar general al repositorio

Añadirás un estándar de documentación al repositorio. El agente en la nube lo recibirá cuando trabaje en incidencias asignadas a partir de este punto.

1. En el terminal del codespace, crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. Vuelve a abrir `.github/copilot-instructions.md`.
3. Localiza la sección **Code formatting requirements**, cerca de la línea 27. Comprueba que aún no contiene una directriz para documentar el código.
4. Añade estas líneas de Markdown debajo de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. Guarda `copilot-instructions.md`.

> [!TIP]
> Las instrucciones globales pertenecen a `.github/copilot-instructions.md`; las instrucciones específicas para lenguajes, tipos de archivo y tareas pueden ir en archivos `*.instructions.md`.

## Confirmar, enviar y combinar la actualización

El agente en la nube lee las instrucciones de la rama a la que se dirige la incidencia. En el siguiente ejercicio, partirá de `main`, así que la actualización debe estar en esa rama para que Copilot la reciba.

1. Prepara y confirma el cambio:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envía la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una PR de `custom-instructions-cloud` a `main` y combínala. Así, el agente en la nube podrá usar las instrucciones cuando trabaje en las incidencias del siguiente ejercicio.

> [!TIP]
> Si prefieres trabajar directamente en `main` para este taller, puedes omitir la rama y confirmar el cambio en `main`. El uso de una rama representa un flujo de trabajo habitual en un proyecto real.

## Resumen y siguientes pasos

En este ejercicio, has:

- explorado cómo las instrucciones personalizadas del repositorio y las instrucciones específicas de rutas proporcionan contexto, directrices de código y estándares de documentación;
- añadido un estándar general al archivo `.github/copilot-instructions.md`.

Verás el efecto de las instrucciones en las PR que genere el agente en la nube.

A continuación, [asignarás tu primera incidencia al agente en la nube de Copilot][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
