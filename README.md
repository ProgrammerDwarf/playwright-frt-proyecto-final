# Playwright E2E & API Test Automation Framework - Conduit (RealWorld App)

Este repositorio contiene un framework de automatización de pruebas de extremo a extremo (E2E) y API para la aplicación [Conduit (RealWorld)](https://github.com/gothinkster/realworld?tab=readme-ov-file). El proyecto está construido con [Playwright](https://playwright.dev/) y TypeScript, y sigue las prácticas aprendidas durante el curso de E2E Testing con Playwright del profesor Patricio Miner, estás prácticas incluyen lo que es el modelo Page Object Model (POM) y pruebas híbridas (UI + API).

La creación de este proyecto es generar una vitrina de las habilidades aprendidas aplicadas a una aplicación un poco más cercana a lo que sería un entorno real en cuanto a la automatización de pruebas web modernas se refiere.

## 🚀 Aplicación Bajo Prueba (AUT)

Como objeto de pruebas se tomó una de las implementaciones del proyecto RealWorld que, en palabras más o menos simples, es una replica del sitio Medium.com, o busca serlo en cuanto a funcionalidad.

  * **Repositorio github:** [Proyecto](https://github.com/yukicountry/realworld-nextjs-rsc?tab=readme-ov-file)
  * **Aplicación Web (Frontend):** [Next.js + React Server Components ](https://realworld-nextjs-rsc.vercel.app/)
  * **Backend:**:  [Demo API](https://api.realworld.show/api)
  * **Documentación de la API:** [RealWorld API Docs (Swagger)](https://docs.realworld.show/)

-----

## ✨ Características del Framework

  * **Playwright + TypeScript:** Para pruebas rápidas, fiables y con tipado seguro.
  * **Page Object Model (POM):** Todo el código de la UI está estructurado en Clases de Página y Componentes para un mantenimiento sencillo y cero duplicación.
  * **Pruebas E2E (UI):** Flujos de usuario críticos (registro, login, creación de artículos, comentarios).
  * **Pruebas de API:** Pruebas directas contra la API de Conduit para validar el backend.
  * **Pruebas Híbridas:** Uso de llamadas de API para *setup* y *teardown* de las pruebas de UI, haciéndolas más rápidas y robustas (ej. login por API).
  * **Autenticación Optimizada:** El `global-setup` se encarga del login por API una sola vez, guardando el estado (`storageState`) para que todas las pruebas de UI se ejecuten ya autenticadas.
  * **Gestión de Entornos:** Configuración de múltiples entornos (ej. Staging, Prod) usando variables de entorno y archivos de configuración.
  * **Reportes:** Generación de reportes HTML de Playwright para analizar fallos, con trazas y videos adjuntos en caso de fallo.

-----

## 📂 Estructura del Proyecto

```plaintext
/
├── .env.example        # Plantilla de las variables de entorno necesarias
├── .gitignore
├── global-setup.ts     # Script para la autenticación global por API
├── playwright.config.ts  # Archivo de configuración principal (proyectos, reportes)
│
├── pages/              # Page Object Model (POM)
│   ├── components/     # Componentes reutilizables (Navbar, Footer, etc.)
│   ├── BasePage.ts     # Clase base con lógica compartida
│   ├── LoginPage.ts
│   └── ArticleEditorPage.ts
│
├── tests/              # (Directorio de Pruebas - testDir)
│   ├── api/            # Pruebas 100% de API
│   └── e2e/            # Pruebas End-to-End (UI)
│
└── utils/              # Herramientas y datos de prueba
    └── environments.ts # Configuración de URLs por entorno
```

-----

## 🛠️ Instalación y Setup

Para ejecutar este proyecto localmente, sigue estos pasos:

1.  **Clonar el repositorio:**

    ```bash
    git clone https://github.com/TU_USUARIO/TU_REPO.git
    cd TU_REPO
    ```

2.  **Instalar dependencias:**

    ```bash
    npm install
    ```

3.  **Instalar los navegadores de Playwright:**

    ```bash
    npx playwright install
    ```

4.  **Configurar variables de entorno:**

      * Crea una cuenta de prueba en la [app de Conduit](https://realworld-nextjs-rsc.vercel.app/).
      * Copia el archivo `.env.example` y renómbralo a `.env`.
      * Edita el archivo `.env` y añade tus credenciales de prueba.

    <!-- end list -->

    ```ini
    # .env
    TEST_USER_EMAIL="tu-usuario@correo.com"
    TEST_USER_PASS="TuPassword123"
    ```

-----

## ▶️ Cómo Ejecutar las Pruebas

Este proyecto está configurado con scripts de NPM para ejecutar diferentes conjuntos de pruebas:

  * **Ejecutar todas las pruebas (API y E2E):**

    ```bash
    npx playwright test
    ```

  * **Ejecutar solo las pruebas End-to-End (UI) en modo Headless:**

    ```bash
    npx playwright test --project=chromium
    ```
    Ejecuta las pruebas limitándose al proyecto de navegador especificado en tu playwright.config.ts. Aísla las pruebas de UI de las de API.

  * **Ejecutar solo las pruebas de API:**

    ```bash
    npx playwright test --project="API Tests"
    ```
    Ejecuta las pruebas limitándose al nombre exacto del proyecto que creaste para tus pruebas de API.

  * **Ejecutar pruebas de E2E con el navegador (UI Mode):**

    ```bash
    npx playwright test --ui
    ```
    Abre la Interfaz de Usuario (UI Mode). La mejor herramienta para la depuración interactiva, permitiendo inspeccionar, depurar y filtrar pruebas.

  * **Ejecutar pruebas con un tag específico (ej. @smoke):**

    ```bash
    npx playwright test --grep @smoke    
    ```
    Ejecuta solo las pruebas que contengan el tag @smoke (o cualquier otro tag) en su título o en el código.

  * **Ejecutar una carpeta específica:**
      
    ```bash
    npx playwright test tests/E2E
    ```

  * **Ejecutar un archivo específico:**
      
    ```bash
    npx playwright test tests/login.spec.ts
    ```

  * **Ejecutar una prueba por nombre:**
      
    ```bash
    npx playwright test -g "debe iniciar sesión"
    ```

  * **Ejecutar en modo Headed (Ver navegador):**
      
    ```bash
    npx playwright test --headed
    ```
    Ejecuta las pruebas de UI mostrando el navegador de forma visible. Útil para la depuración visual sin abrir el modo UI completo.

  * **Detenerse en el primer fallo:**

    ```bash
    npx playwright test --max-failures=1
    ```
    Detiene la ejecución tan pronto como falla la primera prueba. Ideal para el desarrollo local.
    
  * **Generar Reporte:**
  
    ```bash
    npx playwright test --reporter=html
    ```
    Genera o actualiza el reporte HTML de los resultados de la prueba.  
  
### 📊 Ver Reportes

Después de una ejecución, puedes ver el reporte HTML completo con:

```bash
npx playwright show-report
```

### ⚖️ Licencia
Este proyecto está licenciado bajo la Licencia MIT.

Puntos Importantes:

    Permisividad: Esta es una licencia muy permisiva que te permite utilizar, copiar, modificar y distribuir libremente este código.

    Copyright Original: El proyecto de la Aplicación Bajo Prueba (AUT), Conduit (RealWorld App), cuyo repositorio original es gothinkster/realworld, también está liberado bajo la Licencia MIT.

    Requisito: La única condición es que la nota de licencia y copyright original debe incluirse en cualquier copia sustancial o redistribución.

Para obtener el texto completo de la licencia, consulta el archivo LICENSE en la raíz de este repositorio.