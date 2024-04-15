#### ¿Cuál es el objetivo de la librería Joi?

a - Llevar un log de los errores.

b - Validación de datos por medio de un schema

c - Manejo de errores http

La respuesta correcta es b: Validación de datos por medio de un schema.

Joi es una librería de validación de datos para Node.js que se utiliza para validar y verificar que los datos que se envían a una aplicación cumplan con ciertos criterios específicos. Esta librería permite definir un esquema de validación en forma de un objeto de configuración que describe los campos que se deben validar y cómo deben validarse. Joi se utiliza a menudo en aplicaciones web para validar datos de formularios, solicitudes HTTP y otros tipos de datos que se envían a una aplicación.

#### ¿Cuál método de express nos sirve para retornar un formato json como respuesta?

a - app.json({...})

b - app.xml({...})

c - app.sendJson({...})

La respuesta correcta es "a": app.json({...}).

En una aplicación de Node.js con Express, el método `json` se puede utilizar para enviar una respuesta en formato JSON a una solicitud HTTP. Este método recibe como argumento un objeto JavaScript y lo convierte en una cadena JSON antes de enviarlo como respuesta al cliente. Por ejemplo:

```js
app.get('/', function(req, res) {
  res.json({ message: 'Hello, world!' });
});
```

En cambio, "b" y "c" no son métodos válidos en Express para enviar una respuesta en formato JSON. Es importante tener en cuenta que el método `json` solo puede utilizarse para enviar respuestas de tipo application/json, mientras que el método `send` puede utilizarse para enviar respuestas de cualquier tipo, incluyendo JSON. Por ejemplo:

Copy code

```js
app.get('/', function(req, res) {
  res.send({ message: 'Hello, world!' });
});
```

Espero que esto haya sido de ayuda. ¿Hay algo más en lo que pueda ayudarte?

#### ¿Cuál es la definición más adecuada para el principio de Single Resposability?

a - Se trata de inyectar dependencias a nuestros componentes.

b - Cada módulo, clase o función debería tener una sola responsabilidad.

c - Logramos que cada función tenga efectos secundarios.

La respuesta correcta es b: Cada módulo, clase o función debería tener una sola responsabilidad.

El principio de Single Responsibility (también conocido como principio de una sola responsabilidad) es un principio de diseño de software que establece que cada módulo, clase o función debería tener una sola responsabilidad y que dicha responsabilidad debería estar completamente encapsulada dentro del módulo, clase o función. Esto significa que cada módulo, clase o función debería tener una sola razón para cambiar y que dichos cambios deberían afectar solo a ese módulo, clase o función y no a otros módulos, clases o funciones de la aplicación. El principio de Single Responsibility se utiliza para crear aplicaciones más mantenibles y modulares, ya que permite aislar los cambios en una sola parte de la aplicación y hacer que dichos cambios tengan un impacto mínimo en el resto de la aplicación.


#### ¿Cuál es la forma correcta para definir una ruta de tipo patch para actualizar una entidad?

a - router.update('/tasks', ...)

b - router.patch('/tasks', ...)

c - router.patch('/tasks/:id', ...)

La forma correcta para definir una ruta de tipo patch para actualizar una entidad es:

**c** router.patch('/tasks/:id', ...)

La ruta debe incluir el identificador de la entidad que se desea actualizar, de modo que se pueda hacer referencia a ella de manera única. El verbo HTTP utilizado para este tipo de solicitud es "PATCH", por lo que se debe utilizar el método patch() del router.

Es importante tener en cuenta que el verbo PATCH se utiliza para actualizar parcialmente una entidad, mientras que el verbo PUT se utiliza para reemplazar completamente una entidad. Por lo tanto, es importante elegir el verbo adecuado según la acción que se desee realizar.

#### ¿Qué parámetros debemos recibir para tener un middleware que lea errores?

a - solo el error

b - req, res y  next

c - error, req, res y next

Para tener un middleware que lea errores en una aplicación web, debes recibir al menos el parámetro "error" y "next" en la función del middleware. También es común recibir los parámetros "req" (request) y "res" (response) para tener acceso a más información sobre la solicitud y la respuesta del cliente.

Por ejemplo, un middleware para manejar errores podría tener una firma de función similar a esta:

`function errorHandler(error, req, res, next) {   // código para manejar el error }`

Donde "error" es el error que ocurrió durante el procesamiento de la solicitud, "req" es el objeto de solicitud, "res" es el objeto de respuesta y "next" es una función que se debe llamar para pasar el control al siguiente middleware en la cadena.

Es importante tener en cuenta que la firma de la función del middleware puede variar dependiendo del framework o librería que estés utilizando para construir tu aplicación web. Por lo tanto, es importante consultar la documentación del framework o librería en cuestión para obtener más información sobre cómo crear y usar middlewares.

#### ¿Cuál es la manera correcta de obtener parámetros tipo query de una ruta con GET?

a - const { limit, offset } = req.query;

b - const { limit, offset } = req.getQuery;

c - const { limit, offset } = req.queryParams;

La manera correcta de obtener parámetros tipo query de una ruta con GET es:

a const { limit, offset } = req.query;

Los parámetros tipo query son aquellos que se envían en la URL después del signo de interrogación (?) y se usan para enviar información adicional a la ruta. En el caso de una solicitud GET, estos parámetros se pueden acceder a través del objeto req (request) y del atributo query. Por ejemplo, si la solicitud es "GET /tasks?limit=10&offset=0", se puede acceder a los parámetros limit y offset de la siguiente manera:

const limit = req.query.limit; const offset = req.query.offset;

También es posible destruir el objeto query en una sola línea de código, como se muestra en la opción a.

Las opciones b y c son incorrectas, ya que no existen los atributos getQuery ni queryParams en el objeto req.

#### ¿Cuál es la responsabilidad principal de los servicios?

a - Usualmente se encarga de conectarse con datos de terceros como una DB

b - Usualmente está toda la lógica de negocio y resuelve los casos de uso

c - Usualmente expone el servicio al cliente

La responsabilidad principal de los servicios es:

b Usualmente está toda la lógica de negocio y resuelve los casos de uso

Los servicios son componentes de software que tienen como objetivo encapsular la lógica de negocio y separarla de la lógica de presentación. Su responsabilidad principal es resolver los casos de uso del sistema, es decir, realizar las tareas necesarias para satisfacer las necesidades del usuario. Por lo tanto, suelen contener la mayor parte de la lógica de negocio de la aplicación.

Los servicios pueden ser consumidos por diferentes componentes de la aplicación, como controladores o componentes de vista, y pueden ser utilizados para acceder a datos de terceros como bases de datos o servicios web. Sin embargo, esta no es su responsabilidad principal.

La opción c, "Usualmente expone el servicio al cliente", es incorrecta, ya que los servicios no suelen ser expuestos directamente al cliente, sino que son utilizados por componentes de la aplicación que sí están expuestos al cliente.

#### ¿Cuál es la forma de asignarle el puerto en donde corre nuestra app con express?

a - app.port(8000)

b - app.listen(8000)

c - app.run(8000)

La forma de asignarle el puerto en donde corre nuestra aplicación con express es:

b app.listen(8000)

Para iniciar la aplicación en un puerto específico, se debe llamar al método listen() del objeto app de express, pasando como argumento el número de puerto en el que se desea iniciar la aplicación. Por ejemplo:

app.listen(8000, () => { console.log('Aplicación iniciada en el puerto 8000'); });

Las opciones a y c son incorrectas, ya que no existen los métodos port() ni run() en el objeto app de express.

#### ¿Cuál es el middleware de express que me permite recibir la información de POST en formato json?

a - app.use(JSON.parse())

b - app.use(express.json())

c - app.use(express.jsonApply())

El middleware de express que permite recibir la información de POST en formato json es:

b app.use(express.json())

Para poder procesar los datos enviados en una solicitud POST en formato json, es necesario utilizar un middleware que se encargue de parsear esos datos y colocarlos en un formato accesible para nuestra aplicación. En express, este middleware se conoce como express.json().

Para utilizarlo, se debe agregar a la aplicación mediante el método use() de la siguiente manera:

app.use(express.json());

Luego, se pueden acceder a los datos enviados en la solicitud a través del atributo body del objeto request. Por ejemplo, si se envía una solicitud POST con el siguiente cuerpo:

{"name": "John", "age": 30}

Se pueden acceder a estos datos de la siguiente manera:

app.post('/users', (req, res) => { const name = req.body.name; const age = req.body.age; // ... });

Las opciones a y c son incorrectas, ya que JSON.parse() es una función que se utiliza para parsear una cadena de texto en formato json, y express.jsonApply() no es un método válido en express.

#### ¿Cuál la manera de  correcta obtener el parámetro productId enviado desde una ruta con GET?

a - const { productId } = req.params;

b - const productId = req.param(' productId ');

c - const productId = req.get(' productId ');

La manera correcta de obtener el parámetro productId enviado desde una ruta con GET es:

a const { productId } = req.params;

Los parámetros de ruta son aquellos que se envían como parte de la URL y se usan para identificar de manera única a un recurso. En express, estos parámetros se pueden acceder a través del objeto req (request) y del atributo params. Por ejemplo, si la ruta es "GET /products/:productId", se puede acceder al parámetro productId de la siguiente manera:

app.get('/products/:productId', (req, res) => { const productId = req.params.productId; // ... });

También es posible destruir el objeto params en una sola línea de código, como se muestra en la opción a.

Las opciones b y c son incorrectas, ya que no existen los métodos param() ni get() en el objeto req.

#### ¿Cuál es la forma correcta enviar un error de tipo 404 con una respuesta tipo json?

a - res.status(404).json({ message })

b - res.httpStatus(404).json({ message })

c - res.statusCode(404).json({ message })

La forma correcta de enviar un error de tipo 404 con una respuesta tipo json es:

a res.status(404).json({ message })

Para enviar un error de tipo 404 (Not Found) con una respuesta tipo json, se debe utilizar el método status() del objeto res (response) y pasar como argumento el código de estado 404. Luego, se debe utilizar el método json() para enviar el cuerpo de la respuesta en formato json. Por ejemplo:

app.get('/products/:productId', (req, res) => { const productId = req.params.productId;

// Si no se encuentra el producto, se envía un error 404 if (!findProductById(productId)) { res.status(404).json({ message: 'Product not found' }); } else { // ... } });

Las opciones b y c son incorrectas, ya que no existen los métodos httpStatus() ni statusCode() en el objeto res.

#### ¿Cuál es el objetivo de la librería Boom?

a - Validación de datos por medio de un schema

b - Manejo de errores http

c - Llevar un log de los errores.

El objetivo de la librería Boom es:

b Manejo de errores http

Boom es una librería de utilidades para el manejo de errores http en aplicaciones Node.js. Proporciona una serie de funciones que permiten crear y personalizar errores http de manera sencilla y uniforme. Estos errores se pueden enviar al cliente mediante una respuesta http y pueden ser utilizados para informar de problemas como una URL no encontrada (error 404) o una falta de autorización (error 401).

Boom proporciona una serie de funciones para crear errores http de diferentes tipos, como boom.badRequest() para errores 400 (Bad Request) o boom.unauthorized() para errores 401 (Unauthorized). También permite personalizar el mensaje y otros detalles del error para adaptarlos a las necesidades de la aplicación.

Las opciones a y c son incorrectas, ya que Boom no se utiliza para la validación de datos ni para llevar un log de los errores.

#### ¿Cuál es la manera de  correcta de declarar una ruta que reciba un parámetro llamado productId?

a - app.get('/products/*productId',  ...)

b - app.get(’/products/``<productid>``’, …)

c - app.get('/products/:productId',  ...)

La manera correcta de declarar una ruta que reciba un parámetro llamado productId es:

**c** app.get('/products/:productId', ...)

En express, se pueden incluir parámetros en las rutas utilizando el signo dos puntos (:) seguido del nombre del parámetro. Por ejemplo, para declarar una ruta que reciba un parámetro llamado productId, se debe escribir de la siguiente manera:

app.get('/products/:productId', (req, res) => { // ... });

Los parámetros de ruta se pueden acceder a través del objeto req (request) y del atributo params. Por ejemplo, para obtener el valor del parámetro productId se puede hacer de la siguiente manera:

const productId = req.params.productId;

Las opciones a y b son incorrectas, ya que no son sintaxis válida para declarar parámetros de ruta en express.

#### ¿Cuál es el objetivo del archivo Procfile de Heroku? 

a - En este archivo ejecutamos un script para correr pruebas. 

b - En este archivo ejecutamos un script para hacer build. 

c - En este archivo ejecutamos un script para correr la app en prod.

El objetivo del archivo Procfile de Heroku es:

c En este archivo ejecutamos un script para correr la app en prod.

El archivo Procfile es un archivo de texto plano que se utiliza para indicar a Heroku cómo ejecutar la aplicación. Se debe colocar en la raíz del repositorio de la aplicación y debe contener una única línea de texto que indique qué comando ejecutar para iniciar la aplicación.

Por ejemplo, si la aplicación se ejecuta mediante el comando "node index.js", el Procfile debe contener la siguiente línea:

web: node index.js

Heroku utiliza el Procfile para determinar cómo iniciar la aplicación en producción, por lo que es importante que esté presente y contenga el comando correcto.

La opción a, "En este archivo ejecutamos un script para correr pruebas", es incorrecta, ya que el Procfile no se utiliza para ejecutar pruebas. La opción b, "En este archivo ejecutamos un script para hacer build", también es incorrecta, ya que el archivo Procfile no se utiliza para hacer build de la aplicación.

#### ¿Cuál es propósito de instalar nodemon?

a - Nos funciona para hacer livereload cada que hagamos cambios en archivos js

b - Examina las buenas prácticas de código y formato

c - Es un paquete que nos ayuda a controlar los datos de entrada

El propósito de instalar nodemon es:

a Nos funciona para hacer livereload cada que hagamos cambios en archivos js

nodemon es una herramienta que se utiliza para hacer que el proceso de desarrollo de aplicaciones Node.js sea más cómodo. Funciona escuchando los cambios en los archivos del proyecto y reiniciando el servidor cada vez que se producen cambios. De esta manera, se evita tener que detener y volver a iniciar manualmente el servidor cada vez que se realizan cambios en el código.

Para utilizar nodemon, se debe instalar como un paquete de desarrollo y luego configurar el comando de inicio de la aplicación para que use nodemon en lugar de node. Por ejemplo, en lugar de ejecutar "node index.js" para iniciar la aplicación, se debe ejecutar "nodemon index.js".

Las opciones b y c son incorrectas, ya que nodemon no se utiliza para examinar las buenas prácticas de código ni para controlar los datos de entrada.

#### ¿Si una solicitud sale desde el mismo origen, hay problema de CORS?

a - Verdadero

b - Falso

Falso

El origen de una solicitud se refiere al dominio, esquema y puerto desde donde se envía la solicitud. Si una solicitud sale desde el mismo origen que el servidor al que se envía, no hay problema de CORS (Cross-Origin Resource Sharing).

El problema de CORS ocurre cuando una solicitud es enviada desde un origen diferente al del servidor al que se envía. En este caso, el navegador envía una solicitud de tipo "preflight" para verificar si el servidor permite que la solicitud sea enviada. Si el servidor no permite el acceso desde el origen especificado, se envía un error de tipo CORS.

Para evitar problemas de CORS, es necesario que el servidor permita el acceso desde los orígenes que se deseen, mediante la configuración de cabeceras HTTP como "Access-Control-Allow-Origin". Sin embargo, si la solicitud se envía desde el mismo origen que el servidor, no hay problema de CORS.