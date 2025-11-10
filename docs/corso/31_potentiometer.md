# Potenziometri

Un potenziometro è una manopola che traduce il grado di posizionamento della stessa in una tensione percentuale
rilasciata come valore di output.

Si presenta come un dispositivo con 3 connettori, tali che:

- uno va collegato al GND
- uno va collegato ad un pin
- uno va collegato alla tensione (3.3v oppure 5v)

Ovviamente il valore rilasciato dal sensore è un valore analogico e quindi, a livello elettronico, il potenziometro
ha bisogno di un ADC per restituire valori digitali.

![Potenziometro](images/potentiometer.png)


Il codice indicato visualizza una serie di valori (uno ogni decimo di secondo) che rappresentano la posizione
percentuale (in scala 0-4095) della manopola del potenziometro.

<br>

``` py title="Potenziometro"
# In questo esempio i valori restituiti dovrebbero andare da 0 a 4095
from machine import Pin,ADC
import time

adc=ADC(Pin(33))
adc.atten(ADC.ATTN_11DB)
adc.width(ADC.WIDTH_12BIT)

while True:
    adcValue = adc.read()
    print("Value:", adcValue)
    time.sleep_ms(100)
```

Tutto qua! Adesso, sotto con i progetti!!!


<!-- ################################################################################# -->
## Esercizi

Qualche 
<br>
<br>
<br>

