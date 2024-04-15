El algoritmo de clonado estructurado copia objetos JavaScript complejos. Se utiliza internamente al invocar `structuredClone()`, para transferir datos entre `Workers` mediante `postMessage()`, almacenar objetos con `IndexedDB` o copiar objetos para otras `API`.

Clona recorriendo el objeto de entrada mientras mantiene un mapa de referencias visitadas previamente, para evitar ciclos de recorrido infinito.

# Cosas que no funcionan con el clon estructurado

- Los objetos de **función** no pueden ser duplicados por el algoritmo de clonación estructurada; al intentarlo se lanza una excepción DataCloneError.
- La clonación de **nodos DOM** también lanza una excepción DataCloneError.
- Algunas **propiedades** de los objetos no se conservan:
	- La propiedad **lastIndex** de los objetos **RegExp** no se conserva.
	- Los **descriptores de propiedades**, **setters**, **getters** y características similares a los **metadatos** no se duplican. Por ejemplo, si un objeto está marcado como de sólo lectura con un descriptor de propiedad, será de lectura/escritura en el duplicado, ya que ese es el valor predeterminado.
	- La **cadena de prototipos** no se recorre ni se duplica.

# Tipos soportados

## Tipos JS

- Array
- ArrayBuffer
- Boolean
- DataView
- Date
- Tipos Error.
- Map
- Object objects: solo objetos planos (por ejemplo de objetos literales).
- Tipos primitivos, excepto Symbol.
- RegExp (lastIndex no se conserva).
- Set
- String
- TypedArray

## Tipos Error

Para los tipos de error, el nombre del error debe ser uno de los siguientes: **Error**, **EvalError**, **RangeError**, **ReferenceError**, **SyntaxError**, **TypeError**, **URIError** (o se establecerá como "Error").

Los navegadores deben serializar las propiedades nombre y mensaje, y se espera que serialicen otras propiedades "interesantes" de los errores como pila, causa, etc.

## Tipos Web/API

- AudioData
- Blob
- CropTarget
- CryptoKey
- DOMException: browsers must serialize the properties name and message. Other attributes may also be serialized/cloned.
- DOMMatrix
- DOMMatrixReadOnly
- DOMPoint
- DOMPointReadOnly
- DOMQuad
- DOMRect
- DOMRectReadOnly
- File
- FileList
- FileSystemDirectoryHandle
- FileSystemFileHandle
- FileSystemHandle
- GPUCompilationInfo
- GPUCompilationMessage
- ImageBitmap
- ImageData
- RTCCertificate
- VideoFrame