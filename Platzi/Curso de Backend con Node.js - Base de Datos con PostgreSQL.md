#### ¿Cuáles son los métodos que nos ofrece sequelize para expresar una relación uno a muchos?

a - belongsToMany

b - hasMany y belongsTo

c - hasOne  y belongsTo

En Sequelize, hay varios métodos que se pueden utilizar para expresar una relación uno a muchos. Los métodos más comunes son:

a) belongsToMany: este método se utiliza para establecer una relación muchos a muchos entre dos modelos. Por ejemplo, si queremos establecer una relación entre los modelos de "Libro" y "Autor", podríamos utilizar el método belongsToMany para indicar que un libro puede tener varios autores y que un autor puede escribir varios libros.

b) hasMany y belongsTo: estos métodos se utilizan para establecer una relación uno a muchos entre dos modelos. Por ejemplo, si queremos establecer una relación entre los modelos de "Padre" y "Hijo", podríamos utilizar el método hasMany en el modelo "Padre" para indicar que un padre tiene muchos hijos, y el método belongsTo en el modelo "Hijo" para indicar que un hijo pertenece a un padre.

c) hasOne y belongsTo: estos métodos se utilizan para establecer una relación uno a uno entre dos modelos. Por ejemplo, si queremos establecer una relación entre los modelos de "Empleado" y "Departamento", podríamos utilizar el método hasOne en el modelo "Empleado" para indicar que un empleado tiene un solo departamento, y el método belongsTo en el modelo "Departamento" para indicar que un departamento tiene un solo empleado.

En resumen, para expresar una relación uno a muchos en Sequelize podemos utilizar los métodos hasMany y belongsTo o el método belongsToMany, dependiendo de si queremos establecer una relación uno a muchos o muchos a muchos, respectivamente.

#### ¿Cuál es el atributo que nos da Sequelize para obtener relaciones desde el método findAll?

a - models

b - relations

c - include

En Sequelize, el atributo "include" se utiliza para obtener relaciones al ejecutar el método findAll(). El atributo "include" es una opción que se pasa a findAll() y permite incluir otras tablas o modelos en la consulta de forma que se puedan obtener los datos de las relaciones junto con los datos de la tabla principal.

Por ejemplo, si tenemos una relación uno a muchos entre los modelos "Padre" y "Hijo", y queremos obtener todos los padres junto con sus hijos, podríamos utilizar el siguiente código:

````js
const padres = await Padre.findAll({
  include: [{
    model: Hijo
  }]
});
````

En este caso, el atributo "include" se utiliza para indicar que se desea incluir los datos del modelo "Hijo" en la consulta, lo que nos permitirá obtener los hijos de cada padre junto con sus datos.

En resumen, para obtener relaciones al utilizar el método findAll() en Sequelize debemos utilizar el atributo "include".

#### ¿SequelizeORM se puede conectar a MySql y Postgres o solo funciona para Postgres?

a - Funciona para ambos

b - Solo funciona para Postgres

SequelizeORM es una librería de mapeo objeto-relacional (ORM, por sus siglas en inglés) que permite trabajar con bases de datos de manera más sencilla y cómoda, sin tener que escribir consultas SQL directamente. SequelizeORM es compatible con una amplia variedad de bases de datos, incluyendo MySQL y Postgres. Por lo tanto, la respuesta correcta es:

a) Funciona para ambos

SequelizeORM es compatible con una amplia variedad de bases de datos, incluyendo MySQL y Postgres. Esto significa que podemos utilizar SequelizeORM para conectarnos a cualquiera de estos dos tipos de bases de datos y trabajar con ellas de manera más sencilla y cómoda.

Para conectarnos a una base de datos con SequelizeORM, debemos proporcionar los detalles de la conexión, como el nombre de la base de datos, el usuario y la contraseña, y especificar el tipo de base de datos que estamos utilizando. Por ejemplo, para conectarnos a una base de datos MySQL podríamos utilizar el siguiente código:

```js
const sequelize = new Sequelize('database', 'username', 'password', {
  dialect: 'mysql'
});
```

En este caso, estamos especificando que estamos utilizando una base de datos MySQL mediante el atributo "dialect". De esta manera, SequelizeORM sabrá cómo conectarse y trabajar con la base de datos.

En resumen, SequelizeORM es compatible con MySQL y Postgres, por lo que podemos utilizarlo para conectarnos y trabajar con cualquiera de estas dos bases de datos.

#### ¿Cuál es la funcionalidad de sequelize-cli ?

a - Scripts para correr y manejar migraciones

b - Scripts para correr unit tests

c - Scripts para correr el linter de Sequelize

sequelize-cli es una herramienta de línea de comandos (CLI, por sus siglas en inglés) que proporciona scripts para trabajar con SequelizeORM de manera más sencilla y cómoda. Algunas de las funcionalidades más comunes de sequelize-cli son:

a) Scripts para correr y manejar migraciones: sequelize-cli proporciona scripts para crear, aplicar y revertir migraciones de manera más sencilla. Las migraciones son archivos que contienen instrucciones para modificar la estructura de la base de datos, como crear o eliminar tablas o columnas. Con sequelize-cli podemos crear y aplicar estas migraciones de manera sencilla, lo que nos permite mantener la base de datos actualizada y sincronizada con el código de nuestra aplicación.

b) Scripts para generar modelos: sequelize-cli proporciona un script que nos permite generar modelos de manera sencilla. Los modelos son clases que representan tablas de la base de datos y nos permiten trabajar con ellas de manera más cómoda y sencilla. Con el script de sequelize-cli podemos generar modelos de manera rápida y sencilla, sin tener que escribir todo el código manualmente.

c) Scripts para generar seeders: sequelize-cli proporciona un script que nos permite generar seeders de manera sencilla. Los seeders son archivos que contienen datos de prueba que podemos utilizar para llenar la base de datos con información de prueba. Con el script de sequelize-cli podemos generar seeders de manera rápida y sencilla, lo que nos permite llenar la base de datos con datos de prueba de manera sencilla.

En resumen, sequelize-cli es una herramienta muy útil que nos proporciona scripts para trabajar con SequelizeORM de manera más sencilla y cómoda. Algunas de sus funcionalidades más comunes son: scripts para correr y manejar migraciones, scripts para generar modelos y scripts para generar seeders.

#### ¿Correr la forma de sync de Sequelize es recomendado para producción?

a - Falso

b - Verdadero

Es falso que sea recomendado correr la forma de sync de Sequelize en producción.

La forma de sync de Sequelize es un método que se utiliza para sincronizar el esquema de la base de datos con el modelo de Sequelize. Esto significa que sync comparará la estructura de la base de datos con el modelo de Sequelize y aplicará las modificaciones necesarias para que ambos estén sincronizados. Esto incluye crear o eliminar tablas o columnas, dependiendo de lo que se haya modificado en el modelo.

Aunque sync puede ser útil en etapas de desarrollo para asegurarnos de que la base de datos está sincronizada con el modelo de Sequelize, no es recomendado utilizarlo en producción. Esto se debe a que sync modificará directamente la estructura de la base de datos, lo que puede tener consecuencias indeseadas y potencialmente dañar la base de datos. Además, sync puede tardar un tiempo en ejecutarse y puede interrumpir el servicio mientras se está ejecutando, lo que puede afectar la disponibilidad de la aplicación.

Por lo tanto, en lugar de utilizar sync en producción, es mejor utilizar migraciones para modificar la estructura de la base de datos. Las migraciones son archivos que contienen instrucciones para modificar la estructura de la base de datos de manera controlada y segura. Al utilizar migraciones, podemos aplicar cambios a la base de datos de manera controlada y sin riesgo de dañarla.

En resumen, no es recomendado utilizar la forma de sync de Sequelize en producción debido a que puede tener consecuencias indeseadas y potencialmente dañar la base de datos. En lugar de utilizar sync, es mejor utilizar migraciones para modificar la estructura de la base de datos de manera controlada y segura.

#### ¿Cuál es la forma correcta de leer la variable de ambiente PORT con NodeJS?

a - proccess.PORT

**b - proccess.env.PORT**

c - proccess.get('PORT')

#### ¿Cuál es el método que nos ofrece queryInterface para agregar una columna?

a - queryInterface.addRow(...)  

**b - queryInterface.addColumn(...)**

c - queryInterface.pushColumn(...)

#### ¿Cuál es el puerto por defecto en el cual Mysql corre por defecto?

a - 8080

b - 3306

c - 5432

b 3306 es el puerto por defecto en el cual MySQL corre. Es el puerto en el que MySQL escucha las conexiones entrantes.

#### ¿Cuál es la forma de crear una entidad en la base de datos usando Sequelize?

a - models.MyModel.upsert(...)

b - models.MyModel.insert(...)

c - models.MyModel.create(...)

c models.MyModel.create(...) es la forma de crear una entidad en la base de datos usando Sequelize. Esta función recibe como argumento un objeto que representa la entidad a crear, y la guarda en la base de datos. Por ejemplo:

```js
const newEntity = {
  name: 'John',
  age: 30
};

models.MyModel.create(newEntity)
  .then(entity => {
    console.log('Entity created:', entity.get({ plain: true }));
  })
  .catch(error => {
    console.error('Error creating entity:', error);
  });
```

También puedes usar el método `build` para construir una instancia de la entidad en memoria sin guardarla en la base de datos, y luego usar el método `save` para guardarla en la base de datos.

```js
const newEntity = models.MyModel.build({
  name: 'John',
  age: 30
});

newEntity.save()
  .then(entity => {
    console.log('Entity created:', entity.get({ plain: true }));
  })
  .catch(error => {
    console.error('Error creating entity:', error);
  });
```

#### ¿Es una buena práctica manejar nuestra conexión con Postgres usando la estrategia de pooling?

a - Falso

b - Verdadero

b Verdadero. Es una buena práctica manejar la conexión con la base de datos usando la estrategia de pooling. Cuando se usa la estrategia de pooling, se crea un conjunto de conexiones disponibles para ser utilizadas por la aplicación. De esta manera, en lugar de crear una nueva conexión cada vez que se necesita realizar una consulta a la base de datos, la aplicación puede usar una de las conexiones disponibles del pool.

Esto tiene varias ventajas:

-   Ayuda a evitar la sobrecarga del servidor de base de datos al reducir la cantidad de conexiones que se deben manejar.
-   Ayuda a mejorar el rendimiento de la aplicación al reducir el tiempo de espera necesario para crear una nueva conexión cada vez que se necesita realizar una consulta.
-   Ayuda a mejorar la estabilidad de la aplicación al permitir que las conexiones se reutilicen en lugar de crear una nueva conexión para cada consulta.

Para usar la estrategia de pooling con Postgres, puedes usar el módulo `pg-pool`. Este módulo te permite crear un pool de conexiones y luego usar una de las conexiones disponibles para realizar consultas a la base de datos. Aquí tienes un ejemplo de cómo usar `pg-pool`:

```js
const { Pool } = require('pg-pool');

const pool = new Pool({
  user: 'myuser',
  host: 'localhost',
  database: 'mydatabase',
  password: 'mypassword',
  port: 5432
});

pool.query('SELECT * FROM users WHERE id = $1', [1], (error, result) => {
  if (error) {
    console.error('Error executing query:', error);
  } else {
    console.log('Result:', result.rows);
  }
});
```

Una vez que hayas terminado de usar el pool, debes cerrarlo para liberar los recursos:

```js
pool.end(() => {
  console.log('Pool closed');
});
```

#### ¿Cuál es la forma en que podemos hacer paginación usando Sequelize?

a - models.MyModel.findAll({ limit, offset })

b - models.MyModel.findAll({ skip, limit })

c - models.MyModel.findAll({ page })

a models.MyModel.findAll({ limit, offset }) es una forma de hacer paginación usando Sequelize. La opción `limit` indica el número máximo de resultados que se deben obtener, mientras que la opción `offset` indica a partir de qué resultado se deben obtener los resultados. Por ejemplo, si quieres obtener los resultados de la segunda página de un conjunto de resultados con 10 resultados por página, puedes usar:

```js
models.MyModel.findAll({
  limit: 10,
  offset: 10
})
  .then(results => {
    console.log('Results:', results);
  })
  .catch(error => {
    console.error('Error getting results:', error);
  });
```

También puedes usar el método `findAndCountAll` para obtener tanto los resultados como el número total de resultados disponibles. Esto puede ser útil para mostrar información sobre el número total de páginas y el número de resultados disponibles. Por ejemplo:

```js
models.MyModel.findAndCountAll({
  limit: 10,
  offset: 10
})
  .then(result => {
    console.log('Results:', result.rows);
    console.log('Total count:', result.count);
  })
  .catch(error => {
    console.error('Error getting results:', error);
  });
```

Otra forma de hacer paginación es usar el método `findAll` junto con la función `LIMIT` y `OFFSET` de SQL directamente en la consulta. Por ejemplo:

```js
models.MyModel.findAll({
  where: {
    // ...
  },
  limit: 10,
  offset: 10,
  order: [['createdAt', 'DESC']]
})
  .then(results => {
    console.log('Results:', results);
  })
  .catch(error => {
    console.error('Error getting results:', error);
  });
```

#### ¿Cuál es la forma de obtener una entidad de la base de datos con base a la PK?

a - models.MyModel.findOne(myId)

b - models.MyModel.getByPk(myId)

c - models.MyModel.findByPk(myId)

La forma correcta de obtener una entidad de la base de datos con base en su clave principal (PK) es utilizando el método `findByPk` de la clase `Model` del ORM (Object-Relational Mapping) que estés utilizando.

Por ejemplo, si estás utilizando el ORM Sequelize con un modelo llamado `MyModel`, puedes hacer lo siguiente para obtener una entidad con base en su PK:

```js
const entity = await models.MyModel.findByPk(myId);
```

Esto devolverá un objeto que representa la entidad con la PK especificada, o `null` si no se encuentra ninguna entidad con esa PK.

Otras opciones que mencionaste, como `findOne` y `getByPk`, no son métodos estándar de los ORMs y pueden variar dependiendo del ORM que estés utilizando.

#### ¿Cuál es comando que usamos para levantar el contendedor de Postgres con Docker?

a - docker-compose up -d postgres

b - docker-compose run -d postgres

c - docker-compose deploy -d postgres

Para levantar un contenedor de Postgres con Docker, puedes utilizar el comando `docker-compose up`, que iniciará los contenedores especificados en el archivo `docker-compose.yml` de tu proyecto.

Para levantar el contenedor de Postgres en particular, puedes utilizar el siguiente comando:

```docker
docker-compose up -d postgres
```

Este comando levantará el contenedor de Postgres en segundo plano (background), lo que significa que el proceso se ejecutará en segundo plano y no bloqueará la consola. Si quieres ver la salida del proceso en tiempo real, puedes eliminar la opción `-d` y ejecutar el comando sin ella.

Otras opciones que mencionaste, como `docker-compose run` y `docker-compose deploy`, no son relevantes para levantar un contenedor de Postgres con Docker y no funcionarían de la misma manera.

#### ¿Cuál es la forma de eliminar una entidad de la base de datos con base a la PK?

a - const model = await models.MyModel.findByPk(myId) await model.destroy();

b - const model = await models.MyModel.findByPk(myId) await model.remove();

c - const model = await models.MyModel.findByPk(myId) await model.delete();

La forma correcta de eliminar una entidad de la base de datos con base en su clave principal (PK) es utilizando el método `destroy` de la clase `Model` del ORM (Object-Relational Mapping) que estés utilizando.

Por ejemplo, si estás utilizando el ORM Sequelize con un modelo llamado `MyModel`, puedes hacer lo siguiente para eliminar una entidad con base en su PK:

```js
const model = await models.MyModel.findByPk(myId);
await model.destroy();
```

Este código buscará la entidad con la PK especificada y luego la eliminará de la base de datos.

Otras opciones que mencionaste, como `remove` y `delete`, no son métodos estándar de los ORMs y pueden variar dependiendo del ORM que estés utilizando.

#### ¿Cuáles son los métodos que nos ofrece sequelize para expresar una relación uno a uno?

a - belongsToMany

b - hasMany  y belongsTo

c - hasOne  y belongsTo

En Sequelize, existen varios métodos que puedes utilizar para expresar distintas relaciones entre entidades en una base de datos. Algunos de estos métodos son:

-   `hasOne`: Este método se utiliza para expresar una relación uno a uno desde el modelo al que se aplica hacia otro modelo. Por ejemplo, si tienes un modelo de usuarios y quieres asociarle un perfil a cada usuario, puedes utilizar `hasOne` para definir la relación.
    
-   `belongsTo`: Este método se utiliza para expresar una relación uno a uno desde el modelo al que se aplica hacia otro modelo, pero desde el punto de vista inverso al de `hasOne`. Por ejemplo, si tienes un modelo de perfiles y quieres asociarle un usuario a cada perfil, puedes utilizar `belongsTo` para definir la relación.
    

Por lo tanto, la respuesta correcta a la pregunta sería:

c hasOne y belongsTo

Otros métodos que mencionaste, como `belongsToMany`, se utilizan para expresar relaciones muchos a muchos entre dos modelos.

#### ¿Cuál es la forma de definir un campo como Integer con Sequelize?

a - DataTypes.NUMBER

b - DataTypes.INTEGER

c - DataTypes.DATE

Para definir un campo como `INTEGER` (entero) en Sequelize, debes utilizar el tipo de datos `INTEGER` del módulo `DataTypes`.

Por ejemplo, si quieres definir un campo `age` como entero en un modelo de Sequelize, puedes hacer lo siguiente:

```js
module.exports = (sequelize, DataTypes) => {
  const MyModel = sequelize.define('MyModel', {
    age: {
      type: DataTypes.INTEGER,
      allowNull: false
    }
  });

  return MyModel;
};
```

La respuesta correcta a la pregunta sería:

b DataTypes.INTEGER

Otras opciones que mencionaste, como `DataTypes.NUMBER` y `DataTypes.DATE`, no son tipos de datos que sean relevantes para definir un campo como entero en Sequelize.