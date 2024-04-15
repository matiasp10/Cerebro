La propiedad CSS `list-style-type` establece el marcador (como un disco, un carácter o un estilo de contador personalizado) de un elemento de lista.

El **color** del marcador será el _mismo que el color calculado_ del elemento al que se aplica.  
  
Sólo unos pocos elementos (`<li>` y `<summary>`) tienen un valor por defecto de **display**: `list-item`. Sin embargo, la propiedad `list-style-type` puede aplicarse a cualquier elemento cuyo valor de visualización sea **`list-item`**. Además, como esta propiedad se **hereda**, puede establecerse en un elemento padre (normalmente `<ol>` o `<ul>`) para que se aplique a todos los elementos de la lista.
## Sintaxis

```css
/* Partial list of types */
list-style-type: disc;
list-style-type: circle;
list-style-type: square;
list-style-type: decimal;
list-style-type: georgian;
list-style-type: trad-chinese-informal;
list-style-type: kannada;

/* <string> value */
list-style-type: "-";

/* Identifier matching an @counter-style rule */
list-style-type: custom-counter-style;

/* Keyword value */
list-style-type: none;

/* Global values */
list-style-type: inherit;
list-style-type: initial;
list-style-type: revert;
list-style-type: revert-layer;
list-style-type: unset;
```

La propiedad `list-style-type` puede definirse como cualquiera de:  

- un valor `<custom-ident>`
- un valor `symbols()`
- un valor `<string>`
- la palabra clave `none`.

>[!note] Tenga en cuenta que
>Algunos tipos requieren una fuente adecuada instalada para mostrarse como se espera. El `cjk-ideographic` es idéntico al `trad-chinese-informal`; existe por razones de legado.
## Valores

- `<custom-ident>`: An identifier matching the value of a @counter-style or one of the predefined styles:
- `symbols()` Defines an anonymous style of the list.
- `<string>` The specified string will be used as the item's marker.
- none No item marker is shown.
- disc A filled circle (default value).
- circle A hollow circle.
- square A filled square.
- decimal Decimal numbers, beginning with 1. 
- cjk-decimal Han decimal numbers. 
- decimal-leading-zero Decimal numbers, padded by initial zeros. 
- lower-roman Lowercase roman numerals. 
- upper-roman Uppercase roman numerals. 
- lower-greek Lowercase classical Greek. 
- lower-alpha, lower-latin Lowercase ASCII letters. 
- upper-alpha, upper-latin Uppercase ASCII letters. 
- arabic-indic, -moz-arabic-indic Arabic-Indic numbers. 
- armenian Traditional Armenian numbering. 
- bengali, -moz-bengali Bengali numbering. 
- cambodian/khmer Cambodian/Khmer numbering. 
- cjk-earthly-branch, -moz-cjk-earthly-branch Han "Earthly Branch" ordinals. 
- cjk-heavenly-stem, -moz-cjk-heavenly-stem Han "Heavenly Stem" ordinals. 
- cjk-ideographic Identical to trad-chinese-informal. 
- devanagari, -moz-devanagari Devanagari numbering. 
- ethiopic-numeric Ethiopic numbering. 
- georgian Traditional Georgian numbering. 
- gujarati, -moz-gujarati Gujarati numbering. 
- gurmukhi, -moz-gurmukhi Gurmukhi numbering. 
- hebrew Traditional Hebrew numbering. 
- hiragana Dictionary-order hiragana lettering. 
- hiragana-iroha Iroha-order hiragana lettering. 
- japanese-formal Japanese formal numbering to be used in legal or financial documents. The - kanjis are designed so that they can't be modified to look like another correct one. 
- japanese-informal Japanese informal numbering. 
- kannada, -moz-kannada Kannada numbering. 
- katakana Dictionary-order katakana lettering. 
- katakana-iroha Iroha-order katakana lettering. 
- korean-hangul-formal Korean hangul numbering. 
- korean-hanja-formal Formal Korean Han numbering. 
- korean-hanja-informal Korean hanja numbering. 
- lao, -moz-lao Laotian numbering. 
- lower-armenian Lowercase Armenian numbering. 
- malayalam, -moz-malayalam Malayalam numbering. 
- mongolian Mongolian numbering. 
- myanmar, -moz-myanmar Myanmar (Burmese) numbering. 
- oriya, -moz-oriya Oriya numbering. 
- persian, -moz-persian Persian numbering. 
- simp-chinese-formal Simplified Chinese formal numbering. 
- simp-chinese-informal Simplified Chinese informal numbering. 
- tamil, -moz-tamil Tamil numbering. 
- telugu, -moz-telugu Telugu numbering. 
- thai, -moz-thai Thai numbering. 
- tibetan Tibetan numbering. 
- trad-chinese-formal Traditional Chinese formal numbering. 
- trad-chinese-informal Traditional Chinese informal numbering. 
- upper-armenian Traditional uppercase Armenian numbering. 
- disclosure-open Symbol indicating that a disclosure widget such as `<details>` is opened. 
- disclosure-closed Symbol indicating that a disclosure widget, like `<details>` is closed.