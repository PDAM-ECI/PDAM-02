# PDAM-02

En este laboratiorio nos enfocaremos en AngularJS y en otras herramientas que ayudarán en la construcción 
del proyecto final en ionic. 

# Configuración del proyecto base de ionic

Para comenzar instale un proyecto ionic con un template de prueba desde la linea de comandos:

```javascript
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

Para conectarnos con el API de prueba, inyectaremos el modulo "$http" de angular, este modulo permite hacer llamados 
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

### Enviar informacion al API
