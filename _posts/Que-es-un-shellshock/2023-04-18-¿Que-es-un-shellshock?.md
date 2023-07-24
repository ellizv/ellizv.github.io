---
title: ¿Que es un shellshock?
published: true
---

<br>
# Introducción

<br>

Shellshock es una vulnerabilidad que afecta al sistema de variables de los sistemas operativos UNIX, esto quiere decir que normalmente si tú quieres guardar una variable con nombre “i” y con el contenido ‘Esto es una variable’ ejecutarías. 

<br>

Esto sucede porque bash antiguamente, al asignar un valor a una variable de entorno no se paraba a leer la definición como tal sino que lo que hacía era ejecutar los comandos que hubieran después de la función.

```perl
env i='Esto es una variable'
```
<br>

Esto sirve para hacer guardar una cadena de texto, pero ¿Y si consigues ejecutar un comando? No se puede conseguir ejecutar un comando, ya que simplemente te lo almacena como texto y lo trata como tal, así que en ningún momento se está dando opción a la ejecución de comandos, o al menos esto es lo que se pensaba antes de descubrir esta vulnerabilidad.

<br>
# Historia
<br>
Se pensaba que no había ninguna falla de seguridad con el guardado y la interpretación de las variables en bash, hasta que el 12 de septiembre de 2014 Stéphane Chazelas contactó al encargado del mantenimiento de Bash, Chet Ramey, mencionándole acerca de la falla de seguridad que había encontrado. La vulnerabilidad se dio a conocer después de ser parcheada, lo que quiere decir que en principio no tendría que surgir más este problema, pero sí que surge, ya que la gente no actualiza su software a la última versión, y por eso hoy en día todavía se ven casos de shellshock.
<br>
<br>
La manera en la que se ejecuta esta vulnerabilidad es declarando la misma variable que antes, pero poniendo “() { :; }; ” antes del contenido de la variable con esto consigues que lo que escribas después se ejecute como un comando. A continuación mostraré un ejemplo de un shellshock en un sistema vulnerable, posteriormente, en la parte inferior al ejemplo mostraré como se vería en un sistema actualizado y que por ende no es vulnerable.
<br>
<br>
<br>
![hola](https://gcdnb.pbrd.co/images/Joq8nHsDyszT.png?o=1)
<br>
<br>
<br>
Como se puede ver en este ejemplo se está ejecutando el comando que le indiques al definir la función. Ahora vamos con el no vulnerable
<br>
<br>
<br>
![hola](https://gcdnb.pbrd.co/images/yHmUVvqhprzE.png?o=1)
<br>
# Conclusión
<br>
Concluyo esta breve explicación sobre esta vulnerabilidad con un repaso aun más breve para poder recordarlo y entenderlo más fácilmente. Shellshock es una vulnerabilidad que antiguamente había en bash con la que podías ejecutar comandos, esto sucedía y sucede gracias a que al establecer una variable de entorno no se detenía en la definición en sí, sino que ejecutaba los comandos que hubiera despues.
