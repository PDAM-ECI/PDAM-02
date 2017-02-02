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

El resultado final debe ser:

![alt text](http://i.giphy.com/26gskiARSbw06Em08.gif)
