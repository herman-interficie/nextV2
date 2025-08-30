## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

Notas:
Archivos especiales
page.tsx: tiene el contenido de una ruta
layout.tsx: Contiene elementos que seran compartidos por multiples paginas



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