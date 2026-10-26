# ESP32 <---> Flask 

Comincio subito con le scuse... nella lezione della volta scorsa **tutto quello che poteva andare storto è andato storto**. 
Per la legge dei grandi numeri la lezione di oggi sarà mondiale... nel dubbio, mi sono preparato al meglio!!!

Vogliamo imparare a mettere in comunicazione un server web, basato su Flask, con un ESP32. Elenco gli argomenti da affrontare,
cercando di andare più possibile in ordine:

- Dal PC, realizzare un semplice sito in Flask.
- Farlo funzionare e testarlo adeguatamente
- Da ESP32: connettersi alla rete Wifi
- Da ESP32, realizzare un semplice circuito con un sensore di input
- Da ESP32, inviare tramite la libreria *requests* il dato al server Flask
- Da ovunque, con un browser... visualizzare il dato ricevuto

Fatto questo... lavoriamo su ESP32:

- Da ESP32, realizzare un semplice sito con microdot
- Farlo funzionare e testarlo adeguatamente
- Connettersi al sito per modificare lo stato di un sensore di output

Mettendo insieme questo e quello:

- Da ESP32, realizzare un semplice sito con microdot
- Dal PC, realizzare un semplice sito in Flask per inviare richieste a ESP32
- Dal sito sul PC clicco... su ESP32 si accende un led.

Poi sparecchio e vado a casa soddisfatto. Iniziamo!!!


## Flask (su PC)


Flask è una libreria Python che fornisce uno Web Framework utile per realizzare applicazioni web.

Da Thonny, menù opzioni e blah blah e scrivi:

``` bash
pip install flask
```

Pronti, via!

```python title="Primo esempio con Flask"
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello, World!"

if __name__ == "__main__":
    # la mancanza di use_reloader = False è stato uno dei problemi della volta scorsa...
    # è un problema che si verifica solo su Windows...
    # se mi chiedete qualcosa potrebbe uscirmi una parolaccia :)
    app.run(host = "0.0.0.0", port = 5000, debug = True, use_reloader = False)
```

Secondo esempio con Flask: struttura di una pagina con template!

```bash title="Struttura files della cartella"
provaFlask
├── static
    └── image.jpg
├── templates
    └── pagina.html
└── code.py
```

E nei file di codice:

```html title="file pagina.html"
<h1>Ciaone!</h1>

Sono la pagina web nella cartella templates!! <br>
<img src="static/image.jpg">
```


```python title="file code.py"
from flask import Flask,render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("pagina.html")


if __name__ == "__main__":
    app.run(host = "0.0.0.0", port = 5000, debug = True, use_reloader = False)
```

## Invio dati (solo GET)

Facciamo un paio di prove, entrambi con GET: uno per inviare dati all'esterno, uno per inviare e ricevere dati sullo stesso
server.


```html title="prova"
<form action="https://www.google.it/search" method="GET">

<input name="q">
<input type="submit" value="Cerca con Google">
</form>
```

Il codice Flask per far funzionare la richiesta GET neanche lo scrivo... 

Il secondo esempio lo scrivo a metà... ovvero il codice per inviare dati dovreste averlo ormai capito... proviamo
come riceverli

```python title="riceve dati GET"
from flask import Flask,render_template

app = Flask(__name__)

@app.route("/ascolta/<dati>")
def eccomi(dati):
    return render_template("pagina.html", valore = dati)

if __name__ == "__main__":
    app.run(host = "0.0.0.0", port = 5000, debug = True, use_reloader = False)
```

```html title="pagina.html"
Valore inviato: {{ valore }}
```

## ESP32: connessione al wifi

Fai così... immagina di volerti connettere alla rete wifi chiamata "PIPPO" (quello in informatica sarebbe l'*ESSID* della rete wifi)
che ha password "PAPERINO" (in realtà si chiama *key* oppure *passphrase*). Allora tu fai così:

``` python
import network
import time

# l'opzione network.STA_IF crea una interfaccia in grado di connettersi ad una rete Wifi
wlan = network.WLAN(network.STA_IF)

# attiva l'interfaccia
wlan.active(True)

# connette l'interfaccia WLAN alla rete Wifi PIPPO con chiave PAPERINO
wlan.connect('PIPPO', 'PAPERINO')

while not wlan.isconnected():
    print("waiting for connection...")
    time.sleep(1)

print("Connected!")
print(wlan.ifconfig())
```

Tutto qui! Ricorda al prof che deve attivare un'altra rete, perché con la rete *WifiDaVinci* l'ESP32 non funziona!!! Quello sarebbe un altro
dei problemi capitati la scorsa volta...


## ESP32 urequests

Quello che vogliamo fare adesso è inviare richieste GET e non tramite una pagina web, ma tramite una piccola applicazione (Micro)Python
in esecuzione sull'ESP32.

La libreria `urequests` è la libreria MicroPython standard per l'invio dati tramite HTTP. Vediamo un esempio banale di richiesta GET.
Tutto il contorno dovrete inserirlo voi...

``` python title="richiesta GET"
import requests

# immagina di voler inviare la temperatura di 27.5°C
temperatura = 27.5

IP_DEL_PC = "192.168.110.102" # Ad esempio...

URL_di_INVIO = f"http://{IP_DEL_PC}:5000/ascolta/" + str(temperatura)

# visualizza l'URL di invio per capire cosa stai facendo...
print("URL:", URL_di_INVIO)

# poi invia tutto!
resp = requests.get(URL_di_INVIO)
print('Response content:', resp.text)
# Al server in ascolto (si spera) su IP_DEL_PC arriverà il dato 27.5
```


## ESP32 con microdot

*microdot* sarebbe flask in miniatura, adatto per l'ESP32. Si installa semplicemente scaricando il file *microdot.py* e inserendolo nella 
nostra ESP32.

LINK: https://microdot.readthedocs.io/en/latest/intro.html

``` python
from microdot import Microdot

app = Microdot()

@app.route("/")
async def index(request):
    html = """<h1>ESP32 server</h1><p><a href="/led/1">LED ON</a> | <a href="/led/0">LED OFF</a></p>"""
    return html

@app.route("/led/<stato>")
async def comando_led(request, stato):
    led.value(int(stato))
    return "LED: " + str(led.value())

# avvia il server sulla porta 80
app.run(port=80)
```

Da qui in poi... puoi mettere insieme i pezzi e far funzionare tutto da solo...

<br>
<br>
<br>
