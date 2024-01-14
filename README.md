## Next.js Master Class

This repo contains all the course files for the Next.js Master Class on Net Ninja Pro. There is a branch for every lesson. Select the lesson you need from the branch dropdown.

See [Next.js 13 Crash Course Tutorial #1 - Introduction & New Features](https://www.youtube.com/watch?v=TJQbDPGzm0Y&list=PL4cUxeGkcC9jZIVqmy_QhfQdi6mzQvJnT) YouTube list by Net Ninja

Visit [Net Ninja Pro](https://netninja.dev) to view this course and many more.

## Getting Started with the Project

First, run the `json-server`:

```bash
npm run json-server
```

then run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.js`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.


### Experience along the lesson
En esta parte del curso se enseña como funciona el renderizado estático, es decir, le vamos a dar más peso al cliente esta vez, para ello observamos como en el proyecto cambia la estructura.

La página del layout, la página de la barra de navegación, la página de inicio y la página en la que se muestran todos los tickets se siguen quedando como están, pero la página para mostrar un tickete individual sí que cambia.

```jsx
import { notFound } from "next/navigation"

export const dynamicParams = true // default val = true

export async function generateStaticParams() {
  const res = await fetch('http://localhost:4000/tickets')

  const tickets = await res.json()
 
  return tickets.map((ticket) => ({
    id: ticket.id
  }))
}
```

Esa función se ejcuta para obtener un prerenderizado para todos los tickets, y servirlos cuando se necesiten, es decir, el array de objetos será utilizado por NextJS para generar las rutas estáticas para cada tickete en tiempo de compilación.

Luego como novedad también se encuentra una página 404 por defecto.

Esto sucede cuando se intenta acceder a un ticket que no existe:

![Captura 1](./images/screenshot-1.png)