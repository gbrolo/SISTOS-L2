# SISTOS-L2
Sistemas Operativos, S.10 2018 - Laboratorio 2

## Respuestas

### Ejercicio 1
* ¿Qué puede ver en el output cuando realiza estas acciones? Se puede observar el ID de los distintos procesos que corren en un determinado momento en el sistema. El proceso ```swapper``` es el que mas aparece.

* ¿Para qué sirve SystemTap? Sirve para recolectar informacion sobre el sistema de Linux (el kernel en vivo) que este corriendo, lo que ayuda a diagnosticar posibles problemas de rendimiento o funcionales.

* ¿Qué es una probe? Se puede considerar como un objeto utilizado para ver dentro de algo mas, con el fin de encontrar la realidad o verdad de que se encuentra escondido dentro de algo. Por esto mismo, una probe puede inicializar hardware, recolectar recursos y registrar al objeto con el kernel.

* ¿Cómo funciona SystemTap? Es un wrapper alrededor de gcc y kprobes. Systemtap traduce el script en codigo para un modulo Kernel de C, compila y carga el modulo y utiliza kprobes para interceptar los puntos solicitados. Kprobes se encarga de realizar los probes para analizar los procesos y luego se realiza el profiling.

* ¿Qué es hacer profiling? Es un proceso que involucra analizar dinamicamente programas/procesos/kernel con el fin de medir el espacio en memoria, tiempo o complejidad (cuando se habla de programas), asi como se busca medir el uso de un conjunto particular de instrucciones o la frecuencia y duracion de las llamadas a sistema. Esto sirve para optimizar el programa/proceso.

### Ejercicio 2

* ¿Cuál es la diferencia entre un método que no recibe parámetros y uno que recibe void? Una funcion sin parametros, i.e. ```func()``` significa que sera una funcion que tomara una cantidad sin especificar de argumentos de un tipo sin especificar, mientras que una funcion que recibe ```void```, i.e. ```func(void)``` significa que sera una funcion que no tomara argumentos.

* ¿Qué diferencia hay entre printk y printf? ```printk()``` es una funcion a nivel de kernel, que tiene la habilidad de imprimir diferentes loglevels, tal y como se define en ```<linux/kernel.h>```. ```printf()``` siempre imprimira a un ```file descriptor``` - ```STD_OUT```. Por esto, la mayor diferencia es la capacidad de ```printk()``` para especificar un loglevel; el kernel utiliza este loglevel para decidir si imprimir un mensaje a la consola. El kernel despliega todos los mensajes con un loglevel debajo de un valor especificado en la consola.

* ¿Qué es y para qué sirve KERN_INFO? ```KERN_INFO``` es un loglevel de la funcion ```printk()``` en C. Tiene valor numerico 6 y sirve para desplegar "alguna informacion".

* ¿Qué se está haciendo con la definición de meta (goal definition) obj-m? Esto le dira a kbuild que existe un objeto en ese directorio llamado ```simple.o```. Este sera construido desde ```simple.c```. Asimismo, ```simple.o``` sera construido como un modulo.

* ¿Qué función tienen las líneas all: y clean:? ```all``` sirve para que ```make``` construya todo lo que sea necesario para realizar un build completo. ```clean``` sirve para limpiar los archivos objeto.

* ¿Qué hace la opción –C en este Makefile? ```-C``` es para compilar.

* ¿Qué hace la opción M en este Makefile? ```M``` sirve para decirle a make que hara un modulo externo.

* ¿Para qué sirve dmesg? Este comando se utiliza para escribir los mensajes kernel en Linux al ```standard output```, que por default es la pantalla. ```dmesg``` obtiene la data al leer el ```kernel ring buffer```.

* ¿Qué hace la función simple_init en su programa simple.c? Solamente cargara el modulo del programa hecho.

* ¿Qué hace la función simple_exit en su programa simple.c? Remueve o quita el modulo en ejecucion. En otras palabras, descarga el modulo de Linux.

* Usted ha logrado crear, cargar y descargar un módulo de Linux. ¿Qué beneficio tiene el poder ejecutar código de esta forma? Tiene el beneficio que se puede crear el modulo cuando se desee hacerlo y cargarlo solamente cuando sea necesario utilizarlo. Luego, se descarga para evitar utilizarlo cuando no sea necesario y asi ahorrar otros recursos necesarios para otros procesos. Luego se podria volver a cargar si se necesitara.

### Ejercicio 3

* Link simbolico: ```ata-VBOX_HARDDISK_VB9e51fc84-cfbdba3a```

* Contenido de ```<file system>```: ```UUID=5f2e2232-4e47-4fe8-ae94-45ea749a5c92```

* ¿Qué es y para qué sirve el archivo fstab? Es el ```system table``` del sistema operativo. Este archivo se utiliza para definir como las particiones, bloques o sistemas de archivos que son remotos deberian de ser montados e intregados en el sistema Linux.

* ¿Qué almacena el directorio /etc? ¿En Windows, quién (hasta cierto punto) funge como /etc? En los sistemas Unix modernos, casi todos los archivos de configuracion del sistema se encuentran en ```/etc```. Sin embargo, este directorio contendra tambien todos los archivos que no esten incluidos en ```/bin```, ```/dev```, ```/lib``` o ```/usr```. En Windows, podria decirse que esta funcion la cumple ```C:\ProgramData``` o bien ```C:\Users\<Username>\AppData```

* ¿Por qué se usa ```<la dirección completa del link hacia sda>``` en lugar de sólo ```/dev/sda```? Se utiliza esta direccion porque LILO necesita saber con exactitud el punto de partida en donde debera cargarse, es decir el Hard Drive.

* ¿Cuál  sería  la  diferencia  al  usar ```/dev/sdaN``` donde N es  un  número? Investigue y explique los conceptos de Master Boot Record(MBR) y Volume Boot Rercord(VBR). La diferencia seria que se estaria utilizando una particion exacta del disco en vez de utilizar al disco en si, entonces si hubiesen otras particiones con otros sistemas por ejemplo no se podria elegir entre ellos.

* ¿Qué es hacer chain loading? Chainloading es ir colocando en cadena las posibles opciones a elegir para sistema operativo, en el boot loader como Grub o Lilo, en orden segun se desee cual es el SO por defecto.

* ¿Dónde, históricamente, se encuentra la tabla de particiones que editamos, por ejemplo, con cfdisk durante la instalación de Knoppix(ver proyecto LFS)? Esta tabla de particiones se alojara en el directorio /etc

* ¿Qué   se   está indicando   con   la   configuración ```root=”<el  file  system anotado>```”? Se indica el tipo de sistema que debera cargarse en la raiz de la particion que correra al SO, por ejemplo si es ext4, swap o similar.

* ¿Qué es vmlinuz? es el nombre del kernel ejecutable de Linux

* Mencione tres diferencias funcionales entre GRUB y LILO. 

1. GRUB es un boot loader que puede usarse para Linux, vSTA, DOS u otros SO, mientras que LILO es un boot loader generico para Linux.

2. Tanto GRUB como LILO pueden bootear SO desde dispositivos externos como discos duros, pero GRUB permite bootear desde una red mientras que LILO no.

3. Cuando el archivo de configuracion se cambia, LILO necesita reinstalarse al MBR mientras que GRUB se va directo a su interfaz de linea de comandos.

### Screenshots
![1](https://github.com/gbrolo/SISTOS-L2/tree/master/img/1.png)
![2](https://github.com/gbrolo/SISTOS-L2/tree/master/img/2.png)
![3](https://github.com/gbrolo/SISTOS-L2/tree/master/img/3.png)
![4](https://github.com/gbrolo/SISTOS-L2/tree/master/img/4.png)
![5](https://github.com/gbrolo/SISTOS-L2/tree/master/img/5.png)
![6](https://github.com/gbrolo/SISTOS-L2/tree/master/img/6.png)
![7](https://github.com/gbrolo/SISTOS-L2/tree/master/img/7.png)
![8](https://github.com/gbrolo/SISTOS-L2/tree/master/img/8.png)
![9](https://github.com/gbrolo/SISTOS-L2/tree/master/img/9.png)
