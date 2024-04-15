Next.js tiene soporte incorporado para los Módulos CSS usando la extensión **.module.css**.

Los Módulos CSS tienen un **alcance local** del CSS creando automáticamente un **nombre de clase único**. Esto le permite utilizar el mismo nombre de clase en diferentes archivos sin preocuparse por las colisiones.

## Uso

Los módulos CSS pueden ser importados en cualquier archivo dentro del directorio ``app``:

``app/dashboard/layout.tsx``

```jsx
import styles from './styles.module.css';

export default function DashboardLayout({ children }: {
  children: React.ReactNode
}) {
  return <section className={styles.dashboard}>{children}</section>;
}
```

``app/dashboard/styles.module.css``

```css
.dashboard {
  padding: 24px;
}
```

## Características adicionales

Next.js incluye características adicionales para mejorar la experiencia de autoría al añadir estilos:

- Cuando se ejecuta localmente con ``next dev``, las hojas de estilo locales (ya sean globales o módulos CSS) se beneficiarán de **Fast Refresh** para reflejar instantáneamente los cambios a medida que se guardan las ediciones.
- Cuando se construya para producción con ``next build``, los archivos CSS se agruparán en menos archivos **.css minificados** para reducir el número de peticiones de red necesarias para recuperar los estilos.
- Si **desactiva JavaScript**, los estilos se seguirán cargando en la compilación de **producción** (siguiente inicio). Sin embargo, JavaScript sigue siendo necesario para que Next Dev habilite la actualización rápida.