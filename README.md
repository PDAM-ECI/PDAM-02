# PDAM-02

En este laboratiorio nos enfocaremos en AngularJS y en otras herramientas que ayudarán en la construcción 
del proyecto final en ionic. 

# Configuración del proyecto base de ionic

Para comenzar instale un proyecto ionic con un template de prueba desde la linea de comandos:

```bash
ionic start pdam-2 sidemenu
```

Esto generará la aplicación base dentro de la carpeta pdam-2 con un menu lateral. confirme que la instalación 
haya sido exitosa corriendo la aplicación en modo web.

# Interacción con APIs

Para este punto se requiere un API de prueba, usaremos el servicio [JSON placeholder](https://jsonplaceholder.typicode.com/)
Este servicio tiene varios recursos que podemos usar, para el primer punto usaremos "/albums"

### Añadir un item al menu

Para añadir un item al menu lo primero es crear el template (vista) y el controlador del nuevo elemento "albums", 
para hacer esto ubique la carpeta de templates, copie el template playlists y cambie el nombre del nuevo archivo 
por "albums". Dentro del archivo de "controllers.js" cree un nuevo controlador con el nombre "AlbumsCtrl". Dentro de la
vista cambie el titulo por "Albums".

```html
<ion-view view-title="Albums">
...
```

Añada una nueva ruta para la aplicación con base en la ruta de playlists pero en este caso para la nueva vista y 
controlador creados. La estado de la ruta debe tener el nombre "app.albums" y la url debe ser "/albums".

La ultima parte será añadir en el menu lateral un vínculo a la nueva sección creada, para esto edite el archivo 
"menu.html" apropiadamanete.

El resultado debe ser:

![alt text](http://i.giphy.com/26gskiARSbw06Em08.gif)

### Cargar información del API

Para conectarnos con el API de prueba, inyectaremos el servicio "$http" de angular, este modulo permite hacer llamados 
HTTP. Así mismo inyecte el modulo $log para poder depurar su código. 

La logica de la aplicación debe estar ubicada dentro del controlador respectivo, en este caso usaremos el controlador
de "albums". Las llamadas HTTP son asíncronas y retornan un objeto Promise. Usando el metodo 

```javascript
$http.get( ...
```

Haga un llamado GET al servicio https://jsonplaceholder.typicode.com/albums para obtener el listado de los albumes de 
prueba. Una ves tenga esta informacion asignela a una variable del $scope que se llame albums, esto para poder vincularlos
con la vista y mostrarlos el listado.

Teniendo en cuenta que el usuario necesita información acerca de lo que la aplicación está haciendo, necesitamos usar un
servicio de angular para mostrar que la aplicación esta cargando información. Consulte el uso del servicio 
[$ionicLoading](https://ionicframework.com/docs/api/service/$ionicLoading/)

Para simular un ambiente de red mas parecido a la realidad pude usar las herramientas de red de chrome para simular una 
velocidad de red dentro de una red móvil, por ejemplo 4G.

![alt text](http://i.giphy.com/26xBROAJgywbNMleo.gif)

El resultado debe ser:

![alt text](http://i.giphy.com/26gsvxu1OafhHM7S0.gif)

Para crear o borrar información puede usar el mismo servicio $http de angular para hacer llamados POST, PUT y DELETE. En
este caso el API de prueba no soporta la persistencia o actualización de datos.

# Manejo de datos locales

Dentro de las aplicaciones móviles a diferencia de las aplicaciones web, se debe tener en cuenta que el dispositivo puede
perder conectividad. Para esto se usa el almacenamiento local ya sea en memoria o en una base de datos local. Esto permite 
que el usuario pueda usar la aplicación sin necesidad de tener conexión a internet.

En las aplicaciones hibridas se pueden usar dos alternativas, plugins para interactuar con los servicios de persistencia
nativos o usar los servicios de persistencia de los navegadores. Para este laboratorio usaremos las opciones del navegador
para poder probar sin necesidad de un dispositivo real.

Para este laboratorio crearemos usuarios localmente, para estructurar el código es necesario crear un factory de angular 
que maneje la interacción con los usuarios.

Cree el archivo "services.js" dentro de la carpeta www/js dentro de este archivo inserte el siguiente codigo.
 
```javascript
angular.module('starter.services', [])

    .factory('UserFactory', function ($localForage) {
        return {
            createUser:function (username, name) {
                
            },
            listUsers: function () {

            }
        }
    });
``` 

Cargue el archivo desde el index.html

```html
    ...
    
    <script src="js/app.js"></script>
    <script src="js/controllers.js"></script>
    
    <script src="js/services.js"></script>
    
    ...
``` 

Esto creará un modulo para agrupar los servicios y factories de la aplicación. Y tambien definirá el UserFactory. Usaremos
este factory para manejar la persistencia de los datos de los usuarios. Haremos uso de una libreria que facilita el manejo
de los diversos tipos de almacenamiento disponibles en los navegadores.

Instale la libreria [Angular localforage](https://github.com/ocombe/angular-localForage) usando bower.

```bash
bower i angular-localforage --save
```

Siga las instrucciones de la librería para inyectar el modulo y cargar los archivos necesarios. Ejemplo:

app.js

```javascript
angular.module('starter', ['ionic', 'starter.controllers', 'LocalForageModule'])
```

index.html

```html
    ...
    
    <script src="lib/localforage/dist/localforage.min.js"></script>
    <script src="lib/angular-localforage/dist/angular-localForage.min.js"></script>
    
    ...
```

Revise la aplicación en modo web y verifique que no hay errores en la consola.

Dentro del UserFactory, implemente los metodos createUser y listUser. Para manejar la tabla de "usuarios" es necesario
crear una instancia del localforage:

```javascript
    ...
    
    .factory('UserFactory', function ($localForage) {
        var usersTable = $localForage.createInstance({
            name: 'users'
        });
        
    ...

```

usando los metodos setItem e iterate como lo indica la documentación de localforage, podemos implementar los métodos 
necesarios en el factory. Una vez tenga estos métodos deberá implementar las vistas y controladores necesarios para
crear y listar los datos que se almacenan localmente. Para esto cree dos nuevos controladores 

* UsersCtrl
* UsersEditCtrl

dentro de los dos controladores inyecte el servicio de $scope y el factory de users que se creó anteriormente.

```javascript
    ...
    
    .controller('UsersCtrl', function ($scope, UserFactory) {
            
    })
    
    .controller('UsersEditCtrl', function ($scope, UserFactory) {
        
    })
        
    ...

```

Dentro del controlador de UsersCtrl se tendrá la logica para listar los usuarios creados, y dentro del UsersEditCtrl se
tendrá la logica para editar y crear nuevos usuarios.


