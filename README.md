# Boilerplate de Proyecto Next.js & Reglas de Workflow

Bienvenido/a a este boilerplate y conjunto de reglas diseñado para iniciar rápidamente proyectos Next.js robustos, consistentes y mantenibles. Este documento sirve como guía central para entender la estructura, las tecnologías y, lo más importante, **tus responsabilidades** al trabajar en un proyecto basado en este template.

El objetivo es asegurar que todos los miembros del equipo sigan las mismas convenciones, resultando en un código de alta calidad, un flujo de trabajo eficiente y una aplicación escalable.

## ✨ Core Technologies (Stack Principal)

Este boilerplate está construido sobre las siguientes tecnologías clave:

*   **Framework:** Next.js 15+ (App Router)
*   **Lenguaje:** TypeScript (Strict Mode)
*   **Base de Datos:** Supabase (PostgreSQL)
*   **ORM:** Prisma
*   **Autenticación:** Supabase Auth (gestionado con `@supabase/ssr` para cookies seguras)
*   **UI:** Tailwind CSS + Shadcn UI
*   **Gestión de Estado:** Zustand (global), React Context, Estado Local (`useState`, `useReducer`)
*   **Validación:** Zod
*   **Testing:** Jest + React Testing Library
*   **Linting/Formateo:** ESLint + Prettier
*   **Server Actions:** Para mutaciones y lógica del lado del servidor.
*   **(Opcional) AI:** Vercel AI SDK

## 🚀 Getting Started (Primeros Pasos)

Para poner en marcha un nuevo proyecto usando este boilerplate:

1.  **Clonar/Copiar:** Clona este repositorio o copia su contenido a tu nuevo directorio de proyecto.
    ```bash
    # Ejemplo si es un template de GitHub
    # gh repo create my-new-project --template=YOUR_USERNAME/YOUR_BOILERPLATE_REPO
    # cd my-new-project
    # O simplemente copia los archivos
    ```
2.  **Instalar Dependencias:**
    ```bash
    npm install
    ```
3.  **Configurar Variables de Entorno:**
    *   Copia el archivo `.env.example` a `.env.local`.
    *   Rellena los valores necesarios en `.env.local`. Como mínimo necesitarás:
        *   `NEXT_PUBLIC_SUPABASE_URL`: URL de tu proyecto Supabase.
        *   `NEXT_PUBLIC_SUPABASE_ANON_KEY`: Clave anónima (pública) de Supabase.
        *   `SUPABASE_SERVICE_ROLE_KEY`: Clave de servicio (secreta) de Supabase (para operaciones admin/server).
        *   `DATABASE_URL`: URL de conexión directa a la base de datos PostgreSQL de Supabase (para Prisma). La encontrarás en la configuración de base de datos de tu proyecto Supabase.
        *   (Otras claves necesarias para APIs externas, Vercel AI SDK, etc.)
4.  **Sincronizar Prisma Schema (si es necesario):**
    *   Si tu base de datos Supabase ya tiene tablas, puedes introspectar:
        ```bash
        npx prisma db pull
        ```
    *   Si empiezas desde cero, revisa `prisma/schema.prisma` y ajústalo si es necesario.
5.  **Ejecutar Migraciones de Base de Datos:**
    ```bash
    npx prisma migrate dev --name init
    ```
    Esto aplicará las migraciones definidas en `prisma/migrations` a tu base de datos Supabase y generará el cliente Prisma.
6.  **(Opcional) Sembrar Datos Iniciales:**
    ```bash
    npx prisma db seed
    ```
    (Requiere que tengas configurado un script de seed en `prisma/seed.ts` y definido en `package.json`).
7.  **Iniciar Servidor de Desarrollo:**
    ```bash
    npm run dev
    # o
    yarn dev
    ```
8.  Abre [http://localhost:3000](http://localhost:3000) en tu navegador.

## 🧑‍💻 Tu Workflow y Responsabilidades

Como desarrollador/a trabajando con este boilerplate, se espera que sigas estos pasos y principios:

1.  **Setup Inicial:** Sigue los pasos de "Getting Started" cuidadosamente.
2.  **Entender las Reglas:** **Lee los archivos `.mdc` enlazados arriba.** Son la base de cómo construimos software aquí. ¡No te los saltes!
3.  **Seguir Convenciones:** Aplica estrictamente las reglas de estructura de código y convenciones de nombres.
4.  **Codificar:**
    *   Usa Server Components por defecto. Opta por Client Components (`'use client'`) solo cuando sea necesario (interactividad, hooks de cliente).
    *   Implementa la UI siguiendo las directrices de `ui.mdc`.
    *   Gestiona el estado según `state-management.mdc`.
    *   Usa Prisma para todas las operaciones de base de datos y Supabase Client JS principalmente para Auth/Storage/Realtime, como se define en `stack.mdc`.
    *   Implementa Server Actions para mutaciones siguiendo `server-actions.mdc`, incluyendo validación con Zod y revalidación de caché.
    *   Maneja errores de forma robusta (`error-handling.mdc`).
    *   Escribe código teniendo en cuenta el rendimiento (`performance.mdc`) y la seguridad (`security.mdc`).
5.  **Linting y Formateo:**
    *   Asegúrate de tener las extensiones de ESLint y Prettier en tu editor.
    *   El formateo y el linting básico se ejecutarán automáticamente antes de cada commit gracias a Husky y lint-staged. Corrige cualquier error reportado.
6.  **Escribir Pruebas:**
    *   Escribe tests unitarios y/o de integración para la nueva lógica de negocio, hooks complejos y componentes críticos, siguiendo las directrices de `testing.mdc`.
    *   Asegúrate de que todos los tests pasen (`npm run test`) antes de enviar tu código.
7.  **Control de Versiones (Git):**
    *   Crea ramas descriptivas para tus features/bugs (ej: `feat/user-profile`, `fix/login-error`).
    *   Escribe mensajes de commit claros y consistentes (idealmente siguiendo Conventional Commits).
    *   Realiza Pull Requests (PRs) para revisión de código antes de hacer merge a la rama principal (`main` o `develop`).
8.  **CI/CD:**
    *   Presta atención a los resultados del pipeline de CI/CD asociado a tus PRs. Asegúrate de que todos los chequeos (lint, test, build) pasen.
9.  **Dependencias:** Mantén las dependencias actualizadas (con precaución) y revisa vulnerabilidades periódicamente.


## ☁️ Despliegue

Se recomienda desplegar en plataformas como [Vercel](https://vercel.com/) o [Netlify](https://www.netlify.com/), que tienen excelente soporte para Next.js.

**Importante:** Asegúrate de configurar todas las variables de entorno requeridas (las de `.env.local`, especialmente las claves secretas) en la configuración de tu plataforma de despliegue.

---

¡Feliz codificación! Siguiendo estas guías, construiremos juntos una aplicación increíble. Si tienes dudas sobre alguna regla, no dudes en preguntar o proponer una mejora.