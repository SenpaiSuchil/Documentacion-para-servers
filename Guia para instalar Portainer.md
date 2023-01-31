- --

### Herramienta para gestionar docker desde una interfaz web
- --
![200](https://i.pinimg.com/originals/de/8d/e8/de8de8bbfc4d8f2193913611aca6b00f.jpg) 

###### Desripción:
_Portainer es una herramienta web open-source que permite gestionar contenedores Docker.​ Permite administrar contenedores de forma remota o local, la infraestructura de soporte y todos los aspectos de las implementaciones de Kubernetes, Docker standalone y Docker Swarm._

###### ¿porque escoger portainer?
_En mi opinion personal esta herramienta es de mucha ayuda para ahorrar tiempo al momento de crear contenedores, llevar registro y administrar todo lo relacionado con contenedores o stacks de contenedores, gracias a su interfáz web permite hacer deploy en segundos sin tanto problema con comandos._

###### Recomendación:
_Es altamente recomendable (solo porque no puedo obligar a nadie) que la persona que lea esta tremenda documentación se haya familiarizado con el uso de docker desde consola, ya que como siempre puede que haya sistemas donde no tengan esta herramienta y tenga que hacerlo todo de la manera fea que es por consola, despues de bajar algunas imagenes, crear las suyas y hacer algunos contenedores y ver como trabajan en su totalidad, instale Portainer con esta guia practica claro que si_


## Instalación
- ---

lo importante aqui es tener en claro que existen algunos inconvenientes con los puertos ya que portainer usa http y no https asi que en otros tutoriales se vera como proteger la integridad de esos puertos si es necesario.

lo prinicipal para la instalacion es saber tambien que esto correra en un docker asi que el primer requerimiento es que tu servidor tenga instalado docker como servicio (aqui un comando para debian, sino tiene debian pues jaja que perdedor ahí busquele como es en su distro mafufa):

 ```shell
apt update
apt install docker
apt install docker-compose-plugin
```


una vez con docker instalado vamos a escribir una serie de comandos.

el primero es para crear un volumen de _persistant storage_ y ahi pueda guardar los datos (no voy a meterme mucho en esto ya debiste de haber estudiado que pasa si no configuras persistant storage para un docker bruh).

el segundo es el importante ya que lleva toda la configuración del contenedor que vamos a correr, puede que si es la primera vez que corres el comando tarde un poco porque docker necesita bajar la imagen de sus repositorios.

```shell
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

a primera vista se ve como una groseria pero vamos a revisarlo parte por parte:
- <font color="purple">docker run</font>: es el comando para ejecutar un contenedor
- <font color="purple">-d</font>: es para activar la bandera _detach_ y que al ejecutar el contenedor no nos meta al contenedor en si y podamos seguir con nuestra vida dentro de nuestra querida consola de linux
- <font color="purple">-p</font>: sirve para que el docker sea expuesto por un puerto, en este caso el 8000 y el 9000
- <font color="purple">--name</font>: pues para ponerle nombre man es que de verdad ni porque el nombre lo dice
- <font color="purple">--restart</font>: son las condiciones para que el docker se inicie despues de una reiniciada (un init 6 del horror) del sistema.
- <font color="purple">-v</font>: stands for _volume list_ que es donde debemo de especificar en que directorio de la maquina real, el primer -v establece que el contenedor puede acceder a las funciones del _docker daemon_ y esto permite que portainer pueda administrar contenedores, imagenes, volumenes, etc. vaya, que sirve para que portainer pueda crear contenedores y eliminarlos y demás, esa es la parte del comando que le da poder, el segundo solo le dice cual es su volumen donde debera de guardar cosas, este es el persistant storage.

### Post-instalación
- ---

una vez instalado dirijase a su navegador y escriba:
- ip de su server:9000
que se veria algo como:
192.168.100.2:9000

la primera vez que inicies te pedira que configures la cuenta del administrador
recomiendo que cambies el nombre de _admin_ a otro que no sea tan faci de adivinar por cuestiones de seguirdad.

y con eso ya tiene su configuraciń basica de portainer.
