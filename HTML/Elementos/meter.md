El elemento HTML ``<meter>`` representa un valor escalar dentro de un rango conocido o un valor fraccionario.

## Atributos

Este elemento incluye los atributos globales.

### Value

El valor numérico actual. Debe estar entre los valores mínimo y máximo (atributo min y atributo max) si se especifican. Si no se especifica o está mal formado, el valor es 0. Si se especifica, pero no está dentro del rango dado por el atributo min y el atributo max, el valor es igual al extremo más cercano del rango.

> **Nota**: a menos que el atributo value esté comprendido entre 0 y 1 (ambos inclusive), los atributos min y max deben definir el intervalo de modo que el valor del atributo value se encuentre dentro de él.

### min

El límite numérico inferior del rango medido. Debe ser inferior al valor máximo (atributo max), si se especifica. Si no se especifica, el valor mínimo es 0.

### max

El límite numérico superior del rango medido. Debe ser mayor que el valor mínimo (atributo min), si se especifica. Si no se especifica, el valor máximo es 1.

### low

El límite numérico superior del extremo inferior del rango medido. Debe ser mayor que el valor mínimo (atributo min), y también debe ser menor que el valor alto y el valor máximo (atributo high y atributo max, respectivamente), si se especifica alguno. Si no se especifica, o si es menor que el valor mínimo, el valor bajo es igual al valor mínimo.

### high

El límite numérico inferior del extremo superior del intervalo medido. Debe ser menor que el valor máximo (atributo max), y también debe ser mayor que el valor bajo y el valor mínimo (atributo low y atributo min, respectivamente), si se especifica alguno. Si no se especifica, o si es mayor que el valor máximo, el valor alto es igual al valor máximo.

### optimum

Este atributo indica el valor numérico óptimo. Debe estar dentro del intervalo (definido por los atributos mín. y máx.). Cuando se utiliza con los atributos bajo y alto, indica en qué punto del intervalo se considera preferible. Por ejemplo, si está entre el atributo min y el atributo low, entonces se considera preferible el rango inferior. El navegador puede colorear la barra del medidor de forma diferente dependiendo de si el valor es menor o igual que el valor óptimo.

https://caniuse.com/mdn-html_elements_meter