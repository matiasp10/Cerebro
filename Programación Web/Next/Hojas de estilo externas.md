Las hojas de estilo publicadas por paquetes externos pueden importarse en cualquier lugar del directorio ``app``, incluidos los componentes colocados:

``app/layout.tsx``

```jsx
import 'bootstrap/dist/css/bootstrap.css';

export default function RootLayout({ children }: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className="container">{children}</body>
    </html>
  );
}
```

