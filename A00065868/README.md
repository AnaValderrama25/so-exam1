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
3. La página https://cmdchallenge.com propone unos retos en la consola virtual, pero no sólo fueron resueltos ahí sino que también se llevaron a cabo con ejemplos prácticos en CentOS7.
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


### Referencias
* https://cmdchallenge.com  
* https://www.gutenberg.org  
* https://github.com/jvns/kernel-module-fun/blob/master/rickroll.c
* https://www.youtube.com/watch?v=efEZZZf_nTc

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
