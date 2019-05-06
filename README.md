# imageToDockerHub
This repo, upload a docker image to a Docker Hub 

# dockerBasicNode
Only creates a basic "Hello world app" with Node and Docker

## Local 
### 1. Crea un directorio local para nuestra App, con NPM generamos el archivo package.json e instalomos Express.

```
$ mkdir hello-world
$ cd hello-world
$ npm init
$ npm install —save express
```

### 2. Creamos un archivo index.js para nuestro codigo. 

`
$ touch index.js
`

### 3. Abrimos el archivo y creamos nuestra app web básica.

 ```javascript
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(8081, function () {
  console.log('app listening on port 8081!')
})
 ```

### 4. (Opcional) Probar nuestro servidor, con localhost:8081 en el navegador 

`$ node index.js`

## Comenzamos con la parte de Docker 

### 5. Creamos un Dockerfile

` $touch Dockerfile`

### 6. Agregamos nuestra receta en el Dockerfile

```
FROM node:7
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
CMD node index.js
EXPOSE 8082
```

La primera línea le dice a Docker que use otra imagen de Docker como plantilla para la imagen que estamos creando.

Lo que estamos usando es la imagen oficial de Docker para Node.js y su versión 7 de esa imagen.

La segunda línea, establece un directorio de trabajo donde el código de la aplicación vivirá dentro del contenedor Docker.

En las líneas 3, 4 y 5, le pedimos a Docker que copie nuestros archivos locales en el directorio de trabajo del contenedor y que ejecute npm para instalar cualquier dependencia de paquete.

En la línea 6, le pedimos a la ventana acoplable que ejecute nuestra aplicación dentro del contenedor usando un nodo para ejecutar nuestro archivo index.js.

Por último, en la línea 7, configuramos el puerto que Docker expondrá cuando el contenedor se esté ejecutando. Puerto 8082 en nuestro caso.

NOTA: La aplicación Node.js usa el puerto 8081 pero usará ese puerto dentro del contenedor Docker cuando el contenedor se esté ejecutando.

### 7. Constrior imagen de Docker 

`$ docker build -t hola-world .`

## SUBIENDO A DUCKER HUB 

Para subir una imagen al repositorio de docker hub

### 8. Logeandonos desde la terminal 

`$ docker login`

Se nos pedirán nuestras credenciales de nuestra cuenta de docker hub 


### 9. Creando tag para subir la imagen 

Es importante saber que antes de subir nuestra imagen a docker hub, demeos crear un tag nuevo de la siguiente forma: 

`$ docker tag [nombre de la imagen local]:[tag local]  [usuario docker hub]/[nombre nuevo de imagen]:[tag nueva]`

ejemplo:

`$ docker tag old-version:00 oscarwtts/new-version:01`

### 10. Subiendo imagen

`$ docker push oscarwtts/new-version`



