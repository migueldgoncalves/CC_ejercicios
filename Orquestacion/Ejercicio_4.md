# Ejercicio 4

El objetivo de este ejercicio fue provisionar una maquina virtual creada con Vagrant utilizando Ansible.

Así, se ha utilizado este [Vagrantfile](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_4_files/Vagrantfile) para crear en Azure una máquina virtual con el sistema operativo Ubuntu 16 Server, así como para provisionarla posteriormente con Java, Git y Maven utilizando este [playbook de Ansible](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_4_files/playbook.yml), como se hacía en el [ejercicio anterior](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_3.md) con recurso a un [script](https://github.com/migueldgoncalves/CC_ejercicios/blob/master/Orquestacion/Ejercicio_3_files/script).

Antes de ejecutar el Vagrantfile, se ha ejecutado el siguiente comando para añadir una box dummy a Vagrant, necesaria para crear maquinas virtuales en Azure:

```
vagrant box add unaboxdummy https://github.com/azure/vagrant-azure/raw/v2.0/dummy.box --provider azure
```

donde `unaboxdummy` es un cualquier nombre que identificará la box dummy.

También se ha instalado el [plugin](https://github.com/Azure/vagrant-azure) de Vagrant para integración con Azure, con el comando `vagrant plugin install vagrant-azure`.

Antes de ejecutarse el Vagrantfile, se ha creado un [Azure Active Directory service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals) para ser utilizado por Vagrant al conectarse con Azure con el comando `az ad sp create-for-rbac`. El output de este comando, más el output del comando `az account list`, permitieron obtener los valores para las variables de entorno `AZURE_TENANT_ID`, `AZURE_CLIENT_ID`, `AZURE_CLIENT_SECRET` y `AZURE_SUBSCRIPTION_ID`, que se crearon antes de ejecutarse el Vagrantfile.

Por fin, con el Vagrantfile y el playbook de Ansible `playbook.yml` en un mismo directorio, y un fichero de llave privada `id_rsa` en el directorio por defecto `~/.ssh`, se ha ejecutado el Vagrantfile con el comando `vagrant up`.

Fuentes principales:

https://blog.scottlowe.org/2017/12/11/using-vagrant-with-azure/

https://github.com/Azure/vagrant-azure

https://www.vagrantup.com/docs/provisioning/ansible.html
