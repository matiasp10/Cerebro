> **Es bueno saberlo**:
> 
> - Las rutas API deben seguir definiéndose en el directorio `pages/api/*` y no trasladarse al directorio `app`.
> - Estamos considerando cómo serían las rutas API en el directorio `app`.
> - Algunos casos de uso en los que se utilizaba una ruta API para mantener seguros los tokens de acceso cuando se llamaba a una API externa desde el cliente pueden hacerse ahora directamente en Server Components.

Cualquier archivo dentro de la carpeta ``pages/api`` es mapeado a ``/api/*`` y será tratado como un punto final de la API en lugar de una ruta.

Por ejemplo, la siguiente ruta API ``pages/api/user.ts`` devuelve una respuesta json con un código de estado 200:

![[Pasted image 20221120105706.png]]

``pages/api/user.ts``

```ts
import { NextApiRequest, NextApiResponse } from 'next'

export default function handler(req: NextApiRequest, res: NextApiResponse) {
  res.status(200).json({ name: 'John Doe' })
}
```
