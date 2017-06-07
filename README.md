Proyecto creado para integrar create-react-app [Instalación 06-06-2017].

1. Crear un proyecto desde create-react-app.
`$ create-react-app <nombre_del_proyecto>`

2. Agregar foundation-sites como dependencia del proyecto.
`$ npm install foundation-site --save`

3. Incluir los estilos de foundation dentro del archivo CSS principal **index.css**.
```
@import "../node_modules/foundation-sites/scss/foundation";
@include foundation-everything;
```


4. Debido a que foundation está estructurado con Sass es necesario incluir un  
preprocesador de estilos dentro del proyecto y así compatibilizarlos, para esto
nos ayudamos con la documentación que ya trae el kit de react e instalamos
node-sass-chokidar
`$ npm install node-sass-chokidar --save-dev`

5. Luego incluimos en **package.json** los scripts correspondientes para generar 
CSS desde SASS.
```
"scrips": {
    "build-css": "node-sass-chokidar src/ -o src/",
    "watch-css": "npm run build-css && node-sass-chokidar src/ -o src/ --watch --recursive",
    ...
}
```

6. Renombramos los archivos de estilo que queremos procesar, en este caso 
**index.css** a **index.scss** y ejecutamos **npm run build-css** para testear
que funciona correctamente.

Ya podemos ejecutar nuevamente `npm start` y notar que ya no arroja error con 
SASS.  

7. Es posible automatizar la generación de los archivos CSS desde SASS al 
ejecutar `npm start` incluyendo la siguiente dependencia.
`$ npm install npm-run-all --save-dev`

8. Luego es necesario modificar los scripts contenidos en **package.json**
```
"scripts": {
    ...
    "start-js": "react-scripts start",
    "start": "npm-run-all -p watch-css start-js",
    "build": "npm run build-css && react-scripts build",
    ...
}
```
