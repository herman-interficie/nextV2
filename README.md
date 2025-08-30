## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.


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