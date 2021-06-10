# Práctica: Creación de un sitio web estático con MkDocs y GitHub Pages
MkDocs es un generador de sitios web estáticos que nos permite crear de forma sencilla un sitio web para documentar un proyecto. El contenido del sitio web está escrito en texto plano en formato Markdown y se configura con un único archivo de configuración en formato YAML.

## Creación de un contenedor Docker con MkDocs y el theme Material
En esta práctica vamos a utilizar una imagen Docker que contiene MkDocs y el theme Material.

Esta imagen Docker nos permite:

- Crear un nuevo proyecto (Comando: new).
- Crear un servidor de desarrollo local (Comando: serve).
- Generar la documentación (Comando: build).
- Publicar la documentación en GitHub Pages (Comando: gh-deploy)

### Crear un nuevo proyecto (Comando: new)
En primer lugar vamos a situarnos en el directorio donde queremos crear nuestro proyecto. En nuestro caso será el directorio proyecto.

Para crear la estructura de archivos del proyecto MkDocs podemos hacer uso del comando new, como se muestra en el siguiente ejemplo.

` docker run --rm -it -p 8000:8000 -v "$PWD":/docs squidfunk/mkdocs-material new . `
Nota: Vamos a crear el contenedor desde el directorio principal el proyecto porque necesitamos crear un volumen de tipo bind mount entre nuestra máquina y el contenedor Docker.


### Archivo de configuración mkdocs.yml
Dentro del directorio de nuestro proyecto deberemos crear el archivo de configuración YAML mkdocs.yml.

Por ejemplo, en el siguiente archivo configuración mkdocs.yml estamos indicando el nombre del sitio web que estamos creando (site_name), los enlaces a las páginas que van a aparecer en el menú de navegación (nav) y el theme que vamos a utilizar (theme).
```
site_name: IAW

nav:
    - Principal: index.md
    - Acerca de: about.md

theme: material
```
En la documentación oficial del theme Material for MkDocs puede encontrar más información sobre todas las opciones de configuración que podemos incluir en el archivo de configuración mkdocs.yml.

### Generar la documentación (Comando: build)
También es posible generar directamente el sitio web sin tener que iniciar un servidor local de desarrollo. Para generar el sitio web automáticamente podemos ejecutar el siguiente comando:

`docker run --rm -it -v "$PWD":/docs squidfunk/mkdocs-material build`
El comando anterior creará un directorio llamado site donde guarda el sitio web que se ha generado.

### Publicar la documentación en GitHub Pages (Comando: gh-deploy)
Es posible publicar la el sitio web en GitHub Pages con el siguiente comando:

`docker run --rm -it -v ~/.ssh:/root/.ssh -v "$PWD":/docs squidfunk/mkdocs-material gh-deploy`

