# MicroPython Firmware

La prima cosa da fare quando si programma un ESP32 con MicroPython è caricare su di esso il firmware MicroPython, che conterrà l'interprete e le librerie 
di base per l'esecuzione del codice che andremo a scrivere.

Questa operazione va fatta per prima e solo un'unica volta!!!

Il sito ufficiale di MicroPython è (incredibilmente): <a href="https://micropython.org" target="_blank">https://micropython.org</a>

Scaricate fra le releases il seguente file binario:

--- immagine ---

Blah blah

## "Hello, World!"

Connetti il tuo ESP32 al computer e cambia l'interprete Python a `MicroPython (ESP32)`.

Scrivi il tuo difficilissimo codice:

``` py
print("Hello, World!")
```

e salva il file come `HelloWorld.py` dentro la memoria dell'ESP32. Per farlo:

Clicca sul pulsante APRI:

--- immagine ---

Seleziona `MicroPython device`

--- immagine ---

Esegui il codice, premendo `F5` oppure selezionando l'azione `Run current script`

Se vuoi fare in modo che il tuo dispositivo esegua il tuo codice continuamente non appena viene acceso (così come fanno tutti i dispositivi: televisori, forni, macchine del caffè, etc...) apri il file `boot.py` e modificalo come segue:

``` py
# codice per eseguire il file HelloWord.py
```


<br>
<br>
<br>

