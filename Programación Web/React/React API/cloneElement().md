```jsx
React.cloneElement(
  element,
  [config],
  [...children]
)
```

Clona y retorna un elemento React usando `element` como punto de partida. `config` debe contener todas las nuevas props, `key`, o `ref`. El elemento resultante tendrá las props del elemento original con las nuevas props combinadas superficialmente. Los nuevos hijos reemplazarán los hijos existentes. `key` y `ref` del elemento original serán preservadas si `key` y `ref` no están presentes en la configuración.

`React.cloneElement()` es casi equivalente a:

```jsx
<element.type {...element.props} {...props}>{children}</element.type>
```

Sin embargo, también preserva las `refs`. Esto significa que, si se obtiene un hijo con una `ref` en él, no la robará accidentalmente de su ancestro. Se obtendrá la misma `ref` adjunta al nuevo elemento. Las nuevas `ref` o `key` reemplazarán a las antiguas si estuviesen presentes.

Esta API fue introducida como un reemplazo al obsoleto `React.addons.cloneWithProps()`.