# Node Express Mongoose

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=ffffff)&nbsp;
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=flat&logo=node.js&logoColor=white)&nbsp;
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=flat&logo=mongodb&logoColor=white)&nbsp;

Más ejemplos de Badges en [markdown-badges](https://ileriayo.github.io/markdown-badges/), [Badges 4 README.md Profile](https://github.com/alexandresanlim/Badges4-README.md-Profile) y [Awesome Badges](https://github.com/Envoy-VC/awesome-badges)

## Introducción

**Node Express Mongoose** es una aplicación Web de ejemplo, desarrollada con Node.js, Express.js y Mongoose. Es una aplicación sencilla con un fin didáctico, que permite mostrar los usuarios registrados, así como hacer login, modificar tu perfil, hacer logout, o registrarte (sign up).

Utiliza lo siguiente:

* `ejs` como motor de vistas para renderizar páginas web desde el lado del servidor (SSR: Server Side Rendering). La vistas se almacenan en `/views`, donde podemos encontrar:
  * Varias plantillas de página: index.ejs, login.ejs, signup.ejs, edit.ejs, profile.ejs
  * Un par de plantillas usadas como componentes reutilizables por las páginas anteriores: _header.ejs, _footer.ejs
* `mongoose` para definir un esquema o modelo para almacenar Usuarios en MongoDB. Este esquema incluye métodos (ej: checkPassword, name) y un middleware pre-save para cifrar la contraseña con `bcrypt` antes de guardarla (se almacena el hash).
* `connect-flash` para enviar mensajes flash al usuario desde el código Node del servidor, después de una redirección, por ejemplo, al intentar hacer login para mostrar un mensaje de error.
* `passport` es un middleware de autenticación para Node, con el propósito de autenticar peticiones y ahorrar algunos quebraderos de cabeza. `passport` no se encarga de la autenticación de usuarios, sólo proporciona un código inicial para facilitar la autenticación de usuarios, que podría realizarse de diferentes maneras (ej: usuarios almacenados en MongoDB, login social de Facebook, Google, o Twitter, etc). En este caso, utilizaremos una estrategia de usuarios locales, para lo que usaremos `passport-local` para indicarle a `passport` como debe serializar y deserializar usuarios, apoyándonos en una cookie de sesión y `mongoose`para la persistencia en MongoDB.


## Módulos de Node.js utilizados (dependencias)

Revisar el fichero **package.json** para mayor detalle.

### Dependencias de Desarrollo

| Dependencia               | Motivo
|---------------------------|-------
| nodemon                   | Permite reiniciar automáticamente la aplicación al detectar una cambio en un fichero (útil durante el desarrollo y pruebas en local)

### Dependencias de Producción

| Dependencia         | Motivo
|---------------------|-------
| cross-env           | Permite establecer y utilizar variables de entorno de manera uniforme en diferentes plataformas, como Windows, Linux y macOS
| body-parser         | Analiza el cuerpo (body) de las peticiones, extendiendo el objeto `req`, para añadirlas dentro de `req.body`.
| cookie-parser       | Analiza las cookies de las peticiones, extendiendo el objeto `req`, para añadirlas dentro de `req.cookies` (parejas de clave-valor, donde la clave es el nombre de la cookie y el valor es el valor de la cookie).
| connect-flash       | Para almacenar mensajes flash temporales (ej: éxito, error, advertencia, etc) en la sesión del usuario, que se muestran al usuario en una sola solicitud y luego se eliminan en la siguiente solicitud
| bcrypt-nodejs       | Proporciona encriptación de contraseñas para Node.js mediantes hash y sal.
| ejs                 | Motor de plantillas EJS (Embedded JavaScript) para generar HTML de forma dinámica
| express             | Es un servidor Web para Node.js (Web Application Framework)
| passport            | Middleware de autenticación para Node, soporte tanto una estrategia de usuarios locales, como usuarios de Facebook, Google, Twitter, etc.
| passport-local      | Soporte para la estrategia de autenticación local de Passport.
| mongoose            | Es un ODM (Object Document Modeler) para MongoDB y Node.js, permite definir el modelo de datos, son su esquema, validaciones, campos virtuales, etc.
| morgan              | Es un Logger para el registro de peticiones HTTP


## Cómo arrancar MongoDB de forma dockerizada

Arrancamos un docker con MongoDB. Las versiones más recientes de MongoDB requieren algunas extensiones del procesador que impiden su ejecución en procesadores antiguos o básicos, en cuyo caso, se podría utilizar una versión de MongoDB más antigua (ej: mongo:4.4.6).

```shell
docker run -d --rm -p 27017:27017 --name mongodb mongo:7.0.6
```

A continuación se muestra:

* Cómo mostrar los Logs del contenedor de MongoDB
* Cómo conectarse al contenedor de MongoDB mediante una sesión Bash
* Cómo conectarse al contenedor de MongoDB mediante una sesión de Mongo Shell

```shell
docker logs mongodb
docker exec -it mongodb bash
docker exec -it mongodb mongosh
```

## Cómo ejecutar en local el proyecto, de forma dockerizada

A continuación se muestra:

* Cómo crear una imagen en local con docker build.
* Cómo listar las imágenes que tenemos disponibles en local. Deberá aparecer la que acabamos de crear.
* Cómo ejecutar un contenedor con nuestra imagen.
* Cómo comprobar los contenedores que se están ejecutando (estará el nuestro).
* Cómo ver los Logs de nuestro contenedor.
* Cómo parar el contenedor.

```shell
docker build -t node-express-mongoose .
docker images
docker run -it --rm -d -p 3000:3000 --name node-express-mongoose node-express-mongoose
docker ps
docker logs node-express-mongoose
docker stop node-express-mongoose
```

## Cómo ejecutar en local el proyecto, de forma nativa

Nos posicionamos en el directorio de la aplicación (app).

```shell
cd app
```

Instalamos las dependencias, si no lo hemos hecho anteriormente.

```shell
npm install
```

Podemos ejecutar la aplicación, en modo DEV, así.

```shell
npm run dev
```

O ejecutarla, en modo Prod, así.

```shell
npm start
```
