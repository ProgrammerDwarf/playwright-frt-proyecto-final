Test Charter #1: Flujo de Autenticación y Home Page
Misión del Charter
Elemento
Descripción
Explore
El módulo de Autenticación (Login, Registro) y la Home Page (Feed Global) de la aplicación Conduit.
With/using
Datos de prueba válidos e inválidos (usuarios, contraseñas, emails), las Dev Tools (pestaña Network y Elements) y un usuario de prueba.
To discover
 La estructura de las páginas, los componentes reutilizables (ej. Navbar, Footer), los locators más estables (IDs, roles, data-testid) y las llamadas API (XHR) clave.


Elemento
Detalle
Tester Name
ProgrammerDwarf
Environment
Navegador: Chrome (con Dev Tools abiertas)
URL Base
https://react-redux.realworld.io/



 Timebox y Cobertura
Cobertura
Flujo de Registro (Sign Up) - Éxito y Errores (ej. email ya existe)
Flujo de Inicio de Sesión (Sign In) - Éxito y Errores (ej. pass incorrecta)
Navegación de la Home Page (como invitado y como usuario logueado)
Feed Global vs. "Your Feed"
Paginación de artículos
Timebox
#Total Duration: 1 Hora (Sesión enfocada)
#Test Design and Execution: 50 minutos
#Bugs Investigation and Reporting: 10 minutos
POM Discovery Notes (Hallazgos para el Framework)
Setup and Prerequisites
Tener una cuenta de correo de prueba lista.
Tener la URL del frontend de Conduit elegida: https://react-redux.realworld.io/
1. Páginas Identificadas (Clases POM)
HomePage.ts (La página principal con la lista de artículos)
LoginPage.ts (Formulario de Sign In)
RegisterPage.ts (Formulario de Sign Up)
SettingsPage.ts (Página de configuración de perfil)
2. Componentes Reutilizables Identificados
NavbarComponent.ts (El header. Importante: Es diferente para invitados y usuarios logueados).
FooterComponent.ts (El pie de página. Es estático y está en todas las páginas).
ArticleListComponent.ts (La lista de artículos, se repite en el Feed Global y en "Your Feed").
TagsComponent.ts (La lista de "Popular Tags" en el sidebar).
3.  Locators Estables Clave (Contenido de Clases POM)
Elemento
Locator (Playwright)
Descripción
Login - Email
page.getByPlaceholder('Email')
Input de correo electrónico.
Login - Pass
page.getByPlaceholder('Password')
Input de contraseña.
Login - Submit
page.getByRole('button', { name: 'Sign in' })
Botón para iniciar sesión.
Navbar - "New Post"
page.getByRole('link', { name: 'New Post' })
Enlace para crear nuevo artículo.
Navbar - "Settings"
page.getByRole('link', { name: 'Settings' })
Enlace a la página de configuración.
Article List - Contenedor
page.locator('div.article-preview')
Contenedor de cada artículo en la lista.
Article List - Título
locator.locator('h1') o locator.getByRole('heading')
Título del artículo (usado dentro del contenedor).

4. API Calls (XHR) Identificadas
Flujo
Método
Endpoint
Notas de Uso
Login
POST
/api/users/login
Envía email/pass, devuelve un objeto user con un token.
Get Articles
GET
/api/articles
Devuelve el array de artículos para el feed.
Get Tags
GET
/api/tags
Devuelve el array de tags populares.


Conclusiones y Tareas Pendientes
Ideas for Improvement
El mensaje de error en el login ("Invalid credentials") es un poco genérico, pero está bien para el proyecto.
No hay un data-test-id en muchos elementos, por lo que tendremos que depender de getByRole y getByPlaceholder, lo cual es una buena práctica de todos modos.
Bugs
(Aquí anotarías cualquier bug funcional que encuentres durante la ejecución.)
Test Data
Campo
Valor
User
tester-pd-1@test.com
Password
Test1234!

Completion Criteria or Criteria of Done
✅ He definido las 4 clases de página principales.
✅ He identificado los 4 componentes reutilizables más importantes.
✅ Tengo los locators para el flujo de login y registro.
✅ He capturado la llamada API para login, get articles y get tags.


