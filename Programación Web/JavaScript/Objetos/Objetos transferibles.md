Los objetos transferibles son objetos que poseen recursos que pueden ser transferidos de un contexto a otro, asegurando que los recursos sólo están disponibles en un contexto a la vez. Tras una transferencia, el objeto original deja de ser utilizable; ya no apunta al recurso transferido, y cualquier intento de leer o escribir el objeto lanzará una excepción.

Los objetos transferibles se utilizan habitualmente para compartir recursos que sólo pueden exponerse de forma segura a un único subproceso de JavaScript a la vez. Por ejemplo, un `ArrayBuffer` es un objeto transferible que posee un bloque de memoria. Cuando un búfer de este tipo se transfiere entre subprocesos, el recurso de memoria asociado se separa del búfer original y se adjunta al objeto búfer creado en el nuevo subproceso. El objeto buffer en el thread original ya no es utilizable porque ya no posee un recurso de memoria.

La transferencia también puede utilizarse al crear copias profundas de objetos con `structuredClone()`. Tras la operación de clonación, los recursos transferidos se mueven en lugar de copiarse al objeto clonado.

El mecanismo utilizado para transferir los recursos de un objeto depende del objeto. Por ejemplo, cuando un `ArrayBuffer` se transfiere entre hilos, el recurso de memoria al que apunta se mueve literalmente entre contextos en una operación rápida y eficiente de copia cero. Otros objetos pueden transferirse copiando el recurso asociado y borrándolo del contexto anterior.

No todos los objetos son transferibles.

# Objetos soportados

- ArrayBuffer
- MessagePort
- ReadableStream
- WritableStream
- TransformStream
- AudioData
- ImageBitmap
- VideoFrame
- OffscreenCanvas
- RTCDataChannel
