# Esp32 Simulator

Per poter lavorare con i dispositivi ESP32 e tutti i sensori anche da casa o in generale, senza
*apparecchiare* tutto il laboratorio di materiale, è possibile ricorrere ad uno dei tanti progetti di simulazione
dell'hardware. 

Quello che ha più colpito la nostra attenzione si chiama [https://wokwi.com/](https://wokwi.com/) ed 
è una applicazione web per la simulazione di progetti IoT direttamente nel browser.



## Istruzioni Operative


!!! tip "Suggerimento"

    Le seguenti istruzioni valgono per lavorare su un dispositivo virtuale il più possibile identico all'esp32 che
    abbiamo a scuola.
    
    I prof stanno lavorando per renderlo disponibile di default su **wokwi**!!!


1. Scarica il seguente [file zip](data/esp32-wroom-32.zip) ed estrai la cartella `esp32-wroom-32` sul tuo computer

2. Clicca qui per <a href="https://wokwi.com/projects/new/micropython-esp32" target="_blank">creare un nuovo progetto</a>

3. Premi `F1` sull'editor e nella tendina di selezione cerca "Load custom board file..."

4. Carica la cartella `esp32-wroom-32` scaricata precedentemente.

5. Modifica il file `diagram.json` in questo modo:

    ``` json title="file diagram.json modificato" hl_lines="7"
    {
      "version": 1,
      "author": "il tuo nome e cognome",
      "editor": "wokwi",
      "parts": [
        {
          "type": "wokwi-custom-board",
          "id": "board",
          "attrs": { "env": "micropython-20231227-v1.22.0" }
        }
      ],
       "connections": [
         [ "esp:TX", "$serialMonitor:RX", "", [] ],
         [ "esp:RX", "$serialMonitor:TX", "", [] ]
       ],
      "dependencies": {}
    }
    ```

6. **Salva** e sei pronto all'azione!! (indica il nome del tuo progetto! Ad esempio, ProvaLED)

7. **Modifica il tuo progetto hardware** aggiungendo led, resistenze, collegamenti e tutto quanto necessario

8. **Scrivi il codice** nell'editor online (file `main.py`) **e testalo** avviando l'esp32 virtuale.

9. Quando hai finito, **scarica il progetto** (file `main.py` e `diagram.json`) dal menù in alto, facendo `Download project.zip` (e rinomina il file zip a piacimento)

10. Consegna i compiti inviando il file `zip` al docente!


Adesso non hai più alcuna scusa per non fare i compiti a casa!!!

<br>
<br>
<br>

