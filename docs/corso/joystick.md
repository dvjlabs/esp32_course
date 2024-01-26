# Creazione di un joystick con ESP32

## Componenti e collegamenti

Un joystick è un dispositivo di input utilizzato per controllare la posizione di un cursore o di un oggetto su uno schermo, soprattutto nei contesti di videogiochi, simulatori di volo o altre applicazioni interattive. Si tratta di una leva o di un dispositivo simile che può essere spostato in diverse direzioni per controllare il movimento di un cursore o di un'entità virtuale.

I joystick possono avere varie forme e dimensioni, ma in genere consistono in una leva che può essere inclinata o spostata in diverse direzioni.

Esso riceve gli input in 2 assi, X e Y. Inoltre il joystick ha a disposizione anche l'asse Z che ci servirà per indicare la pressione o meno del joystick stesso.

![esempio di joystick](joystick.jpg)

In figura vediamo anche i collegamenti elettrici che il nostro joystick richiede. Nel nostro caso, invece della tensione di 5V come indicato in figura, useremo una tensione di 3,3 volt (come vedremo in seguito).

Spostare il joystick lungo l'asse X o Y, ha effetto su una resistenza variabile. Premere il joystick significa aprire o chiudere un pulsante. Di seguito vediamo il circuito elettrico presente all'interno di un joystick.
![esempio di joystick](schemajoy.jpg)

I due segnali VRX e VRY sono due segnali analogici che andranno collegati direttamenti a due pin GPIO del componente ESP32 con funzione di convertitore Analogico-Digitale.

**Approfondimento-segnale analogico**:
Un aspetto importante dei segnali analogici è che possono assumere un numero infinito di valori all'interno di un intervallo specifico. Ciò li distingue dai segnali digitali, che rappresentano l'informazione in modo discreto, assumendo solo un numero finito di valori discreti. I segnali analogici sono suscettibili a interferenze e degradazioni durante la trasmissione o la manipolazione, ma forniscono una rappresentazione più fedele delle grandezze fisiche originali rispetto ai segnali digitali in molte applicazioni.

La lista dei componenti necessari è indicata nella figura seguente:
![schema elettrico di un joystick](listacomponenti.jpg)
I componenti andranno collegati secondo lo schema della figura sotto. Fare attenzione che nel pin del joystick in cui è indicato il valore di 5V, in realtà bisogna mettere il valore di 3.3V che potete trovare nel pin in alto a sinistra del componente ESP32.

![schema elettrico di un joystick](schema1.jpg)

## Codice

I segnali elettrici collegati ai pin 13 e 14 vengono trasformati in segnali digitali (numeri) i quali sono degli input per il nostro programma.
Al pin 12 arriverà in input o un valore alto (1 o HIGH) o valore basso (0 o LOW).

Il codice è sotto riportato.

```python


```
