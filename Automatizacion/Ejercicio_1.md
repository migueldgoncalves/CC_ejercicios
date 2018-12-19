# Automatización - Ejercicio 1

En este ejercicio se ha utilizado el Azure classic CLI para crear una máquina virtual en Azure, donde después se ha instalado un servidor Nginx para se acceder a la máquina virtual via HTTP.

Después de instalar el Azure classic CLI con el comando `npm install -g azure-cli` (hay que instalar node.js préviamente), de hacer login en Azure y de elegir la suscripción a utilizar, se ha creado una máquina virtual en Azure utilizando el comando

```
azure vm create hito4 b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-16_04_0-LTS-amd64-server-20180814-en-us-30GB miguel Llave01! --location "France Central" --ssh
```

donde `hito4` es el nombre de la máquina, que se poderá acceder en la dirección `hito4.cloudapp.net`; `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-16_04_0-LTS-amd64-server-20180814-en-us-30GB` es el nombre de la imágen a utilizar, en este caso con el sistema operativo `Ubuntu Server 16.04.0-LTS`; `miguel` es el nombre del superusuario de la máquina; `Llave01!` es la llave que se utilizará para la conexión SSH con la máquina; y `France Central` es el centro de datos donde se creará la máquina. La flag `--ssh` es necesaria para permitir la conexión vía SSH con la máquina virtual.

Mirar [aquí](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje1_imagenes/Ejercicio1_1.png) el resultado de la ejecución del comando de creación de la máquina virtual.

Una vez creada, la máquina ha sido arrancada utilizando el comando `azure vm start hito4`. Se ha entonces conectado con la máquina vía SSH usando el comando `ssh hito4.cloudapp.net`, y actualizádola con el comando `sudo apt full-upgrade`.

En seguida, un servidor Nginx ha sido instalado en la máquina virtual con el comando `sudo apt install nginx`, cuyo resultado se puede mirar [aquí](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje1_imagenes/Ejercicio1_2.png). El siguiente paso ha sido abrir el puerto 80 de la máquina virtual al público, lo que se ha hecho con el comando `azure vm endpoint create hito4 80`, cuyo resultado se puede mirar [aquí](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje1_imagenes/Ejercicio1_3.png).

El último paso ha sido abrir el puerto 80 del servidor Nginx al mundo, lo que se ha hecho con el comando `sudo ufw allow 'Nginx HTTP'`. Hecho eso, la conexión a la máquina virtual vía HTTP se tornó posible, y al acceder a `hito4.cloudapp.net` se ha accedido con suceso a la página inicial de Nginx, cómo se puede ver [aquí](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje1_imagenes/Ejercicio1_4.png).
