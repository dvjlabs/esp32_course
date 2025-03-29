# Buttons


In questo capitolo andremo a provare alcuni esperimenti in cui costruiremo
progetti hardware basati sui pulsanti e i led, governati da un ESP32 e
controllati tramite codice MicroPython.

I pulsanti hardware hanno due caratteristiche fisiche che vanno sempre considerate quando se ne inserisce uno in un circuito:

- **floating inputs**: all'inizio l'ESP32 è confuso perché non sa se lo stato iniziale del pulsante è cliccato oppure no. Questo problema si può risolvere con una resistenza di `pull-up` o di `pull-down`.

- **chattering**: se si clicca il pulsante molto rapidamente (ad esempio *sparando* in un gioco), l'ESP32 potrebbe pensare ad un'unica pressione prolungata. Questo problema si può risolvere con tecniche di `debouncing`.

Vediamo come è fatto internamente un pulsante:

![Buttons Internals](images/button_internals.png)

E vediamo in quali modi è possibile collegarlo al nostro ESP32:

![Buttons Connections](images/button_connections.webp)

In qualunque dei 4 modi indicati sopra, tutto il circuito passerà sempre per il pulsante, che avrà la possibilità di *aprirlo* o *chiuderlo*.

Capito che servono due collegamenti, ci sono due modi il cui il pulsante può essere collegato al circuito:

1. in modalità `pull-down`, con una estremità connessa al `GPIO`, l'altra alla tensione di `3.3V`: in questo caso, quando il pulsante è premuto il valore è `HIGH`, altrimenti è `LOW`.
2. in modalità `pull-up`, con una estremità connessa al `GPIO`, l'altra al `GND`: in questo caso, quando il pulsante è premuto il valore è `LOW`, altrimenti è `HIGH`.


<!-- ##################################################################### -->
## Esempi con i pulsanti

(da sistemare)

Nel secondo progetto abbiamo un pulsante collegato ad un LED nel nostro circuito. Incredibilmente...
quando si clicca il pulsante dovrebbe accendersi la luce!!!

Vediamo lo schema elettrico del progetto:


![Schema LED Button](https://esp32io.com/images/tutorial/esp32-button-led-wiring-diagram.jpg)


Quello che manca è il codice di funzionamento. Eccolo:

``` python
from machine import Pin

# xx è il numero del GPIO a cui hai collegato il led
# yy è il numero del GPIO a cui hai collegato il pulsante
led = Pin(xx, Pin.OUT)
button = Pin(yy, Pin.IN,Pin.PULL_UP)

while True:
    if not button.value():
        led.off()
    else:
        led.on()
```



<!-- ################################################################################# -->
## Esercizi


**Button LED...Bar**

Pulsante e barra dei led.

Quando si clicca il pulsante, parte il caricamento della barra, che poi si scaricherà quando è tutta piena.

Difficoltà ulteriore: quando si clicca di nuovo il pulsante il caricamento si interrompe.


<br>


<br>
<br>
<br>
