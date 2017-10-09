### Examen 1
**Universidad ICESI**  
**Curso:** Sistemas Operativos  
**Docente:** Daniel Barragán C.  
**Tema:** Comandos de Linux, Virtualización  
**Correo:** daniel.barragan at correo.icesi.edu.co  
**Estudiante:** Ana Valderrama  
**Código:** A00065868  


### Objetivos
* Conocer y emplear comandos de Linux para la realización de tareas administrativas
* Virtualizar un sistema operativo
* Conocer y emplear capacidades de CentOS7 para la vitualización

### Prerrequisitos
* Virtualbox o WMWare
* Máquina virtual con sistema operativo CentOS7

### Descripción
El primer parcial del curso sistemas operativos trata sobre el manejo de los comandos de Linux, virtualización y el uso de las características de CentOS7

### Actividades
1. Incluir nombre, código (5%)
2. Ortografía y redacción cuando sea necesario (5%)
3. Resuelva los siguienes retos de la página https://cmdchallenge.com y presente la solución a cada uno de ellos a través de un ejemplo práctico en CentOS7. Presente capturas de pantalla relevantes como evidencias de lo realizado (20%)
  * sum_all_numbers
  * replace_spaces_in_filenames
  * reverse_readme
  * remove_duplicated_lines
  * disp_table
4. Realice un script que cumpla las condiciones que se describen a continuación. Presente capturas de pantalla relevantes como evidencias del funcionamiento (30%)
  * El usuario gutenberg debe existir en el sistema operativo
  * El script se debe ejecutar cada 5 minutos, consulte el manual de crontab
  * EL script debe descargar un libro del proyecto https://www.gutenberg.org/ en el directorio /home/gutenberg/mybooks
  * Si ya existe un libro en el directorio mybooks, debe ser reemplazado  
5. Describa el funcionamiento del código fuente rickroll.c del repositorio de github https://github.com/jvns/kernel-module-fun. Muestre el funcionamiento al compilar el código y cargarlo como un módulo del kernel a través de un video que deberá cargar en Youtube e incluir el enlace en el informe (30%). Se recomienda emplear el sistema operativo Ubuntu con interfaz gráfica para esta prueba.
6. El informe debe ser entregado en formato pdf a través del moodle y el informe en formato README.md debe ser subido a un repositorio de github. El repositorio de github debe ser un fork de https://github.com/ICESI-Training/so-exam1 y para la entrega deberá hacer un Pull Request (PR) respetando la estructura definida. El código fuente y la url de github deben incluirse en el informe (10%)  

**Informe Solución**  
**3.** La página https://cmdchallenge.com propone unos retos en la consola virtual, pero no sólo fueron resueltos ahí sino que también se llevaron a cabo con ejemplos prácticos en CentOS7.
Así,  
- **sum_all_numbers:**  
El primero consistía en sumar los números contenidos en un archivo txt, en la consola virtual se empleó el filtro de jq especial para archivos JSON que es bastante útil en diferentes casos, como parámetro opcional se empleó -s que coloca todas las entradas de un archivo en un arreglo, el comando add realiza la suma de los elementos contnidos en el arreglo, arrojando la respuesta que necesito.  
![][1]
Para ejecutarlo en CentOS7 fue necesario primero ejecutar una líneas para instalar el filtro:
yum install epel-release -y
yum install jq -y
Luego, cree una carpeta **parcial** que contiene un archivo de texto sum-me.txt, este archivo contiene números enteros (uno por línea) elegido al azar, luego de esto es posible ejecutar la misma linéa que se ejecutó en la consola virtual de la página web.
jq -s add sum-me.txt  
![][2]  
  
- **replace_spaces_in_filename:**  
Este reto consistía en eliminar los espacios que existían en los nombres de los archivos, se podía hacer de diferentes maneras con el comando rename o con el comando tr, yo emplee este último que traduce, comprime y/o borra caracteres de la entrada estándar, escribiendo el resultado en la salida estándar, sustiyendo el espacio por un punto.  
En la consola virtual,  
![][3]  
En CentOS7, cree varios directorios con espacios en sus nombres para ello fue necesario colocar un backslash después del la primera palabra y antes del espacio, debido a que si se coloca solo el espacio se crean directorios diferentes por cada palabra, para mostrar cada directorio en una linea se empleo ls -1 y luego | para seguir con el comando tr (hacer pipeline, varias instrucciones), como se observa en la siguiente ilustración,   
![][4]  
  
- **reverse_README:**   
Este reto consitía en invertir las líneas de un archivo README que se encontraba en la consola virtual, en ambas soluciones (la realizada en la consola virtual de la página y la realizada en CentOS7) se empleó el comando tac que escribe el fichero pasado por parámetro iniciando por la última línea y terminando con la primera.  
En la consola virtual,  
![][5]  
![][6]  
![][7]  

En CentOS7, se creó una carpeta reverse en la carpeta parcial, y dentro de esta carpeta se creó un archivo txt ('alreves.txt'), y se ejecutó el comando tac.  
De la siguiente forma:  
![][8]  

- **remove_duplicated_lines:**  
Este reto consistía en eliminar las líneas repetidas de un archivo, al investigar se encontró que lo que generalmente se hace es ordenarlas con el comando sort y seguido a eso se emplea el comando uniq -u que imprime las líneas sin repetirlas, en un determinado orden, en este caso no era conveniente ordenar, entonces se empleó el comando cat con el nombre del archivo correspondiente para ver el archivo seguido (|) de el comando awk '!x[$0]++', que lee una línea a la vez buscando que la linea (que no este vacía) no se repita.  
En la consola virtual,  
![][9]  
![][10]  
En CentOS7 se creó un archivo de texto en la carpeta parcial (duplicadas.txt), escribiendo varias líneas repetidas, y ejecutando los comandos tal cual se ejecutaron en la página:  
![][11]  
  
- **disp_table:**  
El último reto consistía en crear una tabla apartir de un archivo de texto cuyas lineás estan todas conformadas por tres palabras separadas por ',', se emplearon tres comandos , cat para ver el resultado del archivo, tr que como se mencionó anteriormente sustituye caracteres, sustituyendo la ',' en en caso del ejercicio web y '/' en el caso de CentOS7 por '\t' que introduce un tab y por último el comando column -t para crear la tabla con el archivo actual.  
En la consola virtual,  
![][12]  
![][13]  
En CentOS7,  
![][14]   
  
  
**4.** En este punto se requería generar un script, que descargara un libro del proyecto https://www.gutenberg.org/ y lo almacenara en el directorio /home/gutenberg/mybooks, para esto se realizó lo siguiente:
- Primero se creó el usuario gutenberg desde root con el comando adduser y se le asignó una contraseña con el comando passwd gutenberg,  
![][15]  
-Luego de crear el usuario gutenberg se accedió a él, y se creó la carpeta mybooks donde posteriormente se almacenará el libro descargado del proyecto.  
-Desde el usuario root se creó una carpeta scripts, que va a contener el script a ejecutar, se crea el script downloadbook.sh con el comando vi, el script contiene una breve descripción al inicio lo más importante es la línea que aparece en primer lugar, que permite que se pueda ejecutar más adelante y es: #!/bin/bash, debido a que el proyecto Gutenberg cuenta con una biblioteca muy amplia de libros, se genera un número aleatorio entre 1 y 1500, con el comando RANDOM, y se introduce el número sobre el URL que va a descargar los libros. Se emplea el camando rm -f (Archivo-Directorio) para que borre el archivo que se esta pasando como parámetro incluso si no existe (por eso -f/ un posible libro), luego con el comando wget (DirectorioDestino) (URLOrigen) se extrae el libro de la web, con este comando se empleó el parámetro -O para descargar el archivo de texto plano en un directorio específico y con un nombre específico.  
![][16]  
Existencia del directorio /home/gutenberg/mybooks,  
![][17]  
-Luego, para que este script sea ejecutado cada cinco minutos fue necesario consultar Crontab, que es un archivo que contiene instrucciones para que un comando se ejecute en una fecha, los comandos se ejecutarán en el usuario en donde crontab se encuentre, en este caso todo lo hice desde el usuario root, crontab es el programa que ejecuta cron daemon y muestra todas las actualizaciones como correos en /var/spool, los cron jobs son tareas que se ejecutan periodicamente, lo que es muy útil si se necesita ejecutar un script varias veces, como en este caso. el formato de crontab esta compuesto por 6 columnas, las primeras 5 detallan el tiempo en el que se va a ejecutar el comando,el primer campo es el de los minutos por eso se empleó /5para que sea ejecutado cada 5 minutos, y la última contiene el comando a ejecutar en este caso el script.  
![][18]  
Después de haberlo editado, informa al usuario que los cambios en crontab serán aplicados luego de 5 minutos, la notificación del primer libro llegó:  
![][19]  
![][20]  
A los 5 minutos el siguiente:  
![][21]  
Se verificó que solo existiera un libro en la carpeta indicada, así:  
![][22]  
Algo que fue necesario para que el script corriera correctamente desde root, fue otorgarle todos los permisos a ese archivo, pues inicialmente llegó un mensaje avisando el acceso denegado al script. Se empleó chmod 777 downloadbook.sh, después de ejecutar ese comando los libros se descargaron con normalidad.  
  
  
**5.** En las referencias se encuentra un enlace de youtube (https://www.youtube.com/watch?v=efEZZZf_nTc) que está relacionado con el código fuente rickroll.c del repositorio https://github.com/jvns/kernel-module-fun/blob/master/rickroll.c , en el video de youtube se observa que apartir de la compilación y ejecución de un código que carga un modulo al kernel alterando la forma en la que se reproducen los archivos .mp3  reproduciendo una misma canción, *Never Gonna Give You - Rick Astley*.   
El código fuente en el repositorio funciona de la siguiente manera:  
En primer lugar se incluyen los módulos necesarios para extender funcionalidades del kernel, la inicialización y las llamadas al sistema, seguidamente se crean tres tipos de modulos: MODULE_LICENSE, MODULE_AUTHOR y MODULE_DESCRIPTION, estos módulos no son empleados por kernel exactamente se utilizan para informar al usuario caracteristicas del modulo, como su licencia, autor y qué hace.  
![][23]  

Seguidamente, se define la ruta que contiene la canción en formato .mp3 con la que se realizará el rickroll (la que reemplazará a todas las canciones en formato .mp3),  
![][24]    
Posteriormente, como se explica en el repositorio que contiene el código fuente se instancian dos módulos, la función de estos module_param y MODULE_PARAM_DESC es especificar el archivo que contiene al rickroll, los permisos que necesita el módulo y una breve descripción de la variable declarada en module_param,    
![][25]  
Se realizan después unas modificaciones al registro de control cr0 para poder modificar la tabla de llamados al sistema, debido a que ésta se encuentra protegida. Luego, el modificador asmlinkage le dice al compilador que en vez de buscar en los registros los llamados al sistema busque que pedirle al kernel en la  pila de la CPU, haciendo que cada vez que se busqué abrir un archivo .mp3 sea reemplazado por la cancion de *Astley*.  
![][26]  
En el método a continuación se inicializa el *rickrolling* modificando la tabla de llamadas al sistema, para que realice el truco, reemplazando la función normal por la del *rickrolling*, se realizan las verificaciones correspondientes como la de la existencia de un archivo para rickroll y  la de la tabla de llamados del sistema cuyo metodo también se encuentra en el código , informando las excepciones en caso de que las verificaciones no se puedan llevar a cabo.   
![][27]  
![][28]  
Luego de esto, ocurre realmente el *rickrolling*, esto es, el étodo que se llama en la inicalización, con el modificador asmlinkage se realiza el proceso de la apertura del archivo .mp3 reproduciendo la canción en cuestión, recibe la ruta del archivo, verifica que el archivo sea .mp3, en caso de no serlo realiza la llamada al sistema normal, en caso de serlo, va al kernel y cambia el segmento con el cual el generalmente realiza esta acción, cambiando la llamada al sistema y haciendo que cuando se abra el archivo se reproduzca *Never Give UP*.    
![][29]    
Existe un método que restaura el sistema, cambiando la tabla de llamadas al sistema, desactivando el *rickrolling*, teniendo en cuenta que necesario desactivar y activar la protección de escritura en memoria con las variables  DISABLE_WRITE_PROTECTION y ENABLE_WRITE_PROTECTION, que se usaron cada vez que era necesario alterar la tabla de llamados al sistema,   
![][30]  
Cabe aclarar que todo el código descrito anteriormente no podría ejecutarse sin la inicialización y cierre del driver que se realiza gracias a los modulos de module_init y module_exit, el primero llama al método de inicialización y el segundo al de restauración del sistema.  
![][31]  






### Referencias
* https://cmdchallenge.com  
* https://www.gutenberg.org  
* https://github.com/jvns/kernel-module-fun/blob/master/rickroll.c
* https://www.youtube.com/watch?v=efEZZZf_nTc
* https://oscarforner.com/2016/03/19/Linux_Kernel_Module_example__Rickroll_prank_  
* http://www.tldp.org/LDP/lkmpg/2.6/html/x279.html  
* http://man7.org/linux/man-pages/man2/syscalls.2.html   
* http://www.tldp.org/LDP/lkmpg/2.6/html/x323.html  
* http://www.theunixschool.com/2012/06/5-ways-to-reverse-order-of-file-content.html  
* https://stackoverflow.com/questions/742466/how-can-i-reverse-the-order-of-lines-in-a-file  
* https://www.cyberciti.biz/faq/unix-linux-shell-removing-duplicate-lines/  
* http://www.unix.com/shell-programming-and-scripting/166246-grep-awk-only-print-lines-two-columns-file.html  
* https://stackoverflow.com/questions/22190902/cut-or-awk-command-to-print-first-field-of-first-row  
* https://stedolan.github.io/jq/  


[1]: images/Desafio1.PNG
[2]: images/Desafio1C.PNG  
[3]: images/Desafio2.PNG
[4]: images/Desafio2C.PNG 
[5]: images/Desafio31.PNG
[6]: images/Desafio32.PNG 
[7]: images/Desafio33.PNG
[8]: images/Desafio3C.PNG 
[9]: images/Desafio41.PNG 
[10]: images/Desafio42.PNG
[11]: images/Desafio4C.PNG 
[12]: images/Desafio51.PNG 
[13]: images/Desafio52.PNG
[14]: images/Desafio5C.PNG 
[15]: images/Gutenberg_user.PNG 
[16]: images/Script_downloadbook.PNG 
[17]: images/directorio.PNG 
[18]: images/crontab_result.PNG 
[19]: images/NotificacionCorreo.PNG 
[20]: images/PrimerLibro.PNG 
[21]: images/SegundoLibro.PNG 
[22]: images/OnlyOne.PNG
[23]: images/Rickroll1.PNG
[24]: images/Rickroll2.PNG
[25]: images/Rickroll3.PNG
[26]: images/Rickroll4.PNG
[27]: images/Rickroll5.PNG
[28]: images/Rickroll8.PNG
[29]: images/Rickroll6.PNG
[30]: images/Rickroll7.PNG
[31]: images/Rickroll9.PNG



