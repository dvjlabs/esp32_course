# Data is in the air

Comincio subito con le scuse... l'idea della lezione mi è venuta solo ieri pomeriggio: il resto del tempo ho solo corretto compiti!

L'idea è carina, ma... ci sarà da lavorare!!!


## Flask


Uno Web Framework rappresenta una collezione di librerie e moduli che permette ad uno web developer 
di scrivere applicazioni web senza occuparsi dei dettagli di basso livello.

> **Flask** è uno **Web Framework** scritto in Python,<br> 
> basato sul toolkit **WSGI Werkzeug** e sul template engine **Jinja2**.

**WSGI (Web Server Gateway Interface)** è una specifica che definisce una interfaccia universale 
di comunicazione fra un server web e una applicazione web: Werkzeug è semplicemente una implementazione 
WSGI utilizzata da Flask.

**Jinja2** è un template engine molto popolare per il linguaggio Python. Un sistema di web template combina 
un template (uno schema, uno scheletro) con delle sorgenti dati per creare una pagina web dinamica.

Flask è disponibile in pochi istanti tramite pip:

``` bash
$ pip install Flask
```

Pronti, via!

```python title="Primo esempio con Flask"
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello, World!"
```


```python title="Secondo esempio: due pagine visitabili da tutti!"
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello, World!"

@app.route("/prova")
def index():
    return "Sono la pagina prova!"

if __name__ == "__main__":
    app.run(host = "0.0.0.0", port = 5000, debug = False)
```

Terzo e ultimo esempio: struttura di una pagina con template!

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
```

## POST

Facciamo un paio di prove: uno il classico invio dati con GET e uno il tipico invio dati con POST.

**Inviamo dati con GET!!!**

```html title="prova"
<form action="https://www.google.it/search" method="GET">

<input name="q">
<input type="submit" value="Cerca con Google">
</form>
```

Il codice Flask per far funzionare la richiesta GET neanche lo scrivo... 


**Inviamo dati con POST!!!**

```html title="base.html"
<form action="/data" method="POST">

ID: <input name="id_sensor"><br>
TEMPERATURE: <input name="temperature"><br>

<input type="submit" value="INVIA">
</form>
```

```html title="data.html"
ID: {{ id_sensor }} <br>
TEMPERATURE: {{ temperature }} <br>
```

``` python
from flask import Flask,render_template,request

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("base.html")

# Questa serve dopo... pazienza...
@app.route("/saluta")
def ciaone():
    return "ciaone"

@app.route("/data", methods=["POST"])
def gestisci_dati():
    if request.is_json:
        payload = request.get_json()
    else:
        payload = request.form
    ids = payload["id_sensor"]
    temp = payload["temperature"]
    return render_template("data.html",id_sensor = ids, temperature = temp)
```

## ESP32 urequests

Quello che vogliamo fare adesso è inviare richieste GET e POST non tramite una pagina web, ma tramite una piccola applicazione (Micro)Python
in esecuzione sull'ESP32.

La libreria `urequests` è la libreria MicroPython standard per l'invio dati tramite HTTP. Vediamo due esempi banali di richiesta GET e POST.
Tutto il contorno dovrete inserirlo voi...

``` python title="richiesta GET"
import requests

try:
    response = requests.get("http://127.0.0.1:5000/saluta")
    print('Response content:', response.text)
except Exception as e:
    print('An error occurred during the request:', str(e))
```

Se invece vogliamo provare con una richiesta di tipo POST dobbiamo inviare i dati in un payload, che tipicamente non è altro che un dizionario.

``` python title="richiesta POST"
import requests

data = {}
data["id_sensor"] = "sensore1"
data["temperature"] = 37.5

try:
    response = requests.post("http://127.0.0.1:5000/data", json=data)
    print('Response content:', response.text)
except Exception as e:
    print('An error occurred during the request:', str(e))
```


## SQLite

Non è ancora pronto... ho cercato un pò su Internet e il tutorial migliore mi è sembrato questo: 
[https://www.sqlitetutorial.net/sqlite-python/](https://www.sqlitetutorial.net/sqlite-python/)

Semplice e completo di tutti gli argomenti che volevo affrontare!!!

* inizializzazione del database (CREATE)
  - creazione tabelle
* inserimento dati (INSERT)
* lettura dati (SELECT)



## dashboard

E' abbastanza ovvio ormai che la struttura del nostro progetto sarà la seguente:

Ogni dispositivo ESP32 monterà i propri sensori e sarà collegato al WiFi. Ogni TOT minuti (nei momenti di test, io direi ogni minuto... nella realtà... sarà sufficiente farlo ogni 30...). Raccoglierà i dati in un payload, in cui inserirà anche il proprio identificatore e invierà in POST tutti i dati ad un raccoglitore centrale.

Il *raccoglitore* fornirà un database `sqlite` e una *dashboard* HTML per la visualizzazione dei dati raccolti.

* dovrà occuparsi di inizializzare il database
* dovrà raccogliere i dati inviati in POST dai vari sensori
* dovrà esporre una dashboard per la visualizzazione dei dati stessi


La dashboard dovrebbe essere una struttura di questo tipo:

``` python title="dashboard"
from flask import Flask, render_template
import sqlite3, datetime

app = Flask(__name__)
DB = "sensors.db"

@app.route("/")
def dashboard():
    with sqlite3.connect(DB) as con:
        rows = con.execute(
            "SELECT device_id,ts,temp_dht,humidity,temp_ds "
            "FROM readings ORDER BY id DESC LIMIT 120"
        ).fetchall()
    return render_template("dashboard.html", rows=rows)
```

E la pagina HTML una cosa del genere!

``` html title="dashboard.html"
<!doctype html>
<html>
    <head>
        <title>Data is in the air: Dashboard</title>
        <!-- aggiorna la pagina automaticamente ogni 30 secondi -->
        <meta http-equiv="refresh" content="30">

        <style>
        body{font-family:sans-serif;padding:20px;max-width:900px;margin:auto}
        table{border-collapse:collapse;width:100%}
        th,td{border:1px solid #ccc;padding:8px 12px;text-align:left}
        th{background:#f0f0f0}
        </style>
    </head>
    <body>
        <h2>Sensor Dashboard</h2>
        <table>
            <tr>
                <th>Device</th><th>Timestamp</th><th>Temp DHT (°C)</th><th>Humidity (%)</th><th>Temp DS18B20 (°C)</th>
            </tr>
            {% for r in rows %}
            <tr>
                <td>{{r[0]}}</td><td>{{r[1]}}</td><td>{{r[2]}}</td><td>{{r[3]}}</td><td>{{r[4]}}</td>
            </tr>
            {% endfor %}
        </table>
    </body>
</html>
```


## Chart.js


Serve per creare grafici a partire dai dati registrati. Per stavolta non ho avuto tempo...


## MQTT

MQTT è un protocollo di messaggistica publish/subscribe pensato esattamente per dispositivi IoT leggeri. 
Invece di fare HTTP POST ogni minuto, ogni ESP32 si connette a un broker (un server centrale, tipo Mosquitto) 
e pubblica messaggi su un canale (detto topic). Il server Flask si iscrive a quei topic e reagisce in tempo reale.

Il vantaggio di utilizzare MQTT al posto di HTTP sta nella gestione delle batterie! Con HTTP, l'ESP32 tiene il WiFi attivo in attesa,
con MQTT + deep sleep, il dispositivo si sveglia, pubblica e torna a *dormire* in meno di 1 secondo! 

Una batteria da 3000 mAh passa da 2-3 giorni con HTTP a 6-12 mesi con MQTT + deep sleep!!!

<br>
<br>
<br>
