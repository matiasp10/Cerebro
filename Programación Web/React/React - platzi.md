**Instalamos** webpack para el bundle de la app, y _babel_ para que el código sirva en cualquier navegador

```bash
npm install @babel/core @babel/preset-env @babel/preset-react 
npm install webpack webpack-cli webpack-dev-server 
npm install babel-loader html-loader html-webpack-plugin
```

> Es buena práctica al momento de trabajar con npm, añadir el _flag "_-D" como dependencia de desarrollo

_babel core ⇒ núcleo de babel_

_babel/preset-env ⇒ para que javascript y las nuevas funcionalidades funcionen en cualquier navegador_

_babel/preset-react ⇒ para que react funcione en cualquier navegador_

_webpack y webpack-cli ⇒ bundler del proyecto_

_webpack-dev-server ⇒ inicializar un servidor en local para mostrar en modo producción o desarrollo nuestra aplicación_

_loaders y plugin ⇒ sirven para optimizar o extraer html de los archivos (i.e React)_

**Archivos de configuración**

```jsx
node_modules
// .gitignore
```

```jsx
{
    "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
    ]
}
//.babelrc
```

```jsx
const path = require('path'); //path del proyecto principal
const HtmlWebpackPlugin = require('html-webpack-plugin'); //traemos el plugin
//de html

module.exports = {
    entry: './src/index.js', // punto de entrada
    output: { // lugar al que saldrán todos los archivos
        path: path.resolve(__dirname, 'dist'), //en nuestro path, crea la carpeta dist
        filename: 'bundle.js' // nombre del archivo js resultante
    },
    resolve: { // extensión de archivos a tomar en cuenta
        extensions: ['.js', '.jsx']
    },
    module: { // loaders para cada tipo de archivo
        rules: [ // reglas para usar
            {
                test: /\.(js|jsx)$/, // extensiones en las cuales actuará babel
                exclude: /node_modules/, // siempre excluir node modules 
                use: { // indicamos el loader
                    loader: 'babel-loader' // babel 
                }
            },
            {
                test: /\.html$/, // extensiones html
                use: [
                    {
                        loader: 'html-loader' // loader a usar
                    }
                ]
            }
        ]
    },
    plugins: [ // plugins 
        new HtmlWebpackPlugin({ // instanciamos el plugin para html 
            template: './public/index.html', // archivo raíz a transformar
            filename: './index.html' // el archivo resultante
        })
    ]
}
```

Pero antes les dejo por aqui unos enlaces para que puedan leer y solucionar posibles problemas con que se puedan topar referentes a esta clase :  
[sass-loader doc](https://webpack.js.org/loaders/sass-loader/#root)

```
{
        test: /\.s[ac]ss$/i,
        use: [
          // Creates `style` nodes from JS strings
          "style-loader",
          // Translates CSS into CommonJS
          "css-loader",
          // Compiles Sass to CSS
          "sass-loader",
        ],
 },
```

.  
El esquema correcto para configurar DevServer es el siguiente:

```
devServer: {
    static: {
      directory: path.join(__dirname, 'public'),
    },
    compress: true,
    port: 9000,
},
```

Por eso el error en el minuto 9:40.  
En el minuto 10:18 se ve que hay un corte en el video y Oscar ya ha borrado la configuracion de DevServer.

Si quieren leer un poco mas les dejo la documentacion oficial:  
[DevServer Doc](https://webpack.js.org/configuration/dev-server/#root)

.  
**Ahora si, los consejos:**

-   Este tipo de configuraciones las hacemos unicamente en proyectos que sean MUY personalizados o bien en proyectos personales donde estemos aprendiendo a utilizar dichas herramientas.
-   En el mundo laboral, (dependiendo de la empresa) la mayoria de organizaciones necesitan entregar productos rapido, y que sean funcionales.
-   Algunas empresas por ejm, en entrevistas tendran que hacer una prueba tecnica, y probablemente esa prueba sea un ejercicio practico live coding.
-   A lo que quiero llegar con esto es que si llegan a tener una prueba tecnica similar con tiempo limitado, no cometan el error de ponerse a hacer estilos con css puro o sass, y configuraciones desde cero existiendo herramientas para ello. (Por supuesto esto depende del proyecto).
-   Ultimamente **create-react-app** ha dejado de obtener un buen soporte y lanza muchos WARNINGS, en su lugar tambien existe **Vite** que personalmente me gusta mucho mas ya que es mas rapida y facil.
-   Para estilos, si ya tenemos buenas bases de CSS podemos aprender al menos 3 frameworks, yo recomendaria TailwindCSS, este tiene muy buen soporte para configurarlo ya sea con create-react-app o con Vite y su doc es muy limpia y entendible, pero tambien existen otros como MaterialUI, etc.
-   Las herramientas existen para facilitarnos la vida, asi que usemoslas 🤗.

**React con Css y Sass**

**Instalaremos** algunos loaders y plugins para que nuestro proyecto pueda funcionar con estilos de css y sass

```bash
npm instal mini-css-extract-plugin css-loader style-loader sass sass-loader -D
// en el video, faltaba solamente el loader de sass por los que nos dio un error
```

```jsx
// como siempre, cada vez que instalamos dichas dependencias, en webpack debemos 
// indicar reglas y los plugins

module.exports = {
	...
		module: {
			rules: [
				...
				{
	         test: /\.s[ac]ss$/i,
           use: [
               "style-loader",
               "css-loader",
               "sass-loader"
	        ]
        }
				...
			]
		}
	...,
	plugins: [
		...
		new MiniCssExtractPlugin({
			filename: '[name].css'
    })
		...
	],
	devServer: {
        allowedHosts: path.join(__dirname, 'dist'), // contentBase corresponde a webpack 4
// ahora en Webpack 5 se usa allowedHosts
// créditos al compañero Fabian Rivera Restrepo
        port: 3005,
        compress: true,
    }
}
```

```scss
// creamos la carpeta styles dentro de src
// en styles, creamos el archivo global.scss

$base-color: #ff0000;
$color: rgb(black, 0.88);

body {
    background-color: $base-color;
    color: $color;
}
```

```jsx
// en App.jsx, importamos los estilos de scss
import '../styles/global.scss';
```

```bash
// ahora si podemos compilar otra vez nuestra app
npm run build
```

###### Ya tienes tu loader de Babel instalado y conectado con Webpack. ¿Dónde defines los presets con los que vas a trabajar?

a webpack.config.js

b **.babelrc**

c .gitignore

d package.json

###### ¿Cuál es el archivo de configuración donde definimos los loaders con los que trabajaremos cada distinto tipo de archivo en nuestro proyecto?

a **webpack.config.js**

b .babelrc

c .gitignore

d package.json

###### ¿Cuál es el loader de Webpack necesario para trabajar con código JavaScript interpretado por Babel?

a **babel-loader**

b @babel/preset-env

c @babel/core

d @babel/preset-react

e webpack-cli

###### ¿Cuál es el comando correcto para trabajar con la versión 17 de React y React DOM.

a Trabajar con la versión 17 de React.js es una mala práctica.

b npm install React ReactDOM --save

c npm install react react-dom --save

d **npm install react@17 react-dom@17 --save**

###### ¿Cuál es el comando correcto para instalar la última versión de React y React DOM.

a npm install react@18 react-dom@18 --save

b npm install React ReactDOM --save

c npm install react@17 react-dom@17 --save

d **npm install react react-dom --save**

#### ¿Qué es router en React?

Debido a que React es de tipo SPA(single page application), no recarga la página cuando cambiamos de url. Sin embargo, router nos ayuda a crear otra página para poder navegar en nuestra aplicación. Imagina twitter web, cuando das click en un tweet, se abre otra sección donde puedes ver el tweet. _Sería un problema que al momento de darle click, no cambie la url, por lo que ese tweet no tiene dirección propia, no se guardaría en tu historial y sería un problema el SEO._ Para ello, usamos router, que se encargará de administrar esta situación, donde en el momento que abras el tweet, cambie la URL, pero todavía mantenga ese dinamismo y rapidez de una SPA.

#### ¿Entonces qué es ReactRouterDOM?

```bash
#Para instalar
npm install react-router-dom
```

```jsx
//import en App.jsx
import { BrowserRouter, Switch, Route } from 'react-router-dom';
// usaremos esas 3 herramientas
```

**ReactRouterDOM** te permite implementar enrutado dinámico en la aplicación. Nos facilita pues podemos enrutar nuestra app basada en componentes de la app (como login o recoverypassword).

```jsx
const App = () => {
    return (
        <BrowserRouter>
            <Switch>
                <Layout>
                    <Route exact path="/" component={Home} />
                    <Route exact path="/login" component={Login} />
                    <Route exact path="recovery-password" component={Recoverypassword} />
                    <Route component={NotFound} />
                </Layout>
            </Switch>
        </BrowserRouter>
    );
}
```

#### ¿Qué estamos haciendo?

**BrowserRoute** sirve para implementar _router_ en el navegador

**Switch** regresa la primera ruta que coincida. En pocas palabras, si estamos en _[www.platzi.com/contacto](https://platzi.com/clases/2484-react-practico/42074-react-router-dom/platzi.com/contacto)_ , regresará el componente que coincida a este (es decir, el componente que contenga la lógica de contacto). En esta caso, estamos poniendo varios _routes dentro de switch, ¿para qué?_ para que solamente traiga esa misma ruta, y no tenga que buscar más. Como si fuese un condicional switch de javascript efectivamente. Y por ello tenemos un route sin path, que será el valor por defecto.

**Layout** solamente renderizará el route que coincida efectivamente con la URL especificada.

**Header para todas nuestras páginas**

**Primero**, seleccionemos el html del proyecto anterior y construyamos un componente.

```jsx
// Header.jsx
import React from 'react';
import '../styles/Header.scss'

const Header = () => {
    return (
        <nav>
            <img src="./icons/icon_menu.svg" alt="menu" className="menu" />
            <div className="navbar-left">
                <img src="./logos/logo_yard_sale.svg" alt="logo" className="logo" />
                <ul>
                    <li>
                        <a href="/">All</a>
                    </li>
                    <li>
                        <a href="/">Clothes</a>
                    </li>
                    <li>
                        <a href="/">Electronics</a>
                    </li>
                    <li>
                        <a href="/">Furnitures</a>
                    </li>
                    <li>
                        <a href="/">Toys</a>
                    </li>
                    <li>
                        <a href="/">Others</a>
                    </li>
                </ul>
            </div>
            <div className="navbar-right">
                <ul>
                    <li className="navbar-email">platzi@example.com</li>
                    <li className="navbar-shopping-cart">
                        <img src="./icons/icon_shopping_cart.svg" alt="shopping cart" />
                        <div>2</div>
                    </li>
                </ul>
            </div>
        </nav>
    );
}

export default Header;
```

> Recordemos que debemos cambiar class del html por className, para evitar problemas.

**Segundo**, traigamos el css, y creamos el archivo scss.

```scss
// Header.scss
nav {
    display: flex;
    justify-content: space-between;
    padding: 0 24px;
    border-bottom: 1px solid var(--very-light-pink);
}
.menu {
    display: none;
}
.logo {
    width: 100px;
}
.navbar-left ul,
.navbar-right ul {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    align-items: center;
    height: 60px;
}
.navbar-left {
    display: flex;
}
.navbar-left ul {
    margin-left: 12px;
}
.navbar-left ul li a,
.navbar-right ul li a {
    text-decoration: none;
    color: var(--very-light-pink);
    border: 1px solid var(--white);
    padding: 8px;
    border-radius: 8px;
}
.navbar-left ul li a:hover,
.navbar-right ul li a:hover {
    border: 1px solid var(--hospital-green);
    color: var(--hospital-green);
}
.navbar-email {
    color: var(--very-light-pink);
    font-size: var(--sm);
    margin-right: 12px;
}
.navbar-shopping-cart {
    position: relative;
}
.navbar-shopping-cart div {
    width: 16px;
    height: 16px;
    background-color: var(--hospital-green);
    border-radius: 50%;
    font-size: var(--sm);
    font-weight: bold;
    position: absolute;
    top: -6px;
    right: -3px;
    display: flex;
    justify-content: center;
    align-items: center;
}
@media (max-width: 640px) {
    .menu {
    display: block;
    }
    .navbar-left ul {
    display: none;
    }
    .navbar-email {
    display: none;
    }
}
```

**Por último,** incorporemos dicho header en el home del proyecto.

```jsx
// Home.jsx
import React from 'react';
import Header from '../components/Header';

const Home = () => {
    return (
        <Header />
    );
}

export default Home;
```

Y listo, ya tenemos nuestro header en la página Home.

> _Reto: analizar todos los componentes, containers y páginas del proyecto para terminar toda la estructura final. Es importante que aprendamos a diferenciar cada uno, pues nuestro objetivo siempre será crear el código más reutlizable y fácil de mantener._

#### ¿Qué es atomic design?

![https://atomicdesign.bradfrost.com/images/content/atomic-design-process.png](https://atomicdesign.bradfrost.com/images/content/atomic-design-process.png)

Piensa en una aplicación. Identifica cada parte, navega por ella, cambia de sección. Te das cuenta? muchos componentes son muy parecidos. Conoce a atomic design, una metodología encargada en interfaces.

**Átomos**

Ahora necesito que recuerdes las clases de química. Sabrás que todo en el universo está compuesto por átomos. Este es nuestro primer nivel de abstracción. Cuando diseñes un UI, mira los botones, textos, imágenes o entradas de texto. Son las partes más fundamentales y pequeñas que usamos.

![https://atomicdesign.bradfrost.com/images/content/html-periodic-table.png](https://atomicdesign.bradfrost.com/images/content/html-periodic-table.png)

La **imágen** de arriba te ayudará a identificar que cosas pueden tomarse como átomos en tu próxima aplicación.

![https://atomicdesign.bradfrost.com/images/content/atoms-form-elements.png](https://atomicdesign.bradfrost.com/images/content/atoms-form-elements.png)

**Moléculas**

Las moléculas son una unión de átomos. Todas estas moléculas, normalmente tienen una función específica para la cuál necesitan varios átomos. Por ejemplo, la glucosa C6H12O6, es la energía en carbohidratos del humanos. Ahora, pasemos al diseño. En interfaces, una parte como un comentario de twitter, una sección de youtube de ME GUSTA y NO ME GUSTA, o el menú en los videos de platzi para avanzar o retroceder en la clase, son todos moléculas. Estas estás compuestas de algunos componentes más pequeños (como por ejemplo, de botón y cuadro de texto). Este es nuestro segundo nivel. Crear moléculas es simple, y recuerda que deberán tener una función única en nuestra UI

![https://atomicdesign.bradfrost.com/images/content/molecule-search-form.png](https://atomicdesign.bradfrost.com/images/content/molecule-search-form.png)

**Organismos**

Los organismos, ya son un nivel mucho más complejo. Los organismo están compuesto de muchas moléculas. Pero lo más interesante, es que tienen vida propia, y pueden interactuar en una manera muy amplia con otros organismos. Imagina una abeja con una flor, ambos colaboran de una u otra manera a que el otro esté bien. En nuestro diseño, imagina al header. El header está compuesto de muchos elementos, y tienen un impacto muy grande en la app. O incluso, de una sección como una tienda de ropa en la paǵina web. Seguramente te das cuenta, que estos tienen muchos artículos, y todos constan de una imaǵen, precio, y un ordenamiento. Puedes verlo así:

_Átomo⇒ imágen, precio, descripción_

_Molécula ⇒ el cuadro que contiene a la imágen, al precio y a la descripción._

_Organismo ⇒ todos los cuadros ordenados en forma de tabla._

El organismo si te das cuenta, puede usar moléculas del mismo tipo o diferentes. El punto clave, es que no trates de abarcar tanto, y que pertenecen a una sección claramente definida en nuestra app.

![https://atomicdesign.bradfrost.com/images/content/organism-header.png](https://atomicdesign.bradfrost.com/images/content/organism-header.png)

**Templates**

Los templates son prácticamente lo que vimos de Layouts. Es un poco más fácil de comprender. Es la plantilla en la cual siempre organizarás los organismos. Es decir, el esqueleto que indica donde irá por ejemplo, el Header, el footer, grid y sección de comentarios.

![https://atomicdesign.bradfrost.com/images/content/template.png](https://atomicdesign.bradfrost.com/images/content/template.png)

**Pages**

Finalmente tenemos a la constitución de nuestra app. Las pages son en sí, toda la página funcionando con contenido interactúando entre ellas.

![https://atomicdesign.bradfrost.com/images/content/page.png](https://atomicdesign.bradfrost.com/images/content/page.png)

> Una recomendación. No pienses en forma secuencial el atomic design. Es decir, no pienses ⇒ primero hago los átomos, después hago las moléculas, tercero los organismos… Según el mismo autor de atomic design, dependerá mucho de tu aplicación y de las necesidades que hay que cubrir. Más bien, es una manera mental de interpretar la UI

> No atribuyas atomic design como algo único de React o del desarrollo web ⇒ es un método de desarrollo de UI que se puede usar en cualquier interfaz.

Te recomiendo profundamente leer el siguiente link, del cual usé toda la referencia. Además, es del autor del Atomic Design.

[Atomic Design Methodology | Atomic Design by Brad Frost](https://atomicdesign.bradfrost.com/chapter-2/)

## Tipos de componentes en React: stateful vs. stateless

#### Clase 14/29

Este es un ejemplo para useState, podemos darle un valor inicial, el cual puede ser cambiado por un evento que se puede asignar a este mismo componente, o a otros componentes y hasta pasarlo por medio de un hijo para que éste cambie el inicial.

Para poder usar componentes stateful es necesario llamar useState desde React, la forma de importarlo y usarlo es la siguiente:

```jsx
import React, { useState } from 'react';

const Button = () => {
    const [name, setName] = useState('Hola Mundo'); 
    return (
        <div>
            <h1>{name}</h1>
        </div>
    );
}
```

Los componentes stateless servirán para pasar un estilo visual o props, pero no tendrá otra función más que esa.

Este sería un componente sin estado, stateless.

```jsx
import React from 'react';

const Button = ({ text }) => <ButtonRed text={text}/>;
```

También esta forma es válida:

```jsx
import React from 'react';

const Button = () => (
        <div>
            <h1>Hola mundo!</h1>
        </div>
);
```

Es por eso que hay que tener presente que NO todos los componentes deben de tener estado y muchos de ellos sólo llevarán información que presentar directamente al HTML con CSS, pero sí serán parte de todo lo que se está construyendo.

Los componentes Stateful y Stateless, son los componentes más utilizados hoy en día.

También hay otro tipos de componentes, que están compuestos por clases.

Aquí, tendremos una clase, con el nombre que queramos, que _extiende_ de React.Component

```jsx
import React from 'react';

class App extends React.Component {
    render() {
        return (
            <div>
                <h1>Hello world! </h1>
            </div>
        )
    }
}
```

Aunque, si importamos React Component, desde un inicio, podemos simplemente escribirlo de esta forma:

```jsx
import React , { Component } from 'react';

class App extends Component {
    render() {
        return (
            <div>
                <h1>Hello world! </h1>
            </div>
        )
    }
}
```

Este tipo de componentes trabajan con constructores, aunque ya no son tan usados, pues han sido reemplazados por la propuesta de React Hooks.

```jsx
import React , { Component } from 'react';

class App extends Component {

    constructor() {
        super();
        this.sate = {
            count: 0
        };
    }

    render() {
        return (
            <div>
                <h1>Hello world! </h1>
            </div>
        )
    }
}
```

Es importante conocer este tipo de componentes porque si en algún momento tenemos que dar mantenimiento a alguna página que fue construida hace unos años atrás, es muy posible que nos encontremos este tipo de componentes.

Los hooks, tienen una funcionalidad particular, pues reciben un componente, extienden su funcionalidad con lo que esté dentro del componente y retornan un componente compuesto. Así podemos tener funcionalidades muy específicas con las que podemos trabajar según nuestras necesidades.

Esta sería la sintaxis:

```jsx
import React , { Component } from 'react';

function ComponentWrapper(WrapperComponent) {
    class Wrapper extends Component {
        render () {
            return <WrapperComponent {...this.props} />;
        }
    }

    return Wrapper;
}
```

Más adelante aprenderemos más sobre React Context y cómo usarlo.

#### ¿Para qué sirven los alias en Webpack?

a **Para facilitar los imports cuando trabajamos con muchas carpetas (e.j. pasar de ../../styles/archivo.css a @styles/archivo.css).**

b Para que Webpack sepa con qué loader o plugin empaquetar nuestros archivos.

c Para facilitar los imports cuando trabajamos con muchas extensiones (e.j. pasar de ../../styles/archivo.css a ../../styles/archivo).

#### ¿Qué comando nos permite instalar la versión 5 de React Router DOM?

a **npm install react-router-dom@5 --save**

b npm install ReactRouterDOM@5 --save

c npm install ReactRouterDOM --save

d npm install react-router-dom --save

#### ¿Qué comando nos permite instalar la última versión de React Router DOM?

a **npm install react-router-dom --save**

b npm install ReactRouterDOM@5 --save

c npm install ReactRouterDOM --save

d npm install react-router-dom@5 --save

#### ¿Qué herramienta nos permite agregar rutas y navegación a aplicaciones con React.js?

a react-dom lo permite por defecto.

b **react-router-dom**

c react lo permite por defecto.

## **¿Cómo usar useState?**

useState es una manera de usar estado con los React Hooks. Recordemos que los estados son maneras en la que un componente puede administrar información cambiante en el entorno, y después de ser llamado se renderiza el React DOM de nuevo.

Para ello primero importamos useState de react

```jsx
import React, { useState } from 'react';
```

**Ahora**, useState será incorporado en nuestro componente ProductItem

```jsx
const ProductItem = () => {
	const [cart, setCart] = useState('Hola');

	const handleClick = () => {
		setCart('Hola mundo');
	}
}
```

Para poder usar los estados, primero debemos crear una constante en la cual tendrá un array. El primero elemento _en este caso cart_ será la variable a la cual le asignaremos un valor de estado. Este valor puede ser de cualquier tipo. En segundo lugar tenemos a setCart. Por convención siempre deberemos escribir esta “función” con set(Variable). Esta será la encargada de asignar un valor cualquiera a cart cada vez que exista algún evento. Esto lo igualamos a _useState_, que es como una manera de inicializar la variable cart. En segundo lugar tenemos a la función handleClick. **handleClick** es la función que dada un evento, _como un click,_ será llamada y por dentro usaremos a setCart para asignarle un nuevo estado a la variable cart. No podemos usar directamente setCart, pues puede dar algún error y no es la manera correcta. Por ello, después en el return, donde tenemos el html, lleva la siguiente estructura.

```jsx
<figure onClick={handleClick}>
		<img src={buttonAddCart} alt="" />
</figure>
```

Al momento de darle click en figure, llama a la función handleClick del componente, y handleClick por dentro cambiará el estado de la variable de estado por uno nuevo. En este caso, cambiamos el valor de cart de hola, por hola mundo.

**¿Cómo acceder a la variable?**

Para acceder a dicha variable cart en el html, podemos usar llaves en donde pasaremos el nombre. Esto es más fácil, pues de otra manera, tendremos que usar más array’s y acceder con el índice, el cual dificulta la lectura del código.

```jsx
<div className="product-info">
				<div>
					<p>$120,00</p>
					<p>Bike</p>
				</div>
				<figure onClick={handleClick}>
					<img src={buttonAddCart} alt="" />
				</figure>
				{cart} // acceder a la variable
</div>
```

## useEffect

**_useEffect_** es una manera de que nuestro componente de React, puede recibir nueva info, re-renderizar o cambiar su contenido, cuando una función se haya completado. Es decir, podemos controlar el momento en el cual nuestro componente tome un cierto comportamiento. Por ejemplo, en situaciones como funciones asíncronas ⇒ **_setTimeout o asyn y await,_** fetch requests o manipulaciones del DOM. Veamos un ejemplo de como usar useEffect.

#### Pre-configuración

> Instalar axios para realizar peticiones get, también instalar el plugin de babel para manejar el asincronismo

```bash
npm install axios
npm install @babel/plugin-transform-runtime
```

Editemos rápidamente .babelrc

```jsx
{
	"presets": [
		"@babel/preset-env",
		"@babel/preset-react"
	],
	"plugins": [
		"@babel/plugin-transform-runtime"
	]
}
```

**Ahora** si veamos como funciona.

```jsx
// ProductList.jsx
import React, { useEffect, useState } from 'react';
import ProductItem from '@components/ProductItem';
import axios from 'axios';

const API = 'https://api.escuelajs.co/api/v1/products';

const ProductList = () => {
	const [products, setProducts] = useState([]);

	useEffect(async () => {
		const response = await axios(API);
		setProducts(response.data);
	}, [])

	return (
		<section className="main-container">
			<div className="ProductList">
				{products.map(product => (
					<ProductItem />
				))}
			</div>
		</section>
	);
}
```

En el inicio estamos importando axios para las peticiones, y creando una constante API que será la necesaria para traer información de los productos

Analicemos el componente productList. Al inicio creamos la estructura inicial de estado, en la cual guardaremos los artículos que traeremos de nuestra API. Ahora, como indicamos, useEffect es muy útil para peticiones HTTP. Para ello, creamos la función anónima que usa useEffect. Por dentro creamos la función que usara async. Dentro creamos una constante llamada response a la cual creamos la petición y guadamos el resultado de la API. A continuación, usamos setProducts para poder guardar la información nueva en products, por eso por dentro le pasamos response.data. Lo más destacable viene ahora, en el momento que pasamos un segundo argumento a useEffect.

#### Maneras de usar useEffect

-   **Array Vacío** ⇒ ejecuta el callback solamente una vez, después de que el componente sea cargado en el DOM. Es decir, solamente cuando nuestro componente este cargado en el DOM, ejecutará la función por dentro SOLO UNA VEZ y nunca más

```jsx
const ProductList = () => {
	const [products, setProducts] = useState([]);

	useEffect(async () => {
		const response = await axios(API);
		setProducts(response.data);
	}, [])
}
```

-   **Sin argumentos** ⇒ cuando usemos useEffect, pero sin segundo argumento, este ejecutará dicho callback cada vez que se re-rendirece en el DOM. Es decir, cada vez que cambie cualquier valor del componente, este callback siempre se ejecuta

```jsx
const ProductList = () => {
	const [products, setProducts] = useState([]);

	useEffect(async () => {
		const response = await axios(API);
		setProducts(response.data);
	},)
}
```

-   **Array con datos** ⇒ este tipo se ejecuta solamente cuando un valor de prop o state de nuestro componente cambie. Es decir, imaginemos que existe un contador interno de clicks. Cada vez que el contador indique explicita mente que un valor del componente cambió, el callback de useEffect siempre se ejecutará.

```jsx
const ProductList = () => {
	const [products, setProducts] = useState([]);

	useEffect(async () => {
		const response = await axios(API);
		setProducts(response.data);
	}, [props, state])
}
```

**Tienen relación a la manera de anterior de componentes con clase**

Usar la manera de array con datos o sin datos son equivalentes a **componentDidUpdate** o **componentDidMount**. Así como indica sus nombres ⇒

-   Si el componente se actualizó, este ejecuta un callback el cual tiene cierta función. Esta manera es igual a usar useEffect con un array con datos. _Es decir, ¿hay nueva info? ⇒ realiza esto cada vez que la info nueva se actualice_
-   Si el componente se cargó en el DOM, un callback será ejecutado y nunca más. Esta manera es igual a usar useEffect con un array sin datos. _Es decir, ¿ya está cargado? ⇒ necesito que hagas esto y después te puedes quedar dormido_

## Custom hooks

En React, podemos crear hooks por nuestra propia cuenta, donde nosotros podemos escribir toda la funcionalidad que deseamos. **Ahora,** haremos un hook el cual servirá para realizar la petición a todos los productos y traer su precio, imágen y descripción.

```jsx
//useGetProducts.js
import { useEffect, useState } from 'react';
import axios from 'axios';

const useGetProducts = (API) => {
    const [products, setProducts] = useState([]);

	useEffect(async () => {
		const response = await axios(API);
		setProducts(response.data);
	}, [])

    return products;
}

export default useGetProducts;
```

El hook es muy sencillo. En el, creamos una array llamado products. Después con ayuda de useEffect realizamos una solicitud a una API (que es pasada como argumento), para traernos toda la información y guardarla con ayuda de axios. setProducts (de useState) guarda el response. Al final regresamos products.

Para poder usar el custom hook, lo implementamos en ProductList

```jsx
// ProductList.jsx
import useGetProducts from '@hooks/useGetProducts'; // Lo importamos

const API = 'https://api.escuelajs.co/api/v1/products';

const ProductList = () => {
	const products = useGetProducts(API);

	return (
		<section className="main-container">
			<div className="ProductList">
				{products.map(product => (
					<ProductItem product={product} key={product.id}/>
				))}
			</div>
		</section>
	);
}
```

Ahora, creamos una constante llamada products que será el mismo array el cual contiene toda la información de los productos. En el, le pasamos API que será un argumento del hook. Como ya sabemos, más abajo en el div, usamos el método map para el array, en donde por cada producto creará una etiqueta del componente ProductItem. ProductItem recibe como datos un key, que es igual a product. id y también product que es igual al producto del array.

Para poder aprovechar esta información, editamos ProductItem.

```jsx
import React, { useState } from 'react';
import '@styles/ProductItem.scss';
import buttonAddCart from '@icons/bt_add_to_cart.svg'

const ProductItem = ({product}) => {
	const [cart, setCart] = useState([]);

	const handleClick = () => {
		setCart([]);
	}

	return (
		<div className="ProductItem">
			<img src={product.images[0]} alt={product.title} />
			<div className="product-info">
				<div>
					<p>${product.price}</p>
					<p>{product.title}</p>
				</div>
				<figure onClick={handleClick}>
					<img src={buttonAddCart} alt="" />
				</figure>
			</div>
		</div>
	);
}

export default ProductItem;
```

En product item, recibimos estos datos en argumentos de la función dentro de llaves. Más abajo, en img, alt, y p, usamos las características de cada producto que son la imágen, titulo, descripción y precio. Así, podemos mostrar la información que corresponde a cada una.

**Características y diferencias entre useRef y useState**  
useRef es un hook utilizado para obtener una referencia a los datos de un objeto con información mutable. Es decir, es como una manera de siempre poder obtener los datos mas recientes mediante referencia de algún objeto de html. En este caso referenciamos a los valores recientes de un formulario. Dos características importantes de useRef es que los datos son persistentes en caso de que se re-renderice el componente. Así como también, actualizar los datos de esta referencia no causan el re-render. Cabe recalcar la diferencia con useState, que la actualización de datos es síncrona, ya además como hemos mencionado, no se re-renderiza

**useRef:**

1.  Genera una referencia al elemento y podremos acceder a los valores por medio de ‘current’, y por este medio obtener lo que estamos typeando según sea el caso y poderlo transmitir a donde lo necesitemos.
    
2.  El elemento que tendrá la referencia debe tener atributo: ref={NOMBRE_USEREF}
    
3.  Podemos acceder a toda la data de la siguiente manera: new FormData(NOMBRE_USEREF.current);
    
4.  El elemento también debe tener un atributo: name=“NOMBRE” y podremos acceder a la data que trae en current de la siguiente manera: formData.get(‘NOMBRE’);

**UseRef:** va a generar una referencia al elemento y poder acceder a los valores por medio de current y de esta forma tener lo que estamos tipeando según sea el caso y poderlo transmitir a donde sea el paso.

**formData**: es parte de javaScript y lo que nos va a permitir es instanciar todos los elementos que se encentren dentro de un formulario y los va a capturar conforme sean llenados y de esta forma cuando le demos on submit los va a tener presentes y podemos hacer con ellos lo que sea necesario también podemos enviar todo el objeto en este caso que se genera con formData a lo que vendría siendo el backend de esta forma va de una forma mas segura y encriptada para que esta información no sea accesible por otras personas o que en este caso alguien malicioso quiera inspeccionar como se está transmitiendo esta información  
**ergo**: tiene mucho mas valor formData que algunos otros metodos que puedas encontrar en el uso de useRef o useState.

### useContext

**Context** es una herramienta para pasar propiedades en un arbol de componentes de arriba hacia abjo sin tener que pasar por componentes intermedios.

Par usar context debemos importar dos cosas:  
**createContext** -> Permite crear el contexto  
**useContext** -> Este hook nos va permitir uusar contextos dentro de los componentes

```jsx
import { createContext, useContext} from 'react'; 
// Tambien podemos importarlo de esta manera
// Creando el contexto
const Context = createContext('valor');
```

**createContext** recibe un valor inicial que se va seleccionar en caso de no tener un provider. Puede ser cualquier valor (string, number, objeto, array…)

### ¿Que es un provider?

Es el encargado de poder pasar el contexto hacia los componentes hijos

```jsx
import { createContext, useContext} from 'react';

//creando el contexto
const Context = createContext('valor por defecto'); 
const Provider = ({children} => {
	return (
//Recibe un valor obligatorio que es el que se va estar pasando a los componentes hijos****
	<Context.Provider value={"soy un valor"} > 
				{children}
	</Context.Provider>
	)
}

//Finalmente usamos nuestro componente Provider

function App() {
	return (
	<Provider>
			<Contenido />
	</Provider>
	);
}

export default App;
```

**¿Qué es react context?**

React context es una manera de acceder a un tipo de “variables globales” entre nuestros componentes de react. Es decir, hay situaciones en las que quisieramos pasarles datos importantes a un componente de react, y a todos sus nodos hijos. Sin embargo, usando props esta tarea es muy repetitiva y poco efectiva de mantener. Incluso, existen ocasiones que le pasamos props a nodos obligadamente aunque nunca la necesiten. Es aquí cuando entra en acción react context. Nosostros podemos acceder desde donde sea a una variables en nuestra aplicación. E inlcuso podemos crear cuantos contexto queramos donde cada uno mantendra información necesaria.

Podemos destructurar las propiedades del objeto initialState definidos en el hook useInitialState de la siguiente forma:

```
const {state:{cart}}=useContext(AppContext);
```

De esta manera nos evitamos escribir state. cada que hagamos referencia a una propiedad del objeto.

```
 {cart.length > 0 ? <div>{cart.length}</div> : null}
```

Puede que no sea muy relevante en este caso… Por el momento, pero imaginate cuando tengamos un objeto con muchas propiedades. 😀💚

#### ¿Para qué sirve React Context?

a **Para compartir un estado general con todos los componentes de la aplicación.**

b Para crear nuevos custom hooks que podamos utilizar en cualquier componente de la aplicación.

c Para almacenar y actualizar información de los usuarios y/o la aplicación en UN solo componente.

#### Creaste un estado name utilizando React.useState. Necesitas que tu párrafo muestre ese nombre. Cada vez que ese estado cambie, tu párrafo debe cambiar también y mostrar el nuevo nombre. ¿Cómo lo harías?

a {{ name }}

b [name]

c **{name}**

d React.useState(name)

#### ¿Cómo ejecutamos un console.log cuando los usuarios presionen un botón?

**a `<button onClick={() => console.log('Eventos en React')}>Enviar</button>`**

b `<button OnClick={() => console.log('Eventos en React')}>Enviar</button>`

c `<button onclick={() => console.log('Eventos en React')}>Enviar</button>`

#### ¿Cuál de las siguientes es una regla para crear Custom Hooks?

a Que nunca usen otros React Hooks internamente.

b **Que su nombre empiece con use (e.j. useToggle, useCarrito).**

c Que solo se usen 1 vez en cada componente donde los necesitemos.

**Usar GitHub Pages:**

1.  npm install —save-dev gh-pages
2.  Agregar reglas al package.json:
    1.  “homepage”:”[https://SergioMaurySterling.github.io/NOMBRE_REPO”](https://sergiomaurysterling.github.io/NOMBRE_REPO%E2%80%9D)
3.  Crear nuevos scripts en package.json
    1.  “predeploy”:“npm run build”, :Este ejecutara automáticamente después el “deploy”
    2.  “deploy”:“gh-pages -d build”
4.  npm run deploy (Crea nueva carpeta llamada build que tiene todos nuestros archivos del proyecto)
5.  En GitHub ingresamos a:
    1.  Settings
    2.  Pages
    3.  Podemos ver el link de publicación

1. ¿Qué es React.js?

Una librería de JavaScript para construir interfaces de usuario.

2. Si nos basamos en el patrón MVC (modelo-vista-controlador), ¿de cuál se encarga React.js?

Vista

3. React.js nos permite construir interfaces con base en:

Componentes

4. ¿Cuál es la súper empresa encargada de construir React.js?

Facebook

5. ¿Qué es JSX?

El sistema de plantillas de React que combina la sintaxis de JavaScript con XML.

6. ¿Qué es el Virtual DOM?

Una copia o representación del DOM para evitar cambios innecesarios en el DOM real.

7. ¿Cómo creamos un elemento de React que se transforme en un DIV con la clase "container" usando JSX?

`<div className="container"></div>`

8. ¿Cómo creamos un elemento de React que se transforme en un `input` de tipo texto usando JSX?

`<input type=“text” />`

9. ¿Cuáles son las herramientas INDISPENSABLES que debemos instalar para usar React en una aplicación web?

react y react-dom

10. ¿Cómo renderizamos el componente principal de nuestra aplicación con React 17?

`ReactDOM.render()`

11. Teniendo lo siguiente:

```
const App = () => {
  return (
    <Layout>
      <Login />
    </Layout>
  );
}
```

¿Cuál es el código correcto del componente Layout?

```
const Layout = ({ children }) => { return (

<divclassname="Layout">{children}</div>

); }
```

12. ¿Qué es React Router DOM?

La herramienta más popular de React para separar nuestra aplicación entre páginas / rutas.

13. ¿Cuál es la forma correcta crear un 404 con React Router DOM 5?

Dentro del componente BrowserRouter. De último lugar con las demás rutas de la aplicación. Y con `<Route component={NotFound} />`.

**REPASAR CLASE**

14. ¿Qué herramienta de React nos permite trabajar con el estado en nuestros componentes?

React.useState

15. ¿Cuál es la forma correcta de actualizar un estado cuando los usuarios den click en un botón?

```html
const Button = () => {
  const [count, setCount] = React.useState(1);
  return (
    <button onClick={() => setCount(count + 1)}>
      ¡Click!
    </button>
  );
}
```