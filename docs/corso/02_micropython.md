# MicroPython 

Come abbiamo già detto, MicroPython è un interprete progettato appositamente per i microcontrollori e che cerca di emulare le funzionalità
base di Python. Sostanzialmente sono implementati due gruppi di funzionalità:

- alcune delle librerie della **Python Standard Library**
- alcune funzionalità specifiche per i microcontrollori.


!!! note "Documentazione Ufficiale"
    
    Il progetto MicroPython espone nel suo sito web la 
    <a href="https://docs.micropython.org/en/latest/index.html" target="_blank">documentazione ufficiale</a> di riferimento per il progetto MicroPython.
    
    Se volete curiosare... fate pure. Lo spirito con cui ho messo i link mirati qui sotto è invece quello di consultare una documentazione specifica secondo necessità.



## Funzionalità *micro-ified* della Python Standard Library


Le funzionalità che sono state reimplementate per MicroPython della Python Standard Library sono elencate al [seguente link](https://docs.micropython.org/en/latest/library/index.html#micropython-lib-python):

In particolare, a noi potrebbero tornare utili:

- `math`, per operazioni matematiche 
- `random`, per generare numeri pseudo-casuali
- `socket`, per funzionalità di rete basate sul livello di trasporto
- `time`, per funzioni relative a data e ora (e la utilissima funzione `sleep()`)




## Funzionalità specifiche MicroPython


L'universo MicroPython implementa alcune funzionalità non disponibili nel Python originale, ma specifiche delle piattaforme per MicroControllori.
Tutte le funzionalità implementate sono documentate al [seguente link](https://docs.micropython.org/en/latest/library/index.html#micropython-specific-libraries).

In particolare, mi piace mettere in eveidenza i seguenti moduli, che sicuramente prima o poi ci ritorneranno utili:

--------

modulo **`machine`** - (<a href="https://docs.micropython.org/en/latest/library/machine.html" target="_blank">documentazione</a>) <br>
Funzioni collegate all'hardware della MCU. Permette di gestire ogni componente hardware del microcontrollore.

modulo **`esp32`** (<a href="https://docs.micropython.org/en/latest/library/esp32.html" target="_blank">documentazione</a>) <br>
contiene funzionalità specifiche per il microcontrollore esp32

modulo **`micropython`** - (<a href="https://docs.micropython.org/en/latest/library/micropython.html" target="_blank">documentazione</a>) <br>
Accesso e controllo delle librerie interne di MicroPython. Può essere utilizzato per implementare funzionalità aggiuntive.

--------

modulo **`network`** - (<a href="https://docs.micropython.org/en/latest/library/network.html" target="_blank">documentazione</a>) <br>
Modulo per la configurazione della rete. Collegamento del dispositivo alla rete Wifi, del suo indirizzamento e routing.

modulo **`bluetooth`** - (<a href="https://docs.micropython.org/en/latest/library/bluetooth.html" target="_blank">documentazione</a>) <br>
Libreria Bluetooth di basso livello. Serve (ovviamente) per connettere la MCU tramite bluetooth

--------

I moduli `network` e `bluetooth` saranno trattati nel capitolo relativo al networking. Qui sotto proveremo a parlare dei moduli di base.


## modulo `machine`

blah blah...



<br>
<br>
<br>

