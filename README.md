# Reporte de Pruebas Exploratorias

## _MISW4103 - Luis Miguel Guzman Perez y Diego Fernando Eslava Lozano_

____
### __Desplegar Ghost de forma Local__

> Instalar la versión 3.41.1 de la aplicación bajo pruebas “Ghost” en su ambiente local de pruebas. Para esto consulte el CodeLab “Desplegar Ghost de forma local” y el siguiente link

Para la instalación de Ghost v3.41.1 se utilizaron los siguientes comandos, funcionales en dos ambientes distintos:

* Ubuntu 20.04.4 LTS - Lenovo Legion 5 Pro
* MacOS Monterrey 12.1 - MacBook Pro 14" 2021

#### Pasos para despliegue de Ghost de forma local

1. Instalar nvm este es necesario para manejar las versions de Node.js en caso de tener instalada una no compatible con la versión de Ghost 3.41.1.

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

2. Instalar la versión adecuada de Node, en este caso para Ghost 3.41.1, la versión LTS 14 de Node.
```sh
nvm install 14
```

3. Usar la versión adecuada de Node
```sh
nvm use 14
```

4. Crear directorio vacío para instalar ghost de forma local
```sh
mkdir ghost-local
```

5. Ir a ese directorio
```sh
cd ghost-local
```

6. Instalar Ghost CLI a nivel global
```sh
npm i -g ghost-cli
```

7. Instalar de forma local la versión de Ghost 3.41.1
```sh
ghost install 3.41.1 --local --force
```

8. En Ubuntu probablemente puede salir un error de que no se pudo iniciar Ghost de forma local porque falta el paquete sqlite3, por lo tanto, se procedió a instalarlo
```sh
npm i sqlite3
```

9. Iniciar Ghost 3.41.1
```sh
ghost start
```

10. Ghost desplegado localmente
Se desplegó Ghost de forma local exitosamente en el puerto 2368.

* Resultado despliegue local en la terminal

![Imagen mostrando el despliegue local de Ghost en la terminal](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/1-despliegue-local.png)

* Resultado despliegue local en el navegador

![Imagen mostrando el despliegue local de Ghost](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/7-despliegue-local-navegador.png)

____
### __Configurar un sistema de registro de incidencias__
> Configurar un sistema de registro de incidencias. Puede hacer uso de cualquier sistema que se encuentre disponible de forma pública en línea o puede instalar alguno de forma local, pero debe asegurar que este se pueda acceder de forma remota. Si tiene dudas acerca de cómo reportar incidencias hemos preparado para usted un video que muestra ¿Cómo reportar incidencias en JIRA, Bugzilla, Mantis y GH?.

Se hizo uso de GitHub, almacenando el despliegue local de Ghost v3.41.1, en un repositorio accesible públicamente en el enlace a continuación [MISW-4103_Ghost_Semana1](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1), para registrar las incidencias en la pestaña de Issues del mismo, creando adicionalmente una plantilla que contiene la información básica necesaria en el momento de crear la incidencia.

![Imagen mostrando el botón para crear plantilla de incidencias](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/2-sistema-incidencias-plantilla.png)

![Imagen mostrando el botón para crear plantilla de incidencias](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/3-sistema-incidencias-contenido-plantilla.png)

___
### __Revisar código fuente de Ghost__
> Revisar el código fuente de la aplicación con el objetivo de identificar: lenguajes usados en la aplicación, estructura de directorios, patrones arquitectónicos y de diseño usados en la ABP.

Accedimos al repositorio del proyecto [Ghost](https://github.com/TryGhost/Ghost) y descargamos el código fuente en formato comprimido para analizarlo localmente. El código fuente fue descargado directamente de los releases en la dirección [3.41.1](https://github.com/TryGhost/Ghost/archive/refs/tags/3.41.1.zip)

#### Lenguajes usados
* JavaScript
* JSON
* Markdown
* YAML
* Handlebars (HTML plantillado)
* CSS

#### Estructura de directorios
* Directorio raíz

![Directorio raíz del proyecto](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/4-estructura-general.png)

* Estructura del frontend

![Estructura del frontend](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/5-estructura-frontend.png)

* Estructura del server

![Estructura del server](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/6-estructura-server.png)

#### Patrones arquitectónicos y de diseño
* Singleton (GoF - Patrón creacional)
  > Se asegura que solo existe una instancia del servicio de URLs dentro de la aplicación, mediante su exposición única como se aprecia en la siguiente imagen:

  ![Uso del patrón Singleton en frontend de Ghost](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/8-singleton.png)

* Facade (GoF - Patrón estructural)
  > Se implementa una fachada que se encarga de exponer objetos con funcionalidades específicas.

  ![Uso del patrón Facade en server de Ghost](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/10-facade.png)

* Observer (GoF - Patrón de comportamiento)
  > El servicio de URL del frontend hace uso del patrón Observador, creando un recurso que hereda de la clase EventEmmiter, permitiendo emitir actualizaciones basadas en eventos específicos.

  ![Uso del patrón Observer en frontend de Ghost](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/11-observer.png)

* Single responsability principle (SOLID)
  > En la imagen a continuación se evidencia como la responsabilidad se asigna a servicios distintos en lugar de reunirlos en uno solo, es posible identificar el servicio de aplicación, el de temas y el de configuración del frontend.

  ![Uso del principio de responsabilidad única en el servidor](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/9-srp.png)

* Alta cohesión (GRASP)
  > El componente GhostServer presenta una alta cohesión, puesto que sus funcionalidades están relacionadas únicamente con características propias del servidor, como encendido, parada y apagado.

  ![Alta cohesión en el objeto GhostServer](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/images/12-cohesion.png)
___
### __Explorar aplicación__
> Explorar rápidamente la aplicación con el objetivo de identificar la estrategia de navegación usada (menús, pestañas, botones, enlaces, etc.) y las funcionalidades de la ABP. Dedique no más de 10 minutos a esto.

* Elementos de navegación
  * Acordeones
  * Botones
  * Campos de texto
  * Menús
  * Tarjetas
  * Cajas de selección
  * Selección de archivos
  * Tour de guía de inicio
  * Barra de navegación
  * Enlaces internos y externos

* Funcionalidades
  * Registro de usuarios
  * Panel de configuración
  * Creación, edición, eliminación y consulta de posts
  * Visualización del sitio
  * Creación, edición, eliminación y consulta de páginas
  * Etiquetas
  * Perfiles de usuario
  * Modificación de diseño visual
  * Modo claro/oscuro
  * Integración con aplicaciones externas
  * Búsquedas
  * Funcionalidades experimentales
  * Carga de archivos
  * Exportación de archivos
  * Soporte y ayuda
  * Noticias
  * Inyección de código
  * Configuración general de la página
  * Organización de listas de contenido
  * Filtrado de listas

___
### __Ejecutar pruebas__
> Ejecutar, para cada una de las funcionalidades, varios escenarios de pruebas positivas y negativas, y registrarlos en el formato [inventario de pruebas exploratorias](https://thesoftwaredesignlab.github.io/AutTestingCourseraBook/templates/inventario-pruebas-exploratorias.xlsx). No olvide que las pruebas exploratorias (PE) deben quedar documentadas a través de un video que muestre los pasos realizados. Si se encuentra un defecto en alguna PE no olvide reportarlo en el sistema de incidencias que usted seleccionó. Se espera que como resultado de la sesión de PE se reporten mínimo 10 defectos.

#### Formato de pruebas exploratorias

El enlace está compartido con usuarios Uniandes, por favor hacer login previo a la consulta. En caso de no poder acceder por favor reportar por Slack a Luis Miguel Guzman Perez o Diego Fernando Eslava Lozano

[Vínculo Formato PE](https://uniandes-my.sharepoint.com/:x:/g/personal/d_eslava_uniandes_edu_co/EdZBPs3hMGpOlFiKIEv0IxQBcB31fnZjnEtgU5Jze-57Rw?e=enO6wp)

#### Videos
|Incidencia|Video|
|----------|-----|
|[Incidencia 001](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/1)|[P002](https://www.loom.com/share/f126c3c6898f43d6ad34bddd335e2a25)|
|[Incidencia 002](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/7)|[P004](https://www.loom.com/share/027c8178dca642cd9c41316862228869)|
|[Incidencia 003](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/8)|[P006](https://www.loom.com/share/d91844fc20a3425aacbcc204c606ec6b)|
|[Incidencia 004](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/9)|[P008](https://www.loom.com/share/4deadf5c5f2a4d0ca0738edcb3d88f94)|
|[Incidencia 005](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/10)|[P010](https://www.loom.com/share/f33904a6bf474ebda1411f7a8212d908)|
|[Incidencia 006](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/2)|[P012](https://www.loom.com/share/e9810e8d95844825ac5de5def5d3cb98)|
|[Incidencia 007](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/3)|[P013](https://www.loom.com/share/be48ff62cad4444c98dc1704a2926f9c)|
|[Incidencia 008](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/4)|[P016](https://www.loom.com/share/994ddb3b0ebf450482a5822e8c48608b)|
|[Incidencia 009](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/5)|[P019](https://www.loom.com/share/b97b12edd6ae4da7b4a9ec85188fa13a)|
|[Incidencia 010](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/issues/6)|[P020](https://www.loom.com/share/a0f64d36685a408382de0ca8df263892)|

____
### __Documentar artefactos__
> A medida que va explorando la aplicación, no olvide documentar su conocimiento a través de los siguientes artefactos: (i) listado de funcionalidades, (ii) modelo de GUI (Graphic User Interface), y (iii) modelo de dominio.

#### Listado de Funcionalidades

* Registro de usuarios
  > Se permite el registro de personal de administración del sitio con distintos roles.
* Panel de configuración
  > Cuenta con un sitio central de configuración de parámetros generales, que incluye la administración de idioma, título y descripción del sitio. Cambio de multimedia principal como íconos y logos.
* Creación, edición, eliminación y consulta de posts
  > Característica principal de la aplicación que permite la administración de contenidos publicados, así como borradores y programación de publicación.
* Visualización del sitio
  > El ambiente de desarrollo cuenta con la posibilidad de previsualizar el contenido generado, dando una idea general de cómo se verá el sitio una vez desplegado en producción.
* Creación, edición, eliminación y consulta de páginas
  > Se incluye funcionalidad de creación de páginas dentro del sitio, con apuntadores propios y personalización de los mismos.
* Etiquetas
  > Las publicaciones pueden ser marcadas con descriptores predefinidos, los cuales también pueden ser creados, consultados, editados y eliminados.
* Perfiles de usuario
  > Los perfiles de usuario pueden ser editados, añadiendo avatares, información de redes sociales, biografía, etcétera.
* Modificación de diseño visual
  > Varias secciones del aplicativo permiten la modificación de aspectos visuales, como colores, imágenes, íconos, logos, avatares, etc.
* Modo claro/oscuro
  > Dentro de las funcionalidades experimentales de la versión 3.41.1 se permite hacer uso del modo oscuro, el cual intercambia los colores predeterminados, los cuales son brillantes en su mayoría, por colores oscuros que son más amigables con los ojos.
* Integración con aplicaciones externas
  > Existe la posibilidad de conectar herramientas externas, como Unsplash, útil para encontrar y usar fotos royalty free.
* Búsquedas
  > El panel de administración principal cuenta con una herramienta global de búsqueda que permite navegar fácilmente entre secciones y encontrar contenido relevante mediante palabras clave.
* Funcionalidades experimentales
  > La sección de herramientas experimentales permite hacer uso o implementación de utilidades como creación de miembros suscriptores y gestión general de contenido.
* Carga de archivos
  > Varias secciones del panel de administración incluyen carga de archivos, principalmente imágenes para uso en perfiles de usuario, banners de los post, logos, etc.
* Exportación de archivos
  > Se permite exportar el contenido en lenguaje JSON (JavaScript Object Notation) el cual es compatible con gran cantidad de aplicativos web.
* Soporte y ayuda
  > La sección de soporte y ayuda contiene enlaces a documentación relevante para la exploración de la documentación oficial de la herramienta.
* Noticias
  > Una ventana modal informa de las novedades de la aplicación en la versión utilizada.
* Inyección de código
  > Las secciones del encabezado y pie de página permite inyección de código personalizado, principalmente para incluir funcionalidades como rastreo y etiquetas de metadatos.
* Configuración general de la página
  > Se habilita la modificación de título y descripción del sitio, entre otras características.
* Organización de listas de contenido
  > Las vistas que presentan información en formato de lista pueden ser ordenadas de acuerdo a parámetros específicos.
* Filtrado de listas
  > Las vistas que presentan información en formato de lista pueden ser filtradas de acuerdo a parámetros específicos.

#### Modelo de GUI

Se utilizó un tablero de Miro para el análisis del flujo de interfaz gráfica de usuario. A continuación se relaciona el enlace:

[Tablero MIRO - MISW-4103](https://miro.com/app/board/uXjVOAa2BLw=/?invite_link_id=469249788849)

#### Modelo de dominio

Para el modelo de dominio se utilizó una herramienta de ingeniería inversa para bases de datos: DbSchema, la cual puede ser descargada desde [su sitio web](https://dbschema.com/)

El resultado del proceso de ingeniería inversa se presenta a continuación:
[Documento Modelo de Dominio](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1/blob/main/reporte/documents/modelo-dominio.pdf)
____
