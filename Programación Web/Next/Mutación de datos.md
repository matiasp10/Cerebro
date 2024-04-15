El equipo de Next.js está trabajando en una nueva RFC para mutar datos en Next.js. Esta RFC aún no ha sido publicada. Por ahora, recomendamos el siguiente patrón:

Puedes mutar los datos dentro del directorio app con ``router.refresh()``.

## Ejemplo

Consideremos una lista. Dentro de su componente de servidor, usted obtiene la lista de elementos:

``app/page.tsx``

```tsx
import Todo from './todo';

interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

async function getTodos() {
  const res = await fetch('https://api.example.com/todos');
  const todos: Todo[] = await res.json();
  return todos;
}

export default async function Page() {
  const todos = await getTodos();
  return (
    <ul>
      {todos.map((todo) => (
        <Todo key={todo.id} {...todo} />
      ))}
    </ul>
  );
}
```

Cada elemento individual tiene su propio **Componente Cliente**. Esto permite que el componente utilice manejadores de eventos (como ``onClick`` o ``onSubmit``) para activar una mutación.

``app/todo.tsx``

```tsx
"use client";

import { useRouter } from 'next/navigation';

interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

async function update(id: number, completed: boolean, refresh: () => void) {
  await fetch(`https://api.example.com/todo/${id}`, {
    method: 'PUT',
    body: JSON.stringify({ completed }),
  });

  // Refresh the current route and fetch new data from the server
  refresh();
}

export default function Todo(todo: Todo) {
  const router = useRouter();

  return (
    <li>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={(e) => update(todo.id, !todo.completed, router.refresh)}
      />
      {todo.title}
    </li>
  );
}
```

Al llamar a ``refresh()``, la ruta actual se refrescará y obtendrá una lista actualizada de "todos" desde el servidor. Esto no afecta al historial del navegador, pero refresca los datos del root layout hacia abajo. Cuando se utiliza ``refresh()``, el estado del lado del cliente no se pierde, incluyendo tanto el estado de React como el del navegador.