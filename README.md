# Buscador de Bebidas y Recetas con React Router DOM
<img src="public/pagina.PNG" alt="Recetas y bebidas"/>
App que consiste en la búsqueda la receta de una bebida,
dando como resultado una ventana modal en que aparece el  producto elegido con la opción de añadirlo a Favoritos, del cual también puedes eliminarlo.

<b>Proyecto: <a href="https://melodic-malasada-78a79f.netlify.app" target="_blank">Buscador de bebidas y recetas</a></b>

### Idea del proyecto 
Octavo proyecto realizado durante el curso de <a href="https://www.udemy.com/course/react-de-principiante-a-experto-creando-mas-de-10-aplicaciones/?couponCode=KEEPLEARNING">React y TypeScript</a>

<a href="https://github.com/antii16/crypto-react"> Ver proyecto anterior </a> 

<a href="https://github.com/antii16/rest_api_typescript_frontend"> Ver proyecto siguiente </a> 

### Tecnologías aplicadas

<ul>
  <li>React</li>
  <li>TypeScript</li>
  <li>Tailwind</li>
  <li>React Router</li>
  <li>ZUSTAND</li>
  <li>Zod</li>
  <li>API</li>
</ul>

## React Router
En este proyecto se introducirá React Router.

### ¿Qué es?
Es una librería muy cómun en REACT con múltiples páginas
Es de los creadores de Remix Run. 
En las últimas versiones es prácticamente un framework de React. 

### Características

<ul>
  <li>Permitirá crear secciones con diferentes urls tales como /tienda, etc.</li>
  <li>En versiones recientes agregaron la posibilidad de consultar API's y 
procesar formularios.</li>
</ul>

### Instalar

Cliquea <a href="https://www.npmjs.com/package/react-router-dom">aquí</a>.


### NavLink o Link

La única diferencia es que NavLink tiene un acceso a un callback en el classname, útil para resaltar, por ejemplo, la página donde se encuentra el usuario. 

### Hook: useLocation

Este hook nos devuelve el objeto `location`. Dentro de este objeto hay información sobre la URL actual. Esta información se guarda en el `pathname`.

## TailwindCSS. Theming

Nuevo concepto: theming

En la sección de `theme` del archivo `tailwind.config.js` es donde puedes definir la paleta de colores, escalas, fuentes, breakpoints, y más. 

En este proyecto se utiliza para añadir imágenes de fondo. 

## ZUSTAND

### Múltiples stores

Son útiles conforme las apps van creciendo o son más complejas. 

Existen dos formas de manejar múltiples stores:

<ul>
  <li>Crear diferentes stores.</li>
  <li>Slice Pattern.</li>
</ul>

En este proyecto se utilizará `Slice Pattern`.

#### ¿Qué es Slice Pattern?
Es una forma de dividir tus stores en pequeñas piezas y unirlas en un store principal (`useAppStore`)

También se utiliza en Redux Toolkit.

#### Tener en cuenta en este proyecto: 

<ol>
  <li>set -> permite escribir en el state. </li>
  <li>...a -> copia de todos los argumentos (set, get)</li>
</ol>

## API
Para acceder a la api 
cliquea <a href="https://www.thecocktaildb.com/api.php">aquí</a>.

## Headless UI 

Biblioteca utilizada para la ventana modal. (instalar <a href="https://headlessui.com/react/dialog">aquí</a>).

## Iconos
Para los iconos de la notificación se ha utilizado @heroicons/react (instalar <a href="https://www.npmjs.com/package/@heroicons/react">aquí</a>)

## Performance para la app con React Router DOM

Cuando se realiza un `npm run build` se crea un solo archivo de javaScript. Así, cuando el usuario visita la página, descarga todo el archivo completo. Esto lleva a que se cargue información innecesaria, como páginas que el usuario aún no ha visitado. 

Esto puede solucionarse de la siguiente forma:

<p style="color:yellow">router.tsx</p>

```
import { lazy, Suspense } from 'react'
import { BrowserRouter, Routes, Route } from 'react-router-dom'
import Layout from './layouts/Layout'

const IndexPage = lazy(() => import('./views/IndexPage'))
const FavoritesPage = lazy(()=> import('./views/FavoritesPage') )

export default function AppRouter() {
    return (
        <BrowserRouter>
            <Routes>
                <Route element={<Layout />}>
                    <Route path='/' element={
                        <Suspense fallback="Cargando...">
                            <IndexPage />
                        </Suspense>
                    } index />
                    <Route path='/favoritos' element={
                        <Suspense fallback="Cargando...">
                            <FavoritesPage />
                        </Suspense>
                    } />
                </Route>
            </Routes>
        </BrowserRouter>
    )
}

```

Lo siguiente es realizar un build. Para comprobarlo, se abre la página en el navegador con `npm run preview` y se verifica que se van descargando los archivos uno a uno. 
