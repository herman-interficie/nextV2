## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

Notas:
Archivos especiales
page.tsx: tiene el contenido de una ruta
layout.tsx: Contiene elementos que seran compartidos por multiples paginas
loading.tsx: is a special Next.js file built on top of React Suspense. It allows you to create fallback UI to show as a replacement while page content loads.



Capitulo 2

* Se importa import '@/app/ui/global.css'; a  "/app/layout.tsx"
* Al crear un nuevo proyecto de next este preguntara si quieres usar tailWind y creara las configuracion inicial
* Se agrerga el triangulo negro en el hero con tailwind 
* Se creo un modulo nuevo en css /app/ui/home.module.css y se importo en /app/page.tsx
* este estilo remplaza el triangulo de taildwind
* En este ejemplo se usa una libreria clsx que sirve para dar clases dinamicas a los componentes EJEMPLO: "app/ui/invoices/status.tsx 10"

Capitulo 3 Fonts/Imagenes

*Agregamos una font al proyecto
* creamos app/ui/fonts.ts 
* importamos Inter y declaramos el sub set latin

'''
import { Inter } from 'next/font/google';
 
export const inter = Inter({ subsets: ['latin'] });
'''

* Lo agregamos al <body> element in /app/layout.tsx

* Agregamos un segundo font Lusitana y lo añadimos a app/page.tsx

*Desbloqueamos el logo acme que antes daba error al usar un font que no tenia

* IMAGENES next tiene su componente para renderizar imagenes de manera optima

* Puedes guardar imagenes en public

* Agregamos una imagen en app/page.tsx

* En el alto y ancho damos las dimenciones originales de la imagen para que obtenga bien el A/R

* Usamos el atributo hidden para poder ocultar las imagenes en un landscape especifico


Capitulo4 Layouts

* Next enruta por carpetas "app/dashboard/inovices/" es una ruta y carpeta

* Para cada ruta puedes crear una ionterfaz usando los archivos genericos layout.tsx y page.tsx

* Creamos /app/dashboard/page.tsx Esto generara una viw para el /dashboard 

* ahora esta pagina existe en http://localhost:3000/dashboard

* Creamos app/dashboard/customers/page.tsx y app/dashboard/invoices/page.tsx

*Ahora creamos un Layout

* Creamos el archivo app/dashboard/layout.tsx

* este archivo afectara a todos los pages debajo y a su nivel
* los componentes pages se renderizaran donde de pasa en atributo childern

* en el capitulo 3 agregamos un font a un layout. Este en especifico es especial y todo proyecto de next es requerido
Se llama RootLayout y en este se agregan los metadatos y los tags

Capitulo 5 Links

* En next el componente <Link />  permite hacer navegacion desde el cliente
*Para usarlo hay que importarlo y reemplazar los <a> por <Links>

*Ahora agregaremos la funcionalidad de ver en que pagina estamos usando el hook de react usePathname();

* Lo agregamos a app/ui/dashboard/nav-links.tsx

* como es un hoock de react hay que decirle que el componente renderiza en el cliente con 'use client';

* Agregamos el hoock y lo usamos junto a la libreria  clsx para asignar una clase dinamica a los elementos del sidebar

Capitulo6 Base de datos

* Nos creamos una cuenta en Vercel https://vercel.com/

* Registramos nuestro repo 

* Desplegamos

* Desde el dashborad elegimos Storage

* Creamos una base de datos SQL con neon

* agregamos los secretos al env

* ahora vamos a  localhost:3000/seed

* Para esto en el archivo app/seed/route.ts tenemos preparado un endpoint que se encarga de conectarse a la base de datos

* Ahora vamos a app/query/route.ts y descomentamos 

Capitulo 8 fech

* al momento de hacer una app normalmente se tiene que comunicar con servicios externos.

*  los componentes de servidor pueden usar async await y una libreria de fecht de react

* para escribir sql estamos usando la libreria postgres.js

* actualizamos el codigo de app/dashboard/page.tsx

* este es un componente de servidor asincrono, los que nos permite usar await

* There are also 3 components which receive data: <Card>, <RevenueChart>, and <LatestInvoices>. They are currently commented out and not yet implemented.

* descomentamos un codigo que activa un fech

* descomentamos el resto del codigo para los demas fechts

* dos cosas a discutir 1: los fechts crean un cuello de botella  2: los datos no cambian en tiempo real

* In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData()


Chapter 8 Static and Dynamic Rendering

*The data requests are creating an unintentional waterfall.

*The dashboard is static, so any data updates will not be reflected on your application.

* el dashboard que estamos haciendo es dinamico

* aca reside el problema de la cascada de peticiones

* simularemos un slow data fecht para el ejemplo

* desomentamos app/lib/data.ts console.log and setTimeout inside fetchRevenue()

* With dynamic rendering, your application is only as fast as your slowest data fetch.

Capitulo 9 Streming

* Streaming is a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.

* Streaming works well with React's component model, as each component can be considered a chunk.

There are two ways you implement streaming in Next.js:

At the page level, with the loading.tsx file (which creates <Suspense> for you).
At the component level, with <Suspense> for more granular control.

* Streaming a whole page with loading.tsx

* In the /app/dashboard folder, create a new file called loading.tsx

*loading.tsx is a special Next.js file built on top of React Suspense. It allows you to create fallback UI to show as a replacement while page content loads.

*Since <SideNav> is static, it's shown immediately. The user can interact with <SideNav> while the dynamic content is loading.

*The user doesn't have to wait for the page to finish loading before navigating away (this is called interruptable navigation).

* mejoraremos el componente

*cambiamos la estructura de carpetas para que el loading solo afecte a la pdina del dashboard

* ahora solo con un componente

* Para esto usaremos React suspense

* Pasaremos la llamada dentro del componente y aplicaremos el suspense

* ahora lo aplicamos para lates invoice

* Por ultimo agrupamos las cards

Capitulo 10 Pre rendering

*So far, you've learned about static and dynamic rendering, and how to stream dynamic content that depends on data. In this chapter, let's learn how to combine static rendering, dynamic rendering, and streaming in the same route with Partial Prerendering (PPR).

*Partial Prerendering is an experimental feature introduced in Next.js 14. The content of this page may be updated as the feature progresses in stability. PPR is only available with the Next.js canary releases (next@canary), not in the stable version of Next.js. We do not yet recommend using Partial Prerendering in production.

* pnpm install next@canary

* borramos todo lo del capitulo pasa ya que es experimental

Capitulo 11 busqueda y paginacion

* Learn how to use the Next.js APIs: useSearchParams, usePathname, and useRouter.

* Apliaremos el codigo de dashboard/invoices/page.tsx## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

Notas:
Archivos especiales
page.tsx: tiene el contenido de una ruta
layout.tsx: Contiene elementos que seran compartidos por multiples paginas
loading.tsx: is a special Next.js file built on top of React Suspense. It allows you to create fallback UI to show as a replacement while page content loads.



Capitulo 2

* Se importa import '@/app/ui/global.css'; a  "/app/layout.tsx"
* Al crear un nuevo proyecto de next este preguntara si quieres usar tailWind y creara las configuracion inicial
* Se agrerga el triangulo negro en el hero con tailwind 
* Se creo un modulo nuevo en css /app/ui/home.module.css y se importo en /app/page.tsx
* este estilo remplaza el triangulo de taildwind
* En este ejemplo se usa una libreria clsx que sirve para dar clases dinamicas a los componentes EJEMPLO: "app/ui/invoices/status.tsx 10"

Capitulo 3 Fonts/Imagenes

*Agregamos una font al proyecto
* creamos app/ui/fonts.ts 
* importamos Inter y declaramos el sub set latin

'''
import { Inter } from 'next/font/google';
 
export const inter = Inter({ subsets: ['latin'] });
'''

* Lo agregamos al <body> element in /app/layout.tsx

* Agregamos un segundo font Lusitana y lo añadimos a app/page.tsx

*Desbloqueamos el logo acme que antes daba error al usar un font que no tenia

* IMAGENES next tiene su componente para renderizar imagenes de manera optima

* Puedes guardar imagenes en public

* Agregamos una imagen en app/page.tsx

* En el alto y ancho damos las dimenciones originales de la imagen para que obtenga bien el A/R

* Usamos el atributo hidden para poder ocultar las imagenes en un landscape especifico


Capitulo4 Layouts

* Next enruta por carpetas "app/dashboard/inovices/" es una ruta y carpeta

* Para cada ruta puedes crear una ionterfaz usando los archivos genericos layout.tsx y page.tsx

* Creamos /app/dashboard/page.tsx Esto generara una viw para el /dashboard 

* ahora esta pagina existe en http://localhost:3000/dashboard

* Creamos app/dashboard/customers/page.tsx y app/dashboard/invoices/page.tsx

*Ahora creamos un Layout

* Creamos el archivo app/dashboard/layout.tsx

* este archivo afectara a todos los pages debajo y a su nivel
* los componentes pages se renderizaran donde de pasa en atributo childern

* en el capitulo 3 agregamos un font a un layout. Este en especifico es especial y todo proyecto de next es requerido
Se llama RootLayout y en este se agregan los metadatos y los tags

Capitulo 5 Links

* En next el componente <Link />  permite hacer navegacion desde el cliente
*Para usarlo hay que importarlo y reemplazar los <a> por <Links>

*Ahora agregaremos la funcionalidad de ver en que pagina estamos usando el hook de react usePathname();

* Lo agregamos a app/ui/dashboard/nav-links.tsx

* como es un hoock de react hay que decirle que el componente renderiza en el cliente con 'use client';

* Agregamos el hoock y lo usamos junto a la libreria  clsx para asignar una clase dinamica a los elementos del sidebar

Capitulo6 Base de datos

* Nos creamos una cuenta en Vercel https://vercel.com/

* Registramos nuestro repo 

* Desplegamos

* Desde el dashborad elegimos Storage

* Creamos una base de datos SQL con neon

* agregamos los secretos al env

* ahora vamos a  localhost:3000/seed

* Para esto en el archivo app/seed/route.ts tenemos preparado un endpoint que se encarga de conectarse a la base de datos

* Ahora vamos a app/query/route.ts y descomentamos 

Capitulo 8 fech

* al momento de hacer una app normalmente se tiene que comunicar con servicios externos.

*  los componentes de servidor pueden usar async await y una libreria de fecht de react

* para escribir sql estamos usando la libreria postgres.js

* actualizamos el codigo de app/dashboard/page.tsx

* este es un componente de servidor asincrono, los que nos permite usar await

* There are also 3 components which receive data: <Card>, <RevenueChart>, and <LatestInvoices>. They are currently commented out and not yet implemented.

* descomentamos un codigo que activa un fech

* descomentamos el resto del codigo para los demas fechts

* dos cosas a discutir 1: los fechts crean un cuello de botella  2: los datos no cambian en tiempo real

* In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData()


Chapter 8 Static and Dynamic Rendering

*The data requests are creating an unintentional waterfall.

*The dashboard is static, so any data updates will not be reflected on your application.

* el dashboard que estamos haciendo es dinamico

* aca reside el problema de la cascada de peticiones

* simularemos un slow data fecht para el ejemplo

* desomentamos app/lib/data.ts console.log and setTimeout inside fetchRevenue()

* With dynamic rendering, your application is only as fast as your slowest data fetch.

Capitulo 9 Streming

* Streaming is a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.

* Streaming works well with React's component model, as each component can be considered a chunk.

There are two ways you implement streaming in Next.js:

At the page level, with the loading.tsx file (which creates <Suspense> for you).
At the component level, with <Suspense> for more granular control.

* Streaming a whole page with loading.tsx

* In the /app/dashboard folder, create a new file called loading.tsx

*loading.tsx is a special Next.js file built on top of React Suspense. It allows you to create fallback UI to show as a replacement while page content loads.

*Since <SideNav> is static, it's shown immediately. The user can interact with <SideNav> while the dynamic content is loading.

*The user doesn't have to wait for the page to finish loading before navigating away (this is called interruptable navigation).

* mejoraremos el componente

*cambiamos la estructura de carpetas para que el loading solo afecte a la pdina del dashboard

* ahora solo con un componente

* Para esto usaremos React suspense

* Pasaremos la llamada dentro del componente y aplicaremos el suspense

* ahora lo aplicamos para lates invoice

* Por ultimo agrupamos las cards

Capitulo 10 Pre rendering

*So far, you've learned about static and dynamic rendering, and how to stream dynamic content that depends on data. In this chapter, let's learn how to combine static rendering, dynamic rendering, and streaming in the same route with Partial Prerendering (PPR).

*Partial Prerendering is an experimental feature introduced in Next.js 14. The content of this page may be updated as the feature progresses in stability. PPR is only available with the Next.js canary releases (next@canary), not in the stable version of Next.js. We do not yet recommend using Partial Prerendering in production.

* pnpm install next@canary

* borramos todo lo del capitulo pasa ya que es experimental

Capitulo 11 busqueda y paginacion

* Learn how to use the Next.js APIs: useSearchParams, usePathname, and useRouter.

* Apliaremos el codigo de dashboard/invoices/page.tsx

* Vamos a app/ui/search.tsx

* Create a new handleSearch function, and add an onChange listener to the <input> element. onChange will invoke handleSearch whenever the input value changes

* URLSearchParams is a Web API that provides utility methods for manipulating the URL query parameters. Instead of creating a complex string literal, you can use it to get the params string like ?page=1&query=a.

Here's a breakdown of what's happening:

${pathname} is the current path, in your case, "/dashboard/invoices".

As the user types into the search bar, params.toString() translates this input into a URL-friendly format.

replace(${pathname}?${params.toString()}) updates the URL with the user's search data. For example, /dashboard/invoices?query=lee if the user searches for "Lee".

The URL is updated without reloading the page, thanks to Next.js's client-side navigation (which you learned about in the chapter on navigating between pages.

defaultValue vs. value / Controlled vs. Uncontrolled

If you're using state to manage the value of an input, you'd use the value attribute to make it a controlled component. This means React would manage the input's state.

However, since you're not using state, you can use defaultValue. This means the native input will manage its own state. This is okay since you're saving the search query to the URL instead of state.

Finally, you need to update the table component to reflect the search query.

Navigate back to the invoices page.

Page components accept a prop called searchParams, so you can pass the current URL params to the <Table> component.

When to use the useSearchParams() hook vs. the searchParams prop?

You might have noticed you used two different ways to extract search params. Whether you use one or the other depends on whether you're working on the client or the server.

<Search> is a Client Component, so you used the useSearchParams() hook to access the params from the client.
<Table> is a Server Component that fetches its own data, so you can pass the searchParams prop from the page to the component.
As a general rule, if you want to read the params from the client, use the useSearchParams() hook as this avoids having to go back to the server.

Best practice: Debouncing

Ahora que todo funciona optimizaremos un poco

por cada stroke del teclado se hace una busqueda lo que estresa al navegador

Debouncing is a programming practice that limits the rate at which a function can fire. In our case, you only want to query the database when the user has stopped typing.

You can implement debouncing in a few ways, including manually creating your own debounce function. To keep things simple, we'll use a library called use-debounce

Adding pagination

After introducing the search feature, you'll notice the table displays only 6 invoices at a time. This is because the fetchFilteredInvoices() function in data.ts returns a maximum of 6 invoices per page.

Adding pagination allows users to navigate through the different pages to view all the invoices. Let's see how you can implement pagination using URL params, just like you did with search.

Navigate to the <Pagination/> component and you'll notice that it's a Client Component. You don't want to fetch data on the client as this would expose your database secrets (remember, you're not using an API layer). Instead, you can fetch the data on the server, and pass it to the component as a prop.

In /dashboard/invoices/page.tsx, import a new function called fetchInvoicesPages and pass the query from searchParams as an argument:

Here's a breakdown of what's happening:

createPageURL creates an instance of the current search parameters.
Then, it updates the "page" parameter to the provided page number.
Finally, it constructs the full URL using the pathname and updated search parameters.

The rest of the <Pagination> component deals with styling and different states (first, last, active, disabled, etc). We won't go into detail for this course, but feel free to look through the code to see where createPageURL is being called.

Finally, when the user types a new search query, you want to reset the page number to 1. You can do this by updating the handleSearch function in your <Search> component:

To summarize, in this chapter:

You've handled search and pagination with URL search parameters instead of client state.
You've fetched data on the server.
You're using the useRouter router hook for smoother, client-side transitions.
These patterns are different from what you may be used to when working with client-side React, but hopefully, you now better understand the benefits of using URL search params and lifting this state to the serve

Capitulo 12

In the previous chapter, you implemented search and pagination using URL Search Params and Next.js APIs. Let's continue working on the Invoices page by adding the ability to create, update, and delete invoices!

What React Server Actions are and how to use them to mutate data.

How to work with forms and Server Components.

Best practices for working with the native FormData object, including type validation.

How to revalidate the client cache using the revalidatePath API.

How to create dynamic route segments with specific IDs.

What are Server Actions?
React Server Actions allow you to run asynchronous code directly on the server. They eliminate the need to create API endpoints to mutate your data. Instead, you write asynchronous functions that execute on the server and can be invoked from your Client or Server Components.

Security is a top priority for web applications, as they can be vulnerable to various threats. This is where Server Actions come in. They include features like encrypted closures, strict input checks, error message hashing, host restrictions, and more — all working together to significantly enhance your application security.

Here are the steps you'll take to create a new invoice:

Create a form to capture the user's input.
Create a Server Action and invoke it from the form.
Inside your Server Action, extract the data from the formData object.
Validate and prepare the data to be inserted into your database.
Insert the data and handle any errors.
Revalidate the cache and redirect the user back to invoices page.

* creamos el archivo dashboard/invoices/create/page.tsx

Your page is a Server Component that fetches customers and passes it to the <Form> component. To save time, we've already created the <Form> component for you.

Navigate to the <Form> component, and you'll see that the form:

Has one <select> (dropdown) element with a list of customers.
Has one <input> element for the amount with type="number".
Has two <input> elements for the status with type="radio".
Has one button with type="submit".

ahora creamos una nueba accion en app/lib/actions.ts

Good to know: In HTML, you'd pass a URL to the action attribute. This URL would be the destination where your form data should be submitted (usually an API endpoint).

However, in React, the action attribute is considered a special prop - meaning React builds on top of it to allow actions to be invoked.

Behind the scenes, Server Actions create a POST API endpoint. This is why you don't need to create API endpoints manually when using Server Actions.

Tip: If you're working with forms that have many fields, you may want to consider using the entries() method with JavaScript's Object.fromEntries().

You'll notice that amount is of type string and not number. This is because input elements with type="number" actually return a string, not a number!

To handle type validation, you have a few options. While you can manually validate types, using a type validation library can save you time and effort. For your example, we'll use Zod, a TypeScript-first validation library that can simplify this task for you.

In your actions.ts file, import Zod and define a schema that matches the shape of your form object. This schema will validate the formData before saving it to a database.



