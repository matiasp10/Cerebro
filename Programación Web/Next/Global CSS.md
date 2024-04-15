Los estilos globales pueden importarse a cualquier diseño, página o componente dentro del directorio de la aplicación.

> Es bueno saberlo: Esto es diferente del directorio pages, donde sólo puedes importar estilos globales dentro del archivo `_app.js`.
 
Por ejemplo, considere una hoja de estilos llamada `app/global.css`:

```css
body {
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}
```

Dentro del diseño raíz (``app/layout.js``), importa la hoja de estilos ``global.css`` para aplicar los estilos a todas las rutas de tu aplicación:

```jsx
// These styles apply to every route in the application
import './global.css';

export default function RootLayout({ children }: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

