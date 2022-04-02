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

![Imagen mostrando el despliegue local de Ghost en la terminal](/reporte/images/1-despliegue-local.png)

* Resultado despliegue local en el navegador

![Imagen mostrando el despliegue local de Ghost](/reporte/images/7-despliegue-local-navegador.png)

____
### __Configurar un sistema de registro de incidencias__
> Configurar un sistema de registro de incidencias. Puede hacer uso de cualquier sistema que se encuentre disponible de forma pública en línea o puede instalar alguno de forma local, pero debe asegurar que este se pueda acceder de forma remota. Si tiene dudas acerca de cómo reportar incidencias hemos preparado para usted un video que muestra ¿Cómo reportar incidencias en JIRA, Bugzilla, Mantis y GH?.

Se hizo uso de GitHub, almacenando el despliegue local de Ghost v3.41.1, en un repositorio accesible públicamente en el enlace a continuación [MISW-4103_Ghost_Semana1](https://github.com/lmguzmanp/MISW-4103_Ghost_Semana1), para registrar las incidencias en la pestaña de Issues del mismo, creando adicionalmente una plantilla que contiene la información básica necesaria en el momento de crear la incidencia.

![Imagen mostrando el botón para crear plantilla de incidencias](/reporte/images/2-sistema-incidencias-plantilla.png)

![Imagen mostrando el botón para crear plantilla de incidencias](/reporte/images/3-sistema-incidencias-contenido-plantilla.png)

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

![Directorio raíz del proyecto](/reporte/images/4-estructura-general.png)

* Estructura del frontend

![Estructura del frontend](/reporte/images/5-estructura-frontend.png)

* Estructura del server

![Estructura del server](/reporte/images/6-estructura-server.png)

#### Patrones arquitectónicos
*

#### Patrones de diseño
*

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

#### Videos

____
### __Documentar artefactos__
> A medida que va explorando la aplicación, no olvide documentar su conocimiento a través de los siguientes artefactos: (i) listado de funcionalidades, (ii) modelo de GUI (Graphic User Interface), y (iii) modelo de dominio.

#### Listado de Funcionalidades

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

#### Modelo de GUI

#### Modelo de dominio
____
