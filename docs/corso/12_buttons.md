# Buttons


In questo capitolo andremo a provare alcuni esperimenti in cui costruiremo progetti hardware basati
sui pulsanti e i led, governati da un ESP32 e controllati tramite codice MicroPython.



<!-- ################################################################################# -->
## Buttons

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

