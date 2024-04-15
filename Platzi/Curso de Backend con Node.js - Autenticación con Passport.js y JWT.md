#### ¿Cuál es el método para verificar un JWT?

a - jwt.check(token, 'my-secret');

b - jwt.isValid(token, 'my-secret');

c - jwt.verify(token, 'my-secret');

La respuesta correcta es c:

```js
jwt.verify(token, 'my-secret');
```

El método `verify` es el método utilizado para verificar un token JWT (JSON Web Token). Este método toma dos argumentos: el token y una clave secreta. La clave secreta es una cadena que se utiliza para firmar el token y que se conoce tanto por el emisor del token como por el receptor. Al verificar el token, se asegura de que el token ha sido firmado correctamente y que no ha sido alterado durante la transmisión.

Es importante tener en cuenta que la verificación de un token JWT no garantiza la autenticación del usuario. Para autenticar al usuario, es necesario verificar el token y luego verificar la información de autenticación contenida en el cuerpo del token.

#### ¿Cuál es la forma correcta de obtener el atributo 'api' desde los headers de una petición?

<mark style="background: #FF5582A6;">a - req.get('api')</mark>

<mark style="background: #BBFABBA6;">b - req.headers``['api']``</mark>

<mark style="background: #FF5582A6;">c - req.headers.get('api')</mark>

La forma correcta de obtener el atributo 'api' de los headers de una petición es:

`req.headers['api']`

Los headers de una petición HTTP se envían junto con la solicitud y proporcionan información adicional sobre la solicitud y el cliente que la envía. Los headers se pueden utilizar para enviar información sobre el tipo de contenido que se está enviando o recibiendo, la autenticación del usuario, y otras características de la solicitud.

En Node.js, los headers de una petición se almacenan en el objeto `req.headers`, que es un objeto de clave-valor que contiene todos los headers de la solicitud. Para obtener un header específico, se puede acceder a él mediante su nombre como una propiedad del objeto `headers`, como se muestra en el ejemplo anterior.

La otra forma de obtener el atributo 'api' de los headers de una petición es utilizando el método `get` del objeto `req.headers`, como se muestra a continuación:

`req.headers.get('api')`

Ambos métodos son válidos y se pueden utilizar según sea necesario.

#### Si usamos Gmail para envío de correos, ¿cuál es la configuración correcta de host para Nodemail?

a - smtp.gmail.com

b - smtp-gmail.com

c - gmail.smtp.com

La respuesta correcta es a:

"`smtp.gmail.com`"

Gmail es un servicio de correo electrónico que se puede utilizar para enviar correos electrónicos a través de un cliente de correo o de una aplicación. Para utilizar Gmail con Nodemailer, una de las librerías más populares para enviar correos electrónicos en Node.js, se necesita configurar el host SMTP (Simple Mail Transfer Protocol) de Gmail.

La configuración correcta del host para Gmail es `smtp.gmail.com`. Este es el host que se utiliza para conectarse a los servidores de Gmail y enviar correos a través de ellos.

Para utilizar Gmail con Nodemailer, se necesitará también una cuenta de Gmail y las credenciales de la misma (dirección de correo y contraseña). Además, es posible que sea necesario habilitar la opción "Permitir el acceso de aplicaciones menos seguras" en la configuración de seguridad de la cuenta de Gmail.

Es importante tener en cuenta que para enviar correos a través de Gmail, es necesario cumplir con los términos de servicio de Gmail y con las leyes aplicables sobre el correo electrónico, como la Ley CAN-SPAM en Estados Unidos.

#### ¿Es posible saber el contenido de un JWT?

a - Falso

b - Verdadero

La respuesta correcta es b:

`Verdadero`

Un token JWT (JSON Web Token) es una cadena de texto que se utiliza para transmitir de manera segura información entre dos partes. Un JWT consta de tres partes separadas por dos puntos: el encabezado, el cuerpo y la firma.

El encabezado incluye información sobre cómo se ha firmado el token, como el algoritmo utilizado para firmarlo. El cuerpo incluye la información que se desea transmitir, como el ID del usuario o la expiración del token. La firma es una cadena cifrada que se utiliza para verificar la integridad del token y asegurar que no ha sido alterado durante la transmisión.

El cuerpo del token JWT está codificado en formato JSON y se puede descifrar para ver su contenido. Esto significa que es posible saber el contenido de un token JWT siempre y cuando se tenga la clave secreta utilizada para firmar el token y se utilice una herramienta adecuada para descifrarlo.

Es importante tener en cuenta que el contenido de un token JWT debe ser confiable y seguro, ya que puede ser utilizado para autenticar al usuario o para transmitir información confidencial. Por lo tanto, es importante proteger la clave secreta utilizada para firmar el token y utilizar un algoritmo seguro para firmar el token.

#### ¿Cuál es la capa que evalúa los permisos de un usuario?

a - Autenticación

b - Firma de token

c - Autorización

La respuesta correcta es c:

`Autorización`

La autorización es la capa de seguridad que evalúa los permisos de un usuario para determinar si tiene acceso a ciertos recursos o funcionalidades. La autorización se basa en la identidad del usuario y en los permisos que se le han asignado.

La autorización suele ir de la mano de la autenticación, que es la capa de seguridad que se encarga de verificar la identidad del usuario. Una vez que se ha autenticado al usuario, se puede evaluar qué acciones está autorizado a realizar.

Por ejemplo, si un usuario se autentica en un sistema utilizando un nombre de usuario y una contraseña, la autorización puede evaluar si el usuario tiene permisos para acceder a ciertas páginas o realizar ciertas acciones en el sistema.

Es importante tener en cuenta que la autorización no garantiza la seguridad de un sistema por sí sola. Es necesario implementar una serie de medidas de seguridad para proteger los datos y evitar accesos no autorizados.

#### ¿Cuál es la forma de aplicar el middleware de inicio de sesión dentro de una ruta?

a - router.post('/login', passport.middleware('local', {session: false}), () => {})

b - router.post('/login', passport.authenticate('local', {session: false}), () => {})

c - router.post('/login', passport.auth('local', {session: false}), () => {})

La respuesta correcta es b:

```js
router.post('/login', passport.authenticate('local', {session: false}), () => {})
```

Passport es una librería de autenticación para Node.js que se puede utilizar para autenticar a los usuarios en una aplicación web. Uno de los modos más comunes de utilizar Passport es a través de middlewares, que son funciones que se ejecutan en el medio de una solicitud HTTP.

Para aplicar el middleware de inicio de sesión de Passport a una ruta, se puede utilizar el método `authenticate` de Passport y pasarle como argumento el nombre del método de autenticación que se está utilizando (por ejemplo, "local" para autenticación local con nombre de usuario y contraseña) y un objeto de opciones.

Por ejemplo, para aplicar el middleware de inicio de sesión a una ruta que utiliza el método POST para iniciar sesión, se puede utilizar el siguiente código:

```js
router.post('/login', passport.authenticate('local', {session: false}), (req, res) => {
  // Código que se ejecuta después de la autenticación
});
```

Es importante tener en cuenta que el middleware de inicio de sesión de Passport no maneja la autorización, sino que simplemente verifica la identidad del usuario. Para evaluar los permisos del usuario, es necesario implementar una capa adicional de autorización.

#### ¿Cuál middleware de Passport.js funciona para hacer un inicio de sesión?

a - passport-local

b - passport-auth

c - passport-jwt

La respuesta correcta es a:

`passport-local`

Passport es una librería de autenticación para Node.js que se puede utilizar para autenticar a los usuarios en una aplicación web. Passport cuenta con una serie de módulos que se pueden utilizar para autenticar a los usuarios de diferentes maneras, como utilizando un nombre de usuario y una contraseña, un token JWT (JSON Web Token) o una cuenta de redes sociales.

Para autenticar a los usuarios utilizando un nombre de usuario y una contraseña, se puede utilizar el módulo `passport-local`. Este módulo proporciona un middleware que se puede utilizar para verificar las credenciales del usuario y autenticarlo en la aplicación.

Por ejemplo, para utilizar el middleware de inicio de sesión de `passport-local`, se puede utilizar el siguiente código:

```js
router.post('/login', passport.authenticate('local', {session: false}), (req, res) => {
  // Código que se ejecuta después de la autenticación
});
```

Es importante tener en cuenta que el middleware de inicio de sesión de `passport-local` no maneja la autorización, sino que simplemente verifica la identidad del usuario. Para evaluar los permisos del usuario, es necesario implementar una capa adicional de autorización.

#### ¿Por qué es importante hacer un hash de las contraseñas?

a - No es importante, ya que postgres debe brindar seguridad por defecto.

b - Para proteger a nuestros usuarios de cualquier ataque o filtración de datos en donde se exponga esa información.

c - Porque con esto evitamos al 100% ataques al sistema.

La respuesta correcta es b:

`Para proteger a nuestros usuarios de cualquier ataque o filtración de datos en donde se exponga esa información.`

Es importante hacer un hash de las contraseñas de los usuarios para proteger a los usuarios de cualquier ataque o filtración de datos en donde se exponga esa información. Al hacer un hash de la contraseña, se crea una versión cifrada de la misma que es difícil de descifrar. Esto significa que, incluso si los datos de la base de datos son expuestos, las contraseñas de los usuarios no podrán ser utilizadas directamente.

Además, el hash de las contraseñas también es útil para proteger a los usuarios de ataques de fuerza bruta, en los que se intenta adivinar la contraseña mediante el ensayo de diferentes combinaciones de caracteres. Al hacer un hash de la contraseña, es mucho más difícil para un atacante adivinar la contraseña original.

Es importante tener en cuenta que el hash de las contraseñas no es una medida infalible de seguridad y no garantiza la protección total de los datos. Es necesario implementar una serie de medidas de seguridad para proteger los datos y evitar accesos no autorizados.

#### ¿Cuál es la forma correcta de crear un hash usando bcrypt?

a - bcrypt.generate(myPlaintextPassword, saltRounds)

b - bcrypt.makeHash(myPlaintextPassword, saltRounds)

c - bcrypt.hash(myPlaintextPassword, saltRounds)

La respuesta correcta es c:

`bcrypt.hash(myPlaintextPassword, saltRounds)`

bcrypt es una librería de Node.js que se utiliza para crear hashes de contraseñas de manera segura. Para crear un hash de una contraseña utilizando bcrypt, se puede utilizar el método `hash`, que toma dos argumentos: la contraseña en texto plano y el número de rondas de sal.

La sal es una cadena aleatoria que se utiliza para agregar más complejidad al hash y hacerlo más difícil de romper. Al aumentar el número de rondas de sal, se aumenta la complejidad del hash y se hace más lento de calcular, lo que lo hace más seguro. Sin embargo, también hace más lento el proceso de crear el hash.

Por ejemplo, para crear un hash de la contraseña "myPassword" con 10 rondas de sal, se puede utilizar el siguiente código:

`const hash = bcrypt.hash('myPassword', 10);`

Es importante tener en cuenta que el hash de una contraseña no puede ser revertido para obtener la contraseña

#### ¿Cuál es el objetivo de instalar y usar Passport.js en la app?

a - Nos provee una serie de middlewares para manejar la capa de autenticación.

b - No provee una serie de middlewares para validar la integración de datos.

c - Nos provee una serie de middlewares para manejar la capa de autorización.

La respuesta correcta es a:

`Nos provee una serie de middlewares para manejar la capa de autenticación.`

Passport es una librería de autenticación para Node.js que se puede utilizar para autenticar a los usuarios en una aplicación web. Uno de los objetivos principales de Passport es proporcionar una serie de middlewares que se pueden utilizar para manejar la capa de autenticación de una aplicación.

Los middlewares son funciones que se ejecutan en el medio de una solicitud HTTP. Passport proporciona una serie de middlewares que se pueden utilizar para autenticar a los usuarios de diferentes maneras, como utilizando un nombre de usuario y una contraseña, un token JWT (JSON Web Token) o una cuenta de redes sociales.

Para instalar y utilizar Passport en una aplicación, es necesario instalar la librería y configurarla de acuerdo a las necesidades de la aplicación. Luego, se pueden utilizar los middlewares de Passport para proteger las rutas o funcionalidades que requieran autenticación.

Es importante tener en cuenta que Passport no maneja la autorización, sino que simplemente verifica la identidad del usuario.

#### ¿Cuál es la capa que evalúa si un usuario puede o no ingresar al sistema?

a - Autorización

b - Autenticación

c - Firma de token

La autenticación es la capa que evalúa si un usuario puede o no ingresar al sistema. La autenticación es el proceso de verificar la identidad de un usuario, a través de la solicitud y verificación de credenciales de inicio de sesión. Estas credenciales pueden ser un nombre de usuario y una contraseña, o una combinación de credenciales y tokens de autenticación.

La autorización es el proceso de determinar qué acciones y recursos están disponibles para un usuario autenticado. Una vez que se ha verificado la identidad del usuario a través del proceso de autenticación, la autorización determina qué acciones y recursos están disponibles para ese usuario. Por ejemplo, un usuario puede tener acceso de solo lectura a ciertos recursos, mientras que otro usuario puede tener acceso de lectura y escritura a los mismos recursos.

La firma de token es una técnica utilizada en la autenticación para verificar la integridad y autenticidad de un token de autenticación. Un token de autenticación es una cadena de caracteres que se utiliza para autenticar un usuario en un sistema. La firma de token utiliza una clave secreta compartida para generar una firma criptográfica del token, que luego se utiliza para verificar la integridad del token y garantizar que no ha sido modificado por un atacante.

#### ¿Cuál es la forma de aplicar el middleware que verifica el JWT para dar acceso o no a una ruta?

a - router.post('/create', passport.middleware('jwt', {session: false}), () => {})

b - router.post('/create', passport.authenticate('jwt', {session: false}), () => {})

c - router.post('/create', passport.auth('jwt', {session: false}), () => {})

La forma correcta de aplicar el middleware que verifica el JWT para dar acceso o no a una ruta es:

```js
router.post('/create', passport.authenticate('jwt', {session: false}), () => {})
```

Passport es una librería de autenticación para Node.js que proporciona un conjunto de middlewares para autenticar solicitudes HTTP. El método `authenticate` de Passport es un middleware que se utiliza para autenticar un usuario a través de un mecanismo de autenticación específico, como JWT (JSON Web Token).

El parámetro `'jwt'` especifica el nombre del mecanismo de autenticación que se está utilizando. El parámetro `{session: false}` indica que no se deben crear sesiones de usuario en el servidor. Esto es útil cuando se utiliza un token de autenticación en lugar de una sesión de usuario para autenticar al usuario.

En resumen, la línea de código `passport.authenticate('jwt', {session: false})` aplica el middleware de Passport que verifica el JWT y permite o deniega el acceso a la ruta `/create` en función de si el JWT es válido o no.

#### ¿Cuál middleware de Passport.js funciona verificar que cada ruta tenga un JWT válido?

a - passport-local

b - passport-auth

c - passport-jwt

El middleware que se utiliza en Passport.js para verificar que cada ruta tenga un JWT válido es `passport-jwt`. Este middleware es un plugin de Passport que se utiliza para autenticar solicitudes HTTP utilizando JWTs (JSON Web Tokens).

Para utilizar este middleware, primero se debe instalar la dependencia `passport-jwt` en el proyecto:

``npm install passport-jwt``

Luego, se debe configurar el middleware en el archivo de configuración de Passport:

```js
const JwtStrategy = require('passport-jwt').Strategy;
const ExtractJwt = require('passport-jwt').ExtractJwt;

const jwtOptions = {
  jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
  secretOrKey: process.env.SECRET
};

passport.use(new JwtStrategy(jwtOptions, (payload, done) => {
  User.findById(payload.id)
    .then((user) => {
      if (user) {
        done(null, user);
      } else {
        done(null, false);
      }
    })
    .catch((error) => {
      done(error, false);
    });
}));
```

Una vez configurado, se puede aplicar el middleware `passport-jwt` a cualquier ruta que desee proteger mediante el uso de un JWT válido. Por ejemplo:

```js
router.post('/create', passport.authenticate('jwt', {session: false}), (req, res) => {
  // Código de la ruta protegida por JWT
});
```

En este ejemplo, se aplica el middleware `passport.authenticate('jwt', {session: false})` a la ruta `/create`, lo que significa que solo se permitirá el acceso a esta ruta si se proporciona un JWT válido en la solicitud. Si no se proporciona un JWT válido o si el JWT es inválido, se denegará el acceso a la ruta.

#### El secret el JWT debe ser guardado dentro del código y no en una variable de ambiente.

a - Falso

b - Verdadero

Falso. Es recomendable guardar el secret del JWT en una variable de ambiente y no dentro del código.

Un JWT (JSON Web Token) es un token de autenticación que se utiliza para autenticar un usuario en un sistema. Un JWT está compuesto por tres partes: el header, el payload y la firma. El header incluye información sobre el tipo de token y el algoritmo utilizado para firmar el token. El payload incluye información sobre el usuario y otros datos, mientras que la firma es una cadena criptográfica que se utiliza para verificar la integridad del token.

Para crear una firma segura, se utiliza una clave secreta. Esta clave secreta se utiliza para firmar el JWT y luego para verificar la firma del JWT durante la autenticación. Es muy importante proteger la clave secreta, ya que si un atacante tiene acceso a ella, podría crear JWTs falsos y acceder a recursos protegidos de forma no autorizada.

Una forma de proteger la clave secreta es guardarla en una variable de ambiente en lugar de incluirla directamente en el código. Las variables de ambiente son valores que se establecen en el entorno de ejecución de una aplicación y se utilizan para configurar la aplicación de forma segura. Al guardar la clave secreta en una variable de ambiente, se evita que se exponga accidentalmente en el código fuente de la aplicación. Además, las variables de ambiente son más seguras que las variables de configuración hardcoded, ya que no se incluyen en el código fuente y son más difíciles de acceder para atacantes o personas no autorizadas.

#### ¿Cuál es el método para generar un JWT?

a - jwt.sign({...}, 'my-secret');

b - jwt.generate({...}, 'my-secret');

c - jwt.make({...}, 'my-secret');

Para generar un JWT (JSON Web Token), se utiliza el método `sign` del paquete `jsonwebtoken`. Este método toma dos argumentos: el primer argumento es el payload del JWT, que es un objeto que contiene información sobre el usuario y otros datos; el segundo argumento es la clave secreta utilizada para firmar el JWT.

Aquí hay un ejemplo de cómo utilizar el método `sign` para generar un JWT:

```js
const jwt = require('jsonwebtoken');

const payload = {
  userId: 123,
  username: 'john.doe'
};

const secret = 'my-secret';

const token = jwt.sign(payload, secret);
```

En este ejemplo, se utiliza el método `sign` para generar un JWT con un payload que incluye el ID del usuario y el nombre de usuario. La clave secreta se utiliza para firmar el JWT y garantizar su integridad. El método `sign` devuelve el JWT generado, que luego se puede enviar al cliente para su uso en futuras solicitudes.

Nota: Es importante proteger la clave secreta y no incluirla directamente en el código. Una forma de hacerlo es utilizar una variable de ambiente para almacenar la clave secreta y luego acceder a ella desde el código. Esto evitará que la clave secreta se exponga accidentalmente en el código fuente de la aplicación.