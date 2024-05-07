# Led(s)


Introduciamo i componenti fondamentali con cui andremo a lavorare:

## LED

Un LED è un componente elettronico che funziona solo quando la corrente scorre nel verso giusto. Tipicamente ha due poli: il polo positivo (catodo)
nel pin più lungo e il polo negativo (anodo) nel pin più corto. 

![LED](images/LED.png)

I led lavorano ad una corrente di attraversamento compresa fra 1.9V e 3.3V. Se la corrente supera questo voltaggio, il LED si danneggerà e magari...
prenderà fuoco. ::blink::


Questo progetto è identico a quello del LED integrato nella MCU che lampeggia. La differenza (sostanziale)
sta nel fatto che in questo progetto il LED è esterno e collegato ad un PIN a piacere (fra quelli... ammissibili).

Vediamo la lista dei componenti necessari (oltre ovviamente all'ESP32 e alla breadboard su cui è alloggiato):


![Lista dei componenti](projects/LED_material.png)


Vediamo adesso come costruire il circuito del LED:


![LED Schema](projects/LED_schema.png)


A seconda del PIN scelto per il collegamento fisico del LED, dobbiamo indicare il numero nel codice (io ci ho lasciato il 5 del led integrato):

``` python
from machine import Pin
from time import sleep

# xx è il numero del GPIO a cui hai collegato il led
led = Pin(xx, Pin.OUT)
led.off()

while True:
    led.on()
    print("LED Acceso")
    sleep(1)
    
    led.off()
    print("LED Spento")
    sleep(1)

```



<!-- ################################################################################# -->
## LED Bar


La barra dei LED è un semplice componente in cui sono integrati ben 8 LED! Per il nostro progetto avremo bisogno di:


![Lista dei componenti](projects/LEDBar_material.png)


Fatto questo, andate a collegare i componenti come in figura:


![LEDBAR Schema](projects/LEDBar_schema.png)


Adesso tramite codice andiamo a fornire un comportamento al nostro progetto: Facciamo in modo che ogni secondo la barra si riempa
sempre più e poi inizi a svuotarsi. Ecco il codice:

``` python
import time
from machine import Pin

# Gli 8 pin, in ordine come connessi alla ledbar
pins=[a,b,c,d,e,f,g,h,i]

acceso = True
while True:
    for p in pins:
        led = Pin( p, Pin.OUT)
        led.value( acceso )
        time.sleep_ms(500)
    
    # rovescia l'ordine dei pin
    pins.reverse()
    
    # inverti vero/falso
    acceso = not acceso
```



<!-- ################################################################################# -->
## Esercizi

<br>

**Luci della Polizia!**

Implementare un circuito con due luci, una rossa e una blu, che si accendono alternativamente.

<br>

**Semaforo**

Implementare un circuito con tre luci: verde, giallo, rossa a rappresentare un semaforo. Tramite codice, con un opportuno timer,
programmare la giusta alternanza di luci tipica di un semaforo.

<br>

**LED...Bar**


Parte il caricamento della barra, una luce ogni secondo. Quando è piena, inizia lo spegnimento, nello stesso ordine, un led al secondo.




<br>
<br>
<br>

