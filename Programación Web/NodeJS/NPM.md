**NPM** = Node Package Manager.

## Historia

- **1995** Nacimiento de JS --> Uno de los lenguajes mas populares con miles de aplicaciones y grandes empresas apostando por este recurso.
- **2009** Nace Node.js --> Un entorno en tiempo de ejecucion multiplataforma.
- **2009** NPM (Node Package Manager) --> Gestor de paquetes por defecto para Node.js

## ¿Qué son los gestores de dependencias?

**Organizan**, **administran** y tienen una serie de **herramientas** las cuales podemos aprovehar en nuestros proyectos y ser mucho mas agiles en la creación de nuestras aplicaciones.

## Paquetes y modulos

Van a ser instalados y utlizados segun sea el caso. Podemos tener paquetes que funcionan solamente de lado de node asi como tambien de lado de la arquitectura web.

## Herramientas que tenemos al instalar Node.js

- **Repositorio onlines** --> Podemos publicar paquetes que sean mejoras y/o ayudas para la construccion de aplicaciones.
- **Command Line Client (CLI)** --> Cliente que nos ayuda a trabajar de manera correcta con comandos.

## NPM vs NPX

![[Pasted image 20221103170248.png]]

## Comandos

#### Install `package.json` dependencies

```shell
npm install
```

#### Shorthand

```shell
# install
npm i <package>

# Install globally
npm i <package> -g

# Instalar una dependencia opcional
npm install <package> -o

# Simula la instalacion de un paquete para ver si hay conflictos
npm install <package> —dry-run

# Instalar un version especifica de un paquete
npm install <package>@0.15.0

# Instalar la version mas reciente del paquete
npm install <package>@latest

# uninstall
npm un <package>

# update
npm up <package>


```

#### Flags

`-S` is the same as `--save`, and `-D` is the same as `--save-dev`.

#### List globally installed packages

```shell
npm list -g --depth=0
```

#### Uninstall global package

```shell
npm -g uninstall <name> 
```

#### Upgrade `npm` on Windows

```shell
npm-windows-upgrade
```

#### Update global packages

To see which packages need updating, use:

```shell
npm outdated -g --depth=0
```

To update global packages individually you can use:

```shell
npm update -g <package> <package> <package>
```

#### list available scripts to run

```shell
npm run
```

#### Update `npm`

```shell
npm install -g npm@latest

# using windows? Then use
npm-windows-upgrade
```

#### Installed version

```shell
npm list # for local packages
```

#### Audita las dependencias en busca de vulnerabilidades

```shell
npm audit
```

#### Audita e intenta arreglar las vulnerabilidades

```shell
npm audit fix
```

#### Muestra los resultados de la auditoria en un JSON

```shell
npm audit --json
```

#### Corrige los problemas instalando otras dependencias si es necesario

```shell
npm audit fix --force
```

#### Script para reinstalar los paquetes

```json
// package.json 
{ 
	"scripts": {
		"phoenix": "rm -f package-lock.json && rm -rf ./node_modules && npm install --no-fund --no-audit" 
	} 
}
```

#### Compilacion para produccion

```shell
npm run build --dd
```
