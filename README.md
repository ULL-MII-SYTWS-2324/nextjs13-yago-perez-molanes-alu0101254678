## Next.js Master Class
This repo contains all the course files for the Next.js Master Class on Net Ninja Pro. There is a branch for every lesson. Select the lesson you need from the branch dropdown.

Visit [Net Ninja Pro](https://netninja.dev) to view this course and many more.

## Getting Started with the Project

First, run the development server:

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
Lo que se pretende hacer en esta parte del curso es crear un formulario en el que el usuario pueda introducir los datos para crear un ticket, y así añadir la funcionalidad de añadir tickets, aparte de visualizarlos.

Para ello, se ha creado una página dentro del directorio tickets con el siguiente contenido:

```jsx
import CreateForm from './CreateForm'

export default async function CreateTicket() {
  return (
    <main>
      <h2 className="text-center">Open a New Ticket</h2>
      <CreateForm />
    </main>
  )
}
```

Luego tenemos un componente del lado del cliente llamado CreateForm que tiene el siguiente contenido:

```jsx
"use client"

import { useRouter } from "next/navigation"
import { useState } from "react"

export default function CreateForm() {
  const router = useRouter()

  const [title, setTitle] = useState('')
  const [body, setBody] = useState('')
  const [priority, setPriority] = useState('low')
  const [isLoading, setIsLoading] = useState(false)

  const handleSubmit = async (e)  => {
    e.preventDefault()
    setIsLoading(true)

    const newTicket = { title, body, priority, user_email: 'mario@netninja.dev' }

    const res = await fetch('http://localhost:4000/tickets', {
      method: "POST",
      headers: {"Content-Type": "application/json"},
      body: JSON.stringify(newTicket)
    })

    if (res.status === 201) {
      router.refresh()
      router.push('/tickets')
    }
    
  }

  return (
    <form onSubmit={handleSubmit} className="w-1/2">
      <label>
        <span>Title:</span>
        <input
          required 
          type="text"
          onChange={(e) => setTitle(e.target.value)}
          value={title}
        />
      </label>
      <label>
        <span>Title:</span>
        <textarea
          required
          onChange={(e) => setBody(e.target.value)}
          value={body}
        />
      </label>
      <label>
        <span>Priority:</span>
        <select 
          onChange={(e) => setPriority(e.target.value)}
          value={priority}
        >
          <option value="low">Low Priority</option>
          <option value="medium">Medium Priority</option>
          <option value="high">High Priority</option>
        </select>
      </label>
      <button 
        className="btn-primary" 
        disabled={isLoading}
      >
      {isLoading && <span>Adding...</span>}
      {!isLoading && <span>Add Ticket</span>}
    </button>
    </form>
  )
}
```
Luego, en la página de los tickets, también nos encontramos con un botón que si pulsamos en él nos lleva a la página para añadir un ticket:

```jsx
import { Suspense } from "react"
import TicketList from "./TicketList"
import Loading from "../loading"
import Link from "next/link"

export default function Tickets() {
  return (
    <main>
      <nav>
        <div>
          <h2>Tickets</h2>
          <p><small>Currently open tickets.</small></p>
        </div>
        <Link href="/tickets/create" className="ml-auto">
          <button className="btn-primary">New Ticket</button>
        </Link>
      </nav>
      <Suspense fallback={<Loading />}>
        <TicketList />
      </Suspense>
    </main>
  )
}
```

Este sería el resultado:

![Captura 1](./images/screenshot-1.png)
![Captura 2](./images/screenshot-2.png)