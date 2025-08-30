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