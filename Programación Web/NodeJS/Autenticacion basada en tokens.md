La **autenticación** basada en token es prominente en todas partes en la web hoy en día. Dado que la mayoría de las empresas web utilizan una API, los tokens son la mejor manera de manejar la autenticación para múltiples usuarios.

Hay algunos factores muy importantes al elegir la autenticación basada en token para su aplicación. Las principales razones de los tokens son:

-   Servidores sin estado y escalables
-   Aplicación móvil lista
-   Pasar autenticación a otras aplicaciones
-   Seguridad adicional

#### Autenticación basada en servidor (el método tradicional)

Dado que el protocolo HTTP no tiene estado, esto significa que si autenticamos a un usuario con un nombre de usuario y una contraseña, en la próxima solicitud, nuestra aplicación no sabrá quiénes somos. Tendríamos que autenticarnos de nuevo.

La forma tradicional de que nuestras aplicaciones recuerden quiénes somos es **almacenar la información de inicio de sesión del usuario en el servidor**. Esto se puede hacer de diferentes maneras en la sesión, generalmente en la memoria o almacenada en el disco.

Con la aparición de la web, las aplicaciones y el auge de las aplicaciones móviles, este método de autenticación ha mostrado **problemas**, especialmente en la escalabilidad.

##### Problemas
-   **Sesiones** : cada vez que se autentica un usuario, el servidor deberá crear un registro en algún lugar de nuestro servidor. Esto generalmente se hace en la memoria y cuando hay muchos usuarios que se autentican, la **sobrecarga** en su servidor aumenta.
-   **Escalabilidad** : dado que las sesiones se almacenan en la memoria, esto genera problemas de escalabilidad. A medida que nuestros proveedores de nube comiencen a replicar servidores para manejar la carga de aplicaciones, tener información vital en la memoria de la sesión limitará nuestra **capacidad de escalar**.
-   **CORS** : como queremos expandir nuestra aplicación para permitir que nuestros datos se usen en múltiples dispositivos móviles, tenemos que preocuparnos por el uso compartido de recursos de origen cruzado (CORS). Cuando usamos llamadas AJAX para obtener recursos de otro dominio (móvil a nuestro servidor API), podríamos tener problemas con **solicitudes prohibidas**.
-   **CSRF** : También tendremos protección contra [la falsificación de solicitudes entre sitios](http://en.wikipedia.org/wiki/Cross-site_request_forgery) (CSRF). Los usuarios son **susceptibles a los ataques CSRF** ya que ya pueden autenticarse con, por ejemplo, un sitio bancario y esto podría aprovecharse al visitar otros sitios.

#### Como funciona el token
La autenticación basada en token no tiene _estado_. No estamos almacenando **ninguna información sobre nuestro usuario** en el servidor o en una sesión.

Este concepto por sí solo soluciona muchos de los problemas de tener que almacenar información en el servidor.

Sin información de sesión significa que su aplicación puede escalar y agregar más máquinas según sea necesario sin preocuparse de dónde está conectado un usuario.

Aunque esta implementación puede variar, la esencia es la siguiente:

1.  Usuario Solicita Acceso con Nombre de Usuario / Contraseña
2.  La aplicación valida las credenciales
3.  La aplicación proporciona un token firmado al cliente
4.  El cliente almacena ese token y lo envía junto con cada solicitud
5.  El servidor verifica el token y responde con datos

Cada solicitud requerirá el token. Este token debe enviarse en el encabezado HTTP para mantener la idea de las solicitudes HTTP sin estado. También necesitaremos configurar nuestro servidor para que acepte solicitudes de todos los dominios usando `Access-Control-Allow-Origin: *`. Lo interesante de la designación `*`en el encabezado ACAO es que no permite solicitudes para proporcionar credenciales como autenticación HTTP, certificados SSL del lado del cliente o cookies.

Una vez que nos hemos autenticado con nuestra información y tenemos nuestro token, podemos hacer muchas cosas con este token.

Incluso podríamos crear un token basado en permisos y pasarlo a una aplicación de terceros (por ejemplo, una nueva aplicación móvil que queremos usar), y podrán tener acceso a nuestros datos, pero solo a la información que permitimos. con ese token específico.

#### Beneficios de los tokens

##### Sin estado y escalable

Los tokens se almacenan en el lado del cliente. Completamente sin estado y listo para ser escalado. Nuestros balanceadores de carga pueden pasar a un usuario a cualquiera de nuestros servidores ya que no hay información de estado o sesión en ninguna parte.

Si tuviéramos que mantener la información de sesión de un usuario que inició sesión, esto requeriría que sigamos enviando a ese usuario al _mismo servidor en el que inició sesión_ (llamado afinidad de sesión).

Esto trae problemas ya que algunos usuarios se verían obligados a usar el mismo servidor y esto podría generar un punto de tráfico pesado.

¡Aunque no te preocupes! Esos problemas desaparecen con los tokens, ya que el token en sí contiene los datos de ese usuario.

##### Seguridad

El token, no una cookie, se envía en cada solicitud y dado que no se envía ninguna cookie, esto ayuda a prevenir ataques CSRF. Incluso si su implementación específica almacena el token dentro de una cookie en el lado del cliente, la cookie es simplemente un mecanismo de almacenamiento en lugar de uno de autenticación. ¡No hay información basada en sesiones para manipular ya que no tenemos una sesión!

El token también caduca después de un período de tiempo determinado, por lo que se le pedirá al usuario que inicie sesión una vez más. Esto nos ayuda a mantenernos seguros. También existe el concepto de [revocación de token](https://tools.ietf.org/html/rfc7009) que nos permite invalidar un token específico e incluso un grupo de tokens en función de la misma concesión de autorización.

##### Extensibilidad (amigo de un amigo y permisos)

Los tokens nos permitirán construir aplicaciones que compartan permisos con otros. Por ejemplo, hemos vinculado cuentas sociales aleatorias a nuestras principales, como Facebook o Twitter.

Cuando iniciamos sesión en Twitter a través de un servicio (digamos Buffer), permitimos que Buffer publique en nuestro flujo de Twitter.

Mediante el uso de tokens, así es como proporcionamos permisos selectivos a aplicaciones de terceros. Incluso podríamos construir nuestra propia API y entregar tokens de permisos especiales si nuestros usuarios quisieran dar acceso a sus datos a otra aplicación.

##### Múltiples Plataformas y Dominios

Hablamos un poco sobre CORS antes. Cuando nuestra aplicación y servicio se expanda, necesitaremos brindar acceso a todo tipo de dispositivos y aplicaciones (¡ya que nuestra aplicación definitivamente se volverá popular!).

Al tener nuestra API solo para servir datos, también podemos elegir el diseño para servir activos desde una CDN. Esto elimina los problemas que genera CORS después de establecer una configuración de encabezado rápido para nuestra aplicación.

```js
Access-Control-Allow-Origin: *
```

Nuestros datos y recursos están disponibles para solicitudes de cualquier dominio siempre que el usuario tenga un token válido.

##### Basado en estándares

Al crear el token, tiene algunas opciones. Profundizaremos más en este tema cuando aseguremos una API en un artículo de seguimiento, pero el estándar a usar sería [JSON Web Tokens](https://www.digitalocean.com/community/tutorials/the-anatomy-of-a-json-web-token).

Este práctico gráfico de biblioteca y depurador muestra la compatibilidad con los tokens web JSON. Puede ver que tiene una gran cantidad de soporte en una variedad de idiomas. ¡Esto significa que en realidad podría cambiar su mecanismo de autenticación si decide hacerlo en el futuro!