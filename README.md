<div align = "justify">

# Instalación de JDK en el SO

- Instalación del JDK en el Ubuntu

## Indice

- [¿Cómo instalar Java en Ubuntu desde repositorios?](#instalar)
- [¿Cómo instalar una versión específica de Java?](#version-especifica)
- [Configuración de las variables de entorno](#configuracion)

## Introduccion
Introducción

Java sin dudas es un lenguaje de programación que es utilizado para diversos propósitos y es un complemento casi esencial para la ejecución y funcionamiento de diversas herramientas, la instalación de java es prácticamente una tarea esencial después de haber realizado la instalación de este.

Es por ello que en esta ocasión compartiré con ustedes un sencillo tutorial de como instalar Java en nuestro sistema con el JDK el cual es un entorno de desarrollo y el entorno de ejecución JRE.

## ¿Cómo instalar Java en Ubuntu desde repositorios? <a name = "instalar"></a>

- Por defecto ya tengo instalado una version de Java en mi MV:
   ```code
   atprodriguez@atprodriguez-VirtualBox:~$ java --version 
   openjdk 11.0.19 2023-04-18
   OpenJDK Runtime Environment (build 11.0.19+7-post-Ubuntu-0ubuntu122.04.1)
   OpenJDK 64-Bit Server VM (build 11.0.19+7-post-Ubuntu-0ubuntu122.04.1, mixed mode, sharing)
   ```

## ¿Cómo instalar una versión específica de Java? <a name = "version-especifica"></a>
- **OpenJDK**:  
- *11*
```code
sudo apt install openjdk-11-jdk
```

  - Salida (tras instalarlo):
    ```code
    atprodriguez@atprodriguez-VirtualBox:~$ sudo apt install openjdk-11-jdk
    [sudo] contraseña para atprodriguez:              
    Leyendo lista de paquetes... Hecho
    Creando árbol de dependencias... Hecho
    Leyendo la información de estado... Hecho
    openjdk-11-jdk ya está en su versión más reciente (11.0.20.1+1-0ubuntu1~22.04).
    0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 201 no actualizados.
    ```
- *13*
```code
sudo apt install openjdk-13-jdk
```
  - salida:
    ```code
    atprodriguez@atprodriguez-VirtualBox:~$ sudo apt install openjdk-13-jdk
    Leyendo lista de paquetes... Hecho
    Creando árbol de dependencias... Hecho
    Leyendo la información de estado... Hecho
    E: No se ha podido localizar el paquete openjdk-13-jdk
    ```
- *8*
```code
sudo apt install openjdk-8-jdk
```
  - Salida (tras instalarlo):
    ```code
    atprodriguez@atprodriguez-VirtualBox:~$ sudo apt install openjdk-8-jdk
    Leyendo lista de paquetes... Hecho
    Creando árbol de dependencias... Hecho
    Leyendo la información de estado... Hecho
    openjdk-8-jdk ya está en su versión más reciente (8u382-ga-1~22.04.1).
    0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 201 no actualizados.
    ```

La versión que se debe de trabajar es la versión 8. Para ello verificaremos la versión de java que se esta ejecutando con la sentencia:
```code
java --version
```
- Salida:
```code
atprodriguez@atprodriguez-VirtualBox:~$ java --version
openjdk 11.0.20.1 2023-08-24
OpenJDK Runtime Environment (build 11.0.20.1+1-post-Ubuntu-0ubuntu122.04)
OpenJDK 64-Bit Server VM (build 11.0.20.1+1-post-Ubuntu-0ubuntu122.04, mixed mode, sharing)
```
En caso que no se ejecuta la versión 8 se debe configurar las variables de entorno.

## Configuración de las variables de entorno <a name = "configuracion"></a>
El siguiente paso consiste en establecer las variables de entorno. Es necesario porque cuando se usa Java, Linux necesita saber dónde está ubicado el programa para ejecutarlo y qué versión de Java usar de forma predeterminada. Para modificar esto, usaremos el editor de texto nano. Primero, abra el archivo en Nano.

### Listar la versiones de OpenJDK instaladas
Ejecuta el siguiente comando para verificar que se han descargado las diferentes versiones de OpenJDK.
```code
ls /usr/lib/jvm
```

- salida:
```code
atprodriguez@atprodriguez-VirtualBox:~$ ls /usr/lib/jvm
default-java               java-11-openjdk-amd64     java-8-openjdk-amd64
java-1.11.0-openjdk-amd64  java-1.8.0-openjdk-amd64  openjdk-11
```

### Actualización de las variables de entorno
Edita y modifica el fichero profile, con los comandos:
```code
sudo update-alternatives --config java
```
y selecciona la version 8.

- salida:
```code
atprodriguez@atprodriguez-VirtualBox:~$ sudo update-alternatives --config java
[sudo] contraseña para atprodriguez:              
Existen 2 opciones para la alternativa java (que provee /usr/bin/java).

  Selección   Ruta                                            Prioridad  Estado
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      modo automático
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      modo manual
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      modo manual

Pulse <Intro> para mantener el valor por omisión [*] o pulse un número de selección: 2
update-alternatives: utilizando /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java para proveer /usr/bin/java (java) en modo manual
```
Otra opción es : añadir el siguiente código:
```code
# Java version
JAVA_HOME=/usr/lib/jvm/(SELECCIONA UN PATH DE LA VERSION QUE DESEAS QUE SE EJECUTE)
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
export JAVA_HOME
export JRE_HOME
export PATH
```
en

```code
/etc/profile.d/java.sh
```
- salida:
```code              
atprodriguez@atprodriguez-VirtualBox:~/Escritorio/jdk$ sudo nano /etc/profile.d/java.sh
```
Haga que el script sea ejecutable con chmod:
```code
sudo chmod +x /etc/profile.d/java.sh
```
- salida:
```code
atprodriguez@atprodriguez-VirtualBox:~/Escritorio/jdk$ sudo chmod +x /etc/profile.d/java.sh
```
Finalmente, cargue las variables de entorno usando el comando de source
```code
source /etc/profile.d/java.sh
```
- salida: 
```code
atprodriguez@atprodriguez-VirtualBox:~/Escritorio/jdk$ source /etc/profile.d/java.sh
```
- Comprobar la versión de Java con:
```code
java -version
```
- salida:
```code
atprodriguez@atprodriguez-VirtualBox:~$ java -version
openjdk version "1.8.0_382"
OpenJDK Runtime Environment (build 1.8.0_382-8u382-ga-1~22.04.1-b05)
OpenJDK 64-Bit Server VM (build 25.382-b05, mixed mode)
```
</div>