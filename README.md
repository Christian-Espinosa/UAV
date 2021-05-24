
# Índice de contenidos
* [UAV](#UAV)
* [Descripción del proyecto](#descripción-del-proyecto)
* [Componentes Electrónicos](#componentes-electrónicos)
* [Esquema Hardware](#esquema-hardware)
* [Arquitectura del Software](#arquitectura-del-software)
* [Estrategia de Simulación](#estrategia-de-simulación)
  * [Simulaciones Prácticas](#simulaciones-prácticas)
        * [Algoritmo de Movimiento Autónomo por Sensores de Ultrasonidos](#algoritmo-de-movimiento-autónomo-por-sensores-de-ultrasonidos)
        * [PATH PLANNING](#path-planning)
* [Autores](#autores)  

# UAV
Este proyecto consiste en desarrollar las funcionalidades de un dron al cual definamos un trayecto, escoja el camino más apropiado, realice el recorrido y una vez hecho el recorrido aterrice de manera precisa donde se le especifique. Además en situaciones concretas el dron será capaz de esquivar obstáculos a partir de la información de sus sensores.

## Descripción del proyecto:
La idea de nuestro proyecto es montar un dron de 4 brushless motors, con tres sensores ultrasonido para evitar que se choque con elementos próximos a las hélices. Además el dron llevará equipado un acelerómetro y un GPS para poder ubicar y controlar apropiadamente el dron. Para poder aterrizar con precisión se le va a implementar visión por computador que va a reconocer el terreno y distancias del dron.

En este github encontraremos una simulación de como nuestro dron debería comportarse en la realidad. Hemos desarrollado básicamente dos algoritmos, el primero permite al
dron moverse de forma autònoma de un punto origen a un punto destino usando los 3 sensores de ultrasonidos para evitar colisionar con objetos en el camino. Por otra parte también hemos desarollado un algoritmo de path planning al que se le da información sobre el area donde el dron deberá volar y, teniendo en cuenta los obstáculos que hay en esta
establece un camino entre el punto inicial y el punto final mediante el algoritmo A*.

El objetivo principal del dron es que vuele, se pueda ubicar y mover según se le haya programado. La idea es dejarlo volando y según algoritmos de reconocimiento de patrones sepa donde y como tiene que aterrizar. El patrón estará en el suelo, bien visible para que el dron pueda reconocerlo a unos 10 a 20 metros de altura. El dron se pondrá en vuelo programado y aterrizará automáticamente una vez llegue a cierta altitud o a las coordenadas cercanas a la marca (patrón) del destino.

## Componentes Electrónicos
This is the list of the used components:
- Motores y ESCs RS2205 2205 2300KV
- Hélices
- Arduino nano
- Batería
- MPU6050
- RaspberriPi
- RP Cam
- GPS
- Sensores Ultrasonido
- Impresiones 3d

## Esquema Hardware
<img src="/images/hw_scheme.png" width="500" height="300" >

## Arquitectura del Software

<img src="/images/ARQUITECTURA_SW_def.png" width="500" height="300" >

## Contribuciones

El dron puede actuar por sí mismo. Se le puede aplicar una ruta y a partir de entonces, ser totalmente autónomo con los objetivos que se le marquen hasta que aterrice.
Tendrá un sistema aterrizaje inteligente y sensores para poderse mover con seguridad y libertad en cualquier eje.

## Piezas 3D

Utilizaremos la impresora 3D para poder hacer aquellas piezas de la estructura del dron.
En este caso vamos a crear una caja donde guardaremos algunos componentes del dron, como las distintas placas base etc...
Por otra parte, hemos creamos los distintos brazos del dron, donde colocaremos tanto las hélices como los distintos motores.

Finalmente, un conjunto de acoples para cada servomotor.

<img src="/images/3D_model.png" width="500" height="300">

## Estrategia de Simulación

En nuestro caso vamos a utilizar un simulador llamado coppelia, que es con el que estamos trabajando en clase. Una de las primeras pruebas que queremos realizar en el simulador es conseguir que el dron se levante del suelo en una altura concreta y que sea capaz de desplazarse hasta un lugar indicado, de este aspecto se habla más adelante en el documento.
Para poder realizar las simulaciones ya tenemos implementado en el propio coppelia el objeto dron que lo vamos a modificar según las especificaciones de piezas hardware, especificadas anteriormente. De entrada hemos añadido 3 sensores para medir las distancias del dron a objetos/obstáculos cercanos.

### Simulaciones Prácticas
Simulación simple:
El dorn es capaz de seguir un path creado por nosotros con el coppelia
<img src="/images/coppelia_based_path.png" width="500" height="500" >

El drone es capaz de esquivar 1 obejto pro la derecha o por la izquierda. NO PARA ya que es una de las primeras simulaciones

<img src="/images/simple.png" width="500" height="300">

**Algoritmo de Movimiento Autónomo por Sensores Ultrasonido:**

Agoritmo echo desde cero por el grupo para dotar al dron de movimiento mediante la sensórica de este, que consta de 3 sensores de ultrasonidos: uno frontal y dos a los laterales.
El módulo tiene como entradas 2 puntos: origen = [xo,yo,zo] y destino =[xd,yd,zd], el lugar de donde va empezar el dron el desplazamiento y la posición exacta donde va a aterrizar.



<img src="/images/trees.PNG" width="500" height="300" >

**PATH PLANNING:**

Finalmente decidimos aplicar A* al ser una estrategia rápida computacionalmente y eficiente para encontrar una posible solución. En el código se le definen los obstáculos, que va a tener que evitar y el algoritmo busca una posible ruta óptima para poder ir al destino.

Primeramente obtenemos el área de trabajo:

<img src="/images/area.png" width="500" height="300" >

A partir de esta obtenemos una serie de puntos por donde el dron va a pasar mediante el algoritmo A*:

<img src="/images/path.png" width="500" height="300" >

Y con esto finalmente el dron se va a mover del punto inicial al punto final:

<img src="/images/path_sim.png" width="500" height="300" >

## Autores:

- <a href="https://github.com/arnaubalaguer">Arnau Balaguer Albareda</a>
- <a href="https://github.com/Christian-Espinosa">Christian Espinosa Reboredo</a>
- <a href="https://github.com/Pau-Riba-Escobar">Pau Riba Escobar</a>
- <a href="">Alberto Vallespín Herranz</a>
