# Automatización - Ejercicio 2

## Preparación

Antes de ejecutar el script de creación y provisionamiento de una máquina virtual en Azure, hay que instalar el Azure CLI (su versión más moderna, no el Azure classic CLI) y iniciar sesión en él, elegindo la suscripción que se quiere utilizar para crear la máquina virtual.

Hay que tener un par de llaves SSH ya creadas, incluso es más seguro crear un par de llaves específicamente para este ejercicio. Si se está realizándolo en Ubuntu 16, se tendrá que añadir el siguiente contenido al fichero ~/.ssh/config:

```
Host ccazure.francecentral.cloudapp.azure.com
  StrictHostKeyChecking no
```

dado que en cada arranque o creación de raíz la máquina tendrá una dirección IP diferente, por lo que hay que deshabilitar el strict host key checking con estas líneas para permitir la conexión con la máquina virtual.

Por último, es necesario instalar Ansible. Asumiendo que se lo ha instalado en su carpeta por defecto `/etc/ansible` y que se está en Ubuntu 16, hay que añadir un fichero `playbook.yml` a ese directorio con este [contenido](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje2_documentos/playbook.yml).

## Creación y provisionamiento de la máquina virtual

Para crear y provisionar una máquina virtual Debian en Azure se ha creado y utilizado el siguiente script:

```
#!/bin/bash

az group create -l francecentral -n CCGroup
az vm create -g CCGroup -n CCazure --image Debian --ssh-key-value <public_key>
az vm start -g CCGroup -n CCazure
az vm open-port -g CCGroup -n CCazure --port 80 --priority 100
az vm open-port -g CCGroup -n CCazure --port 22 --priority 110
az network public-ip update -g CCGroup -n CCazurePublicIp --dns-name ccazure --allocation-method Dynamic
ansible-playbook /etc/ansible/playbook.yml
```

Para ejecutarlo, hay que crear un fichero llamado `acopio.sh` que esté vacío en una ubicación cualquier y copiar en él el script arriba. Hay que dar permiso de ejecución del fichero como programa, en Ubuntu 16 esto se hace pulsando con el botón derecho del ratón en el fichero; seleccionando la pestaña Permisos; y en ella la opción Permitir Ejecución de Fichero enquanto Programa. Mirar una ilustración [aquí](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje2_documentos/Ejercicio2_3.png).

El último paso antes de la ejecución del script es copiar al campo <public_key> la llave pública que se desea utilizar; en Ubuntu 16 las llaves SSH por defecto están en el directorio `~/.ssh`, donde las llaves públicas están en ficheros `.pub`. Abrir el fichero deseado, por ejemplo con `sudo gedit <nombre_del_fichero>`, y copiar todo su contenido para el campo <public_key> del script. Es crucial que la llave esté entre comillas simples, `''`, de otro modo el script no funcionará.

Por fin, ejecutar el script abriendo un terminal en el directorio donde esté el script y correr el comando `./acopio.sh`, si se está en Ubuntu 16.

El script tardará cerca de 6 minutos a ejecutar completamente. Irá crear un grupo de recursos necesarios para la máquina virtual, después la própria máquina virtual Debian. En seguida la arrancará, abrirá sus puertos 22 (SSH) y 80 (HTTP) al mundo, y añadirá un nombre DNS `ccazure` para que se pueda acceder a la máquina independientemente de su dirección IP. Por fin, ejecutará el playbook de Ansible `playbook.yml`, el cual instalará el Java 8, Git y Maven en la máquina virtual.

El output inicial de la consola deberá ser parecido a [esto](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje2_documentos/Ejercicio2_1.png), y la ejecución del script deberá tener este [aspecto](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Automatizacion/eje2_documentos/Ejercicio2_2.png).
