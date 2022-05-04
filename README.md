# Instalacion y configuracion del servidor web Nginx : Virtual Hosts
### Para la instalación y configuración del servidor web Nginx en un equipo Linux, se lleva a cabo el siguiente proceso :

Lo primero de todo es instalar NGINX, para ello hay que usar el comando ``apt-get install nginx``

![instalacion1](https://user-images.githubusercontent.com/91699247/166102518-3e13cf38-b2c0-41d3-a7b1-3da4708818bc.png)


A través de nuestro navegador podemos comprobar si la instalación se ha realizado correctamente, si escribimos nuestra dirección ip o *localhost* nos debe aparecer la página de bienvenida de nginx.
![instalacion2](https://user-images.githubusercontent.com/91699247/166102526-f7e2c2d2-f462-4394-ac5f-f139825a5969.png)


Ahora procederemos a la configuración de nginx :

Primero hay que dirigirse al directorio del servidor nginx contenido en el directorio etc  `` cd /etc/nginx/`` . 

Dentro de este se encuentra *sites-available*, donde crearemos la configuración de los sitios, que están diferenciados por los *virtual hosts*. 

<img width="296" alt="sites-av1" src="https://user-images.githubusercontent.com/91699247/166122529-86eb3b75-2b95-444f-b4fe-bd32e0028c0e.png">

A continuación nos dirigimos a *sites-available* , donde encontraremos un único archivo llamado *default* , que contiene la configuración por defecto de nginx. 

![sites-av2](https://user-images.githubusercontent.com/91699247/166122954-a1ca7769-ca4a-4f97-9bd8-c90b41507bef.png)


Creamos dos nuevos archivos a partir de la copia de este archivo *default* de esta manera `` cp default subdominio.dominio `` 
![copy_def](https://user-images.githubusercontent.com/91699247/166122961-041a83f3-ba85-4c61-b73d-4c3ed8351dc3.png)


Todo seguido modificamos estos dos nuevos archivos que hemos creado, que se puede hacer mediante un `` sudo nano subdominio.js.com `` 
![edit1](https://user-images.githubusercontent.com/91699247/166123894-315f9e80-4399-4aa4-9d64-890d5359f71d.png)


El primero cambio se corresponde al ``server_name _;``, que debemos cambiar el ``_`` por el nombre de nuestro sitio . El segundo sería en root, donde se encuentran los archivos de nuestro sitio, hay que reemplazar ``html``  de ``root/var/www/html`` por el subdominio de nuestro sitio. Guardamos el archivo y salimmos.

![edit2 1](https://user-images.githubusercontent.com/91699247/166123943-be9ccb92-92cd-4712-8814-04704d389951.png)![edit2 2](https://user-images.githubusercontent.com/91699247/166123945-1a07df68-18e3-4799-9792-ec7d24d27c95.png)

Aparte de la anterior configuración mencionada, hay que modificar el servidor por defecto, eliminarlo ya que solo puede existir uno.

![edit_serv1](https://user-images.githubusercontent.com/91699247/166123998-406a1ee7-8e9a-4b8e-b574-310bef1ee01f.png)![edit_serv1 2](https://user-images.githubusercontent.com/91699247/166123999-28e44d4d-f01f-44bf-84f9-831610342e64.png)



Para activarlos nos dirigiremos a sites-enabled, donde vemos un link simbólico ( un archivo contenido en otro directorio ) , el servidor piensa que es encuentra en este directorio (*sites_available*), pero al no ser así debemos estabblecer el verdadero directorio . Esto creará un link simbólico del archivo contenido en *sites_available* y lo pondrá en *sites-enabled*.

Para ello escribimos ``ln -s /ruta/origen/archivo ruta/destino/archivo``

![ruta1](https://user-images.githubusercontent.com/91699247/166124060-381b7f1b-bbc0-4c7d-adfa-1b368116778b.png)![ruta2](https://user-images.githubusercontent.com/91699247/166124063-b68fdb9f-912a-4d93-8e63-00904c21ec97.png)

Con el objetivo de actualizar esta configuración que hemos hecho, debemos recargar nginx, lo haremos mediante el comando ``nginx -s reload``

Ahora podemos comprobar si con las direcciones de nuestros sitios podemos visualizar nuestros proyectos, para ello, estas deben apuntar a la ip del servidor. 
Para que esto se cumpla, debemos modificar el archivo *hosts*, que se encuentra en el directorio ``/etc`` .

Esta modificación la podemos llevar a cabo mediante un `` sudo nano hosts`` y queda de esta manera :
![Captura desde 2022-05-04 22-58-39](https://user-images.githubusercontent.com/91699247/166825209-4ca749de-1d11-4913-b3df-312cb5ce8bfd.png)



Escribimos la dirección de nuestro sitio en el navegador y vemos que sale el error de que no encuentra nuestra página 

![404 1](https://user-images.githubusercontent.com/91699247/166125188-c27d8dec-084a-4003-bec1-7ec83a05735b.png)


Esto lo podemos solucionar creando los directorios con los nombres que especificamos en root en la configuración del server al inicio del proceso :

![mkdir1](https://user-images.githubusercontent.com/91699247/166125217-fb0b945f-de0e-4bc5-8053-da05f2ee119e.png)


Dentro de estos directorios, insertamos en el correspondinete archivo html el código del proyecto elegido
![index1](https://user-images.githubusercontent.com/91699247/166703200-4afd85c7-5813-41df-a1fd-bfbcae0c23e7.png)
![index2](https://user-images.githubusercontent.com/91699247/166703221-55760546-a586-462b-8935-7cacda6ca696.png)
![index3](https://user-images.githubusercontent.com/91699247/166703242-9615cf2a-6322-40d5-8618-5ea3e4478b0c.png)



Ya podemos desplegar los proyectos, cada uno con su correspondiente subdominio 
![ping](https://user-images.githubusercontent.com/91699247/166125290-77e241bc-084c-45a7-8c7b-87c13f63b5c7.png)![meat](https://user-images.githubusercontent.com/91699247/166125291-0815e61a-a984-4ce0-be7a-c34ef5009763.png)



