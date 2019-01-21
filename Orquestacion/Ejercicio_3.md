# Ejercicio 3

El objetivo del ejercicio fue crear un script para provisionar de forma básica una máquina virtual para mi proyecto de la asignatura.

Así, he creado un [script](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_3_files/script) que instala Java, Git y Maven en una máquina, necesarios para mi proyecto. Enseguida, he creado un [Vagrantfile](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_3_files/Vagrantfile) que utiliza la box `gbarbieru/xenial` de Vagrant presente en el enlace [https://atlas.hashicorp.com/gbarbieru/boxes/xenial] para crear una máquina con sistema operativo Ubuntu 16 Server, provisionándola con el script indicado que he puesto en el Desktop.

La comprobación del correcto provisionamiento de esa máquina virtual se puede ver [aquí](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_3_files/Ejercicio_3_1.png) y [aquí](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_3_files/Ejercicio_3_2.png).
