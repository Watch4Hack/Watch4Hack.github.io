# Como publicar en la web

Jekyll permite generar una web estatica a traves de archivos Markdown, tenemos que seguir los siguientes pasos para publicar en la web:

1. Descargamos la última versión de los dos repositorios, uno es privado y lleva el código para generar la web, el otro repositorio solo contiene la parte estatica de la web que hemos generado.
    * https://github.com/Watch4Hack/Watch4Hack.github.io -> repositorio público que tiene la web
    * https://github.com/Watch4Hack/Website.git -> repositorio privado que contiene el código del jekyll
<br>

2. Generamos un archivo dentro del repositorio Website, en la carpeta _posts. El nombre del archivo tiene que tener el siguiente formato: "aaaa-mm-dd-xxxxxxx.md" donde:
    * aaaa = año
    * mm = mes
    * dd = dia
    * xxxxxx = nombre que quermos darle al post

3. El archivo tiene que seguir el siguiente formato de ejemplo (no meter los comentarios que pongo en el ejemplo), las etiquetas de titulo, author, tags, etc van entre dos cadenas "---":
    ```
    ---
    title: Example protected page     # El titulo del post
    layout: protected                 # Solo poner esta etiqueta si es un post con contraseña
    password: s00pers3cr3t            # Contraseña del post (solo si tiene layout protected)
    author: BinaryShadow              # Quien es el autor
    tags: HTB Writeup                 # Etiquetas para buscar el post (separadas por espacios)
    ---
    
    # This content is served encrypted
    <img src="{% base64 images/w4h.png %}" /> 
    You can use *markdown* as always.
    ```
4. Una vez escrito el post ejecutamos desde la carpeta raiz del repositorio el siguiente comando "jekyll build"

    Si es la primera vez que generais un post necesitareis ejecutar los siguientes comandos para tener jekyll y las dependencias instaladas en vuestra máquina antes de construir la web:
    ```?
    sudo apt-get install ruby-full build-essential zlib1g-dev
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
    gem install jekyll bundler
    ```

5. Para ver que todo se visualiza correctamente podeis ejecutar un servidor http con python3 en el directorio **_site** y verlo desde vuestro localhost.
    ```
    sudo python3 -m http.server 80
    ```

6. Si todo esta correcto, copiamos el contenido de la carpeta **_site** a la raiz del repositorio publico https://github.com/Watch4Hack/Watch4Hack.github.io.

7. Hacemos commit de ambos repositorios y push.

8. Ya tenemos el nuevo contenido disponible en la web. (https://watch4hack.github.io)

# Tricks
* Para poner contraseña en los post utilizar las siguientes etiquetas (perfecto para writeups de maquinas activas, cuando ya se retiren solo debemos quitar las etiquetas y estarán sin contraseña):
    *  layout: protected
    *  password: xxxxxxxxxxxx -> cambiar por la contraseña del post

* Para que las imagenes queden codificadas en base64 tenemos que guardarlas en el directorio **images** y añadirlas al post con el siguiente formato (el directorio images no se genera en la web estatica):
    ```\<img src="{% base64 images/w4h.png %}" />```
    
Más info: https://jekyllrb.com/docs/ https://tianqi.name/jekyll-TeXt-theme/docs/en/quick-start
