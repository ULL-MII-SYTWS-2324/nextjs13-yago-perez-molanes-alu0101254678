## Next.js Master Class

This repo contains all the course files for the Next.js Master Class on Net Ninja Pro. 
There is a branch `lesson-1`  ... `lesson-43` for every lesson. Select the lesson you need from the branch dropdown.

See [Next.js 13 Crash Course Tutorial #1 - Introduction & New Features](https://www.youtube.com/watch?v=TJQbDPGzm0Y&list=PL4cUxeGkcC9jZIVqmy_QhfQdi6mzQvJnT) YouTube list by Net Ninja. There are 13 videos.

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

### Experience along lesson
En esta parte se ha aprendido a crear una página 404 que se renderiza cuando se accede a algún tipo de recurso que no existe, se han creado dos páginas, una para cuando se accede a un ticket que no existe, y otra para el resto del sitio web.

```jsx
import Link from "next/link"

export default function NotFound() {
  return (
    <main className="text-center">
      <h2 className="text-3xl">We Hit a Brick Wall.</h2>
      <p>We could not find the ticket you were looking for.</p>
      <p>Go back to all <Link href="/tickets">tickets</Link>.</p>
    </main>
  )
}
```

```jsx
import Link from "next/link"

export default function NotFound() {
  return (
    <main className="text-center">
      <h2 className="text-3xl">There was a problem.</h2>
      <p>We could not find the page you were looking for.</p>
      <p>Go back to the <Link href="/">dashboard</Link>.</p>
    </main>
  )
}
```

Aquí se prueba su funcionamiento:

![Captura 1](./images/screenshot-1.png)
![Captura 2](./images/screenshot-2.png)