# Laboratorio #1 - Robótica Industrial.

### Herramienta. 

Como primer objetivo de esta práctica de laboratorio, se tenía el diseñar y construir una herramienta que permitiera fijar un marcador borrable al flanche del robot.

Por lo tanto, para llevar a cabo la fabricación de la herramienta, fue necesario establecer un diseño que tuviera un acople adecuado y preciso a la articulación número 6 del robot ABB IRB140, es decir, se consultó el manual del operario del robot utilizado, y se extrajo el plano del plato correspondiente para poder diseñar la base en la cual se apoyaría la herramienta. 

![Plano](https://i.imgur.com/J3SebCN.png)

Se realizó el modelado con Autodesk Inventor por facilidades en la exportación a archivos .STL, y para poder obtener una estructura con escala real de la herramienta a fabricar. En la imagen a continuación se muestra el modelo obtenido.

![](https://i.imgur.com/9KUTvKP.png)

Como se puede observar en el modelo anterior, la base de la herramienta se ideó para tener un soporte cilíndrico con una inclinación de 10 grados respecto al plano basal de la pieza, lo cual le permitió estar desalineado del plano del plato como fue recomendado. La base de la herramienta fue entonces impresa y quedó como se muestra en la siguiente imagen.

![](https://i.imgur.com/HJcXccb.jpg)

Finalmente, la pieza logró ser acoplada a la articulación número seis del manipulador luego de algunos arreglos hechos posteriormente. Se tuvo algunas dificultades que se abordarán en los aspectos a mejorar.

Esta pieza fue ideada para completar la herramienta con un tubo en PVC junto con un tapón del mismo material usado para tuberías. estos fueron unidos a la base por medio de un acople y finalmente la pieza quedó de la siguiente manera:

![](https://i.imgur.com/A7oxIx0.jpg)

Se puede observar el marcador montado en la herramienta que sale por medio de un orificio taladrado en la tapa. Para la función de retractibilidad del marcador se usó espuma dentrro del tubo que permtía que el marcador entrase cuando fuera oprimido.

### RobotStudio

En primera instancia se realizó un modelado CAD, en el cual estuvieran las letras correspondientes para ser escritas por el ABB IRB140, esto con el objetivo de facilitar la selección e indicación del recorrido a realizar. 

![](https://i.imgur.com/o4uTZxs.png)



Cabe resaltar que el llevar a cabo la simulación del recorrido de algunas letras, es de gran ventaja, no solo por el poder generar el código RAPID, sino también por poder solventar errores de singularidad, alcance del robot, alcance de máxima rotación por articulación, entre otros errores que deben ser tenidos en cuenta para la obtención de un resultado positivo.

Posteriormente, se modeló la herramienta teniendo en cuenta su altura final adquirida incluyendo la punta del marcador. Esta se importó al RobotStudio, se creó como new tool y se le creó un Frame correspondiente para crear su propio UTP. 

![](https://i.imgur.com/A9gHy87.png)
![](https://i.imgur.com/DKDkfnV.png)

Una vez realizado lo mencionado, se estableció un nuevo WorkObject en donde se situarían los targets y los paths creados para desarrollar la rutina de la escritura de las letras. 

![](https://i.imgur.com/jvWzuNr.png)


#### Rutinas realizadas: 

* Se realizaron dos rutinas sobre el tablero plano (piso del robot). Una de ellas frente a la posición de home del robot, y otra con un ángulo de 30° respecto a z.

![](https://i.imgur.com/eVVsrKM.png)

* Se realizó una rutina con una inclinación de 30°.
![](https://i.imgur.com/vrJP4lm.png)

Los códigos RAPID y videos de su producción, se encuentran dentro del mismo repositorio. 

#### Factores considerados al momento de realizar la programación de los target y paths.

* El situar en un lugar adecuado el WorkObject es de suma importancia, debido a que para escribir en lugares diferentes o como fue el caso, con inclinaciones diferentes, únicamente fue necesario cambiar el lugar del WorkObject para que todos los puntos que se encontraban dentro de él también fueran desplazados y con ellos lograr ubicar la escritura en un lugar distinto. 
* La creación de un punto Home que estuviera fuera de cualquier WorkObject, para evitar que este también se desplace en caso de mover el primero.
* Situar el modelado en donde se ubicarán los targets de un path, dentro de la cobertura o alcance del robot.
* Utilizar movimientos Joint para acercar el robor a algún punto cercano de la rutina y para llevarlo a Home. Esto debido a que le da más libertad al robot (movimiento de las articulaciones) de llegar a algún punto cuando se conoce que puede ir sin una precisión alta durante ese recorrido.


#### Aspectos a mejorar


* Se podría mejorar las curvaturas de las letras utilizando una mejor interpolación de los puntos de las trayectorias, es decir, establecer más cantidad de targets dentro del path y colocarles movimientos circulares para evitar los trazos rectos en estas curvas.
* Se podría reducir la distancia entre letras, debido a que varios de los errores arrojados por RobotStudio se basaban en que el manipulador no podía llegar tan fácil de un punto a otro que fuera relativamente lejano, y también para evitar posibles singularidades, entre más distancia, más probable a que deba existir una rotación o movimiento indeseado en el robot, lo que causaría su bloqueo o singularidad.
* La pieza impresa tuvo problemas al ser implementada pues no se siguieron las indicaciones dadas por el plano del manipulador, se podría tener en cuenta las dimensiones correctas para no evitar problemas de ensamblare de la herramienta.
