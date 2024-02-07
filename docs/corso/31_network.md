# Connettere l'ESP32

In questa parte del corso andremo ad esplorare le potenzialità di rete presenti in ESP32!
In particolare vedremo:

- come collegare l'ESP32 ad una rete WIFI
- come configurare l'ESP32 per creare una propria rete Wifi, a cui far connettere altri dispositivi.
- come gestire la connettività Bluetooth, presente nel microcontrollore.

Per la gestione del Wifi, si utilizza il modulo `network`, già disponibile nel bundle MicroPython.

Vediamo come

<!-- ################################################################################# -->
## Collegarsi ad una rete Wifi


A volte visualizzare un pò di codice ben commentato rende le cose più semplici che tante parole...

``` python
# RICORDA di importare il modulo network.
import network

# crea l'oggetto interfaccia WLAN
# l'opzione network.STA_IF crea una interfaccia in grado di connettersi ad una rete Wifi
wlan = network.WLAN(network.STA_IF)

# attivala
wlan.active(True)

# scansiona per individuare le reti Wifi disponibili 
network_list = wlan.scan()

# connette l'interfaccia WLAN alla rete Wifi SSID con chiave KEY
wlan.connect('ssid', 'key')

# controlla SE l'interfaccia è connessa al Wifi.
# Ritorna True/False
wlan.isconnected()

# visualizza la configurazione di rete.
# Ritorna la tupla ( 'IP', 'SubnetMask' , 'gateway' , 'DNS')
wlan.ifconfig()
```



<!-- ################################################################################# -->
## Creare una rete Wifi Ad-hoc

Il codice che presentiamo adesso serve invece a configurare l'interfaccia WLAN per creare una propria rete
Wifi, a cui evetualmente far connettere altri dispositivi.

Vediamo il codice:

``` python
# RICORDA di importare il modulo network.
import network

# crea l'oggetto interfaccia WLAN
# l'opzione network.AP_IF crea una interfaccia Access-Point
wlan = network.WLAN(network.AP_IF)

# Imposta il nome (si chiama SSID) della rete Wifi
wlan.config(ssid='ESP-AP')

# imposta il numero massimo di connessioni simultanee alla 'nuova' rete Wifi
wlan.config(max_clients=10)

# attivala
wlan.active(True)
```


<!-- ################################################################################# -->
## Bluetooth

Quando arriva, arriva...


<!-- ################################################################################# -->
## WebREPL

Questo con calma... più avanti...

<!-- https://docs.micropython.org/en/latest/esp8266/tutorial/repl.html?highlight=webrepl -->



<!-- ################################################################################# -->
## Web Server

Questo da qualche parte bisognerà metterlo...


<br>
<br>
<br>

