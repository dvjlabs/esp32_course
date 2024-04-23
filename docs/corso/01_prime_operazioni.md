# Prime Operazioni


In questo capitolo installeremo il firmware MicroPython su ESP32 e faremo un primo test di funzionamento. 
L'obiettivo di questo capitolo è essere operativi... le spiegazioni sul codice (Micro)Python e il dispositivo ESP32... arrivano dopo!


## Installazione Firmware

Per caricare il firmware MicroPython Thonny offre una comodissima interfaccia, che ci permette di scaricarlo e installarlo automaticamente!!!

Se invece volete curiosare sul sito ufficiale MicroPython:

- Aprite il link <a href="https://micropython.org" target="_blank">MicroPython</a>;
- Cliccate sulla voce `Download`;
- Scendete sull'elenco dei microcontrollori fino a trovare `ESP32 / WROOM - EspressIf`
- Verificate l'ultima ***Firmware release*** disponibile  (l'ultima volta che ho guardato, la versione `v1.22.2`)

Adesso un attimo di riposo... siete praticamente già ad un terzo del lavoro!!!

La seconda fase consiste semplicemente nel collegare il microcontrollore ESP32 al nostro computer tramite un cavo USB.<br>
Mi immagino che siate già riusciti nell'impresa... pronti per l'ultima fase:

- Aprite `Thonny`
- Dal menù `ESEGUI`, seleziona `CONFIGURA L'INTERPRETE`
- Seleziona `MicroPython (ESP32)` (vedi figura sotto)

<br>

![Opzioni Thonny](images/opzioni_thonny.png)

<br>

!!! note "La giusta porta COM"

    Come vedete in figura, la MCU utilizza una porta COM supportata dal driver **Silicon Labs CP210x USB to UART Bridge**.
    
    Se nel tuo computer manca... chiedi al prof!!!

<br>

- Adesso selezionate `Installa o Aggiorna MicroPython`
- Si aprirà la finestra qui sotto. Vanno selezionate:
    
    - la porta su cui è collegata il microcontrollore ESP32
    - La famiglia della MCU (ESP32)
    - La variante (EspressIf - ESP32 / WROOM)
    - la versione (dovrebbe apparire automaticamente l'ultima installabile)

- Poi clicca `installa`

<br>

![Installazione Firmware](images/install_firmware.png)

<br>

!!! tip "... attendi fiducioso un minutino buono..."
    
    Al termine della procedura dovrebbe apparire l'interprete MicroPython nella shell di Thonny

<br>

![Shell Thonny](images/shell_thonny_micropython.png)

<br>

Ecco fatto!

Siamo pronti per il primo esempio!


## "Hello, World!" con ESP32 e MicroPython

Tecnicamente questo... non è un HelloWorld program... nel senso che non scriveremo "Hello, World!", ma faremo accendere e spegnere un led.
Ok... capisco la delusione: aggiungerò in cima la scritta "Hello, World!" e, ad ogni accensione o spegnimento scriverò una notifica del tipo
"LED Acceso" o "LED Spento".

Il programma ci serve come esempio per prendere confidenza con i mondi MicroPython ed ESP32: non è importante adesso quello che fa il programma, 
ma riuscire a capire tutte le operazioni da svolgere. Per questo ho deciso di dividere le operazioni in step successivi. Andiamo!!

**Step 0**

Se non lo hai già fatto, connetti il tuo ESP32 al computer, apri Thonny e cambia l'interprete Python a `MicroPython (ESP32)`.

**Step 1**

Copia su Thonny il seguente codice:

``` py
from machine import Pin
from time import sleep

# Il pin 5 è quello del LED programmabile
# Ricordate?
led = Pin(5, Pin.OUT)

while True:
    if led.value():
        led.off()
        print("LED Spento")
    else:
        led.on()
        print("LED Acceso")
    
    # Aspetta 1 secondo...
    sleep(1)
```

**Step 2**

Adesso salva il file come `led_test.py` dentro la memoria dell'ESP32. Per farlo:

- clicca SALVA
- Dall'interfaccia seleziona *Dispositivo MicroPython*

<br>

![Salva su MCU](images/save_selection.png)

<br>

- Salva il file nella MCU con nome `led_test.py` o come preferisci.

**Step 3**

Esegui il codice, premendo `F5` oppure selezionando l'azione `Run current script`: dovresti vedere PRIMA la scritta `Hello, World!` e poi alternate
di un secondo le scritte `LED Spento` e `LED Acceso` mentre il LED si accende e si spegne.

Ecco fatto!





## "boot.py" e "main.py"


Sicuramente avrai notato che nel filesystem dell'ESP32 è presente un file chiamato "boot.py". Questo file viene eseguito automaticamente... al boot del dispositivo.
Quindi il poco codice che va lì dentro può servire per le prime indispensabili operazioni irrinunciabili: collegarsi ad una rete wifi, attivare il bluetooth, far partire webrepl (qualunque cosa esso sia)...

Se invece dovete eseguire un codice, salvate il vostro file con il nome "main.py". Questo, rispetto a copiare il codice nel file "boot.py" presenterà diversi vantaggi:

- sarà eseguito subito dopo il boot, ovvero quando il dispositivo è già pienamente funzionante.
- sarà possibile collegarsi al dispositivo tramite (web)repl e stoppare/far ripartire il main senza dover riavvare tutto il dispositivo.
- blah blah (finiscimi!!!)


<br>
<br>
<br>

