# fake-ansvr-in-wsl2-for-nina
[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/luzbel/fake-ansvr-in-wsl2-for-nina/blob/master/README.en.md)

Scripts y procedimientos para poder usar desde N.I.N.A. una versión actualizada de astrometry.net instalada en WSL2 en vez de ansvr

Así que quieres usar una versión local de astrometry.net desde N.I.N.A. pero ...  
¿no quieres instalar Cygwin cuando WSL2 es una opción más moderna e integrada con Windows?  
¿no te fías del ejecutable de ansvr ya que no publica las fuentes?  
¿crees que la última versión de ansvr no está actualizada y no tiene las últimas versiones de astrometry.net?  
¿necesitas una versión personalizada de astrometry.net con algún cambio en las fuentes?  
¿usar astrotortilla tampoco parece conveniente por los mismos motivos?  
¿no te fías del ejecutable distribuido por https://www.hnsky.org/linux_subsyst y no te apetece compilar las fuentes?  

¡pues usemos la versión Linux de astrometry.net en WSL2 y engañemos a N.I.N.A. para que piense que está llamando a ansvr!

- Instala WSL2 en Windows
-  Asegurate de ejecutar los siguientes pasos en la distribución marcada por defecto en WSL2
	1. Instala astrometry.net con el sistema de paquetes de tu distribución preferida o compilando desde las fuentes
	2. Renombra /usr/bin/wcsinfo a /usr/bin/wcsinfo.elf
	3. Renombra /usr/bin/solve-field a /usr/bin/solve-field.elf
	4. Descarga los scripts solve-field y wcsinfo de este repositorio y copialos en /usr/bin
	5. Asegurate que los scripts tienen permisos 755 (rwxr-xr-x) para ser usados por cualquier usuario
- En Windows
	1. Crea un directorio para que N.I.N.A. piense que tienes un Cygwin instalado, por ejemplo en %USERPROFILE%\fakecygwin
	2. Crea un subdirectorio bin, por ejemplo en %USERPROFILE%\fakecygwin\bin
	3. Copia c:\Windows\System32\bash.exe al directorio bin creado en el paso anterior
- En N.I.N.A.
	1. En el apartado "Plate Solving" de Opciones->Plate Solving elige como Plate Solver "Local plate solver"
	2. En el apartado "Plate solver setting\Local plate solver" de Opciones->Plate Solving
		- En el apartado "Cygwin folder" selecciona el directorio falso de Cygwin creado (la base sin el /bin)
	3. Usa N.I.N.A. con normalidad

Puedes abrir un terminal de WSL2 y ver las trazas  en /tmp/solve.txt  o /tmp/wcs.txt  
Lo normal es que tu distribución Linux en WSL2 purgue este directorio en cada reinicio, así que no hay ningún mecanismo de rotado de los ficheros de trazas.  
No olvides copiar estos archivos si quieres guardar trazas de alguna sesión.  
Si en algún momento la resolución se eterniza porque has descargado muchos catálogos y estás seguro que no va a resolver (por ejemplo, si por error has realizado una toma sin quitar la tapa o te han salido las estrellas movidas) lo mejor es terminar el proceso desde una terminal WSL2 con "pkill solve-field" . Así evitas que el proceso de N.I.N.A. deje de responder. Recuerda que si has configurado "Local plate solver" tanto como "Plate solver" y como "Blind solver" tendrás que ejecutar un segundo pkill para terminar el segundo intento de resolución.

Basado en la solución propuesta para usar astrometry.net en WSL2 en https://www.hnsky.org/linux_subsyst
