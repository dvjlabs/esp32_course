# Umidità del terreno - Moisture Sensor 

Il Grove Moisture Sensor è un sensore che misura l'umidità del suolo.  
Funziona inserendo le due sonde metalliche nella terra: passa una piccola corrente tra di esse e, in base alla resistenza del suolo (che varia con la quantità d'acqua presente), restituisce un valore analogico — più il suolo è bagnato, più alta è la lettura.
È compatibile con Arduino, Raspberry Pi e altre schede tramite il sistema Grove (connettore a 4 pin), quindi è semplice da collegare senza saldature. Viene usato spesso in progetti di irrigazione automatica o monitoraggio di piante. 

Puoi collegare il Grove-Moisture Sensor direttamente a una scheda con ESP32. Può essere collegato a un pin analogico dell'ESP32 per leggere i valori.  

## Schema di collegamento
Il Grove-Moisture Sensor ha tre pin:
1. VCC (alimentazione)
2. GND (massa)
3. SIG (segnale)  
   
## Collegamento:  
- VCC del sensore → 3.3V della ESP32
- GND del sensore → GND della ESP32
- SIG del sensore → Un pin analogico dell'ESP32 (ad esempio, GPIO34)  
> Nota: L'ESP32 opera a 3.3V, quindi alimentare il sensore a 3.3V è essenziale per evitare di danneggiare la scheda.  

