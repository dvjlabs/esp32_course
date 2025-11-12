# Il multimetro

Un multimetro digitale è uno strumento che permette di misurare valori di:  
1. Corrente
2. Tensione
3. Resistenza

I multimetri digitali possono cambiare di colore e forma, ma la struttura principale è la stessa a quella che si può vedere nella figura seguente.

![Multimetro digitale](images/multimetro-tutorial.jpg)  

E' composto da tre parti:
1. display
2. manopola di selezione
3. porte o contatti dove inserire le punte metalliche

Il display di solito è a quattro cifre e ha la possibilità di visualizzare un segno negativo. Alcuni multimetri hanno il display illuminato per una migliore visualizzazione in condizioni di scarsa luce.
La manopola di selezione permette all'utente di impostare il multimetro per leggere diversi valori, come corrente (A) , tensione (V) e resistenza (Ω).
Per quanto riguarda la tensione, si possono eseguire misure di tensione continua(V) e di tensione alternata (V~).  

![Manopola di selezione](images/selezione-manopola.jpg)

Due sonde sono collegate a due porte sul frontale dell'unità. COM sta per comune ed è quasi sempre collegata a terra o '-' di un circuito. La sonda COM è convenzionalmente nera, ma non vi è alcuna differenza tra la sonda rossa e la sonda nera, sono solo di colore diverso. 10A è la porta speciale utilizzata per misurare correnti elevate (superiori a 200mA). mAVΩ è la porta dove la sonda rossa è convenzionalmente collegata. Questa porta permette la misura di correnti (fino a 200mA), la tensione (V), e resistenza (Ω).

## Misura della resistenza con un multimetro

Le normali resistenze hanno codici di colore su di loro. Ci sono un sacco di calcolatori online che sono facili da usare. Tuttavia, se mai vi trovate senza accesso a internet, un multimetro è molto utile per misurare la resistenza.
​
Scegliere una resistenza casuale e impostare il multimetro per l'impostazione 20kΩ. Quindi tenere le sonde sui reoferi del resistore.
![Misura Resistenza](images/multimetro-resistenza.jpg)

Ricordarsi di portare il selettore della manopola su un valore di resistenza. Se ad esempio selezioniamo 2kΩ, questo significa che possiamo misurare resistenze di valore non più grande di 2kΩ.
Se ad esempio la resistenza sarà da 1kΩ nominale, potrà succedere di leggere il valore di 0.97 (ogni resistenza ha una sua tolleranza e non sarà quasi mai precisa).
Se invece metteremo una resistenza ad esempio da 10kΩ, il multimetro darà un valore di 1 che significa che abbiamo superato il fondo scala (in questo caso 2kΩ). Dovremo allora mettere il cursore su un valore più alto.

## Misura della continuità
Un caso particolare della misura della resistenza è quello della continuità.
Con questo termine si intende dire: verificare che tra due punti ci sia una resistenza di 0Ω. Detto in altri termini, con questa misura si vede se tra due punti del circuito ci sia un cortocircuito.
Il Selettore deve essere messo nel simbolo del diodo come visto in figura.

![continuità](images/continuità.jpg)

Se c'è continuità (o cortocircuito), il multimetro ci avverte con un suono continuò.


## Misura della tensione

### Misura della corrente in continua

![tensione continua](images/volt-dc_orig.jpg)

Supponiamo di voler misurare la tensione di una batteria da 1.5Volt (valore nominale).
Dobbiamo mettere i puntali delle sonde ai capi della batteria e il selettore della manopola su 2V (fondoscala maggiore del valore nominale della batteria). Nel nostro caso, dal momento che la batteria è nuova, si legge un valore di 1,629V.

![misura batteria](images/multimetro-misura-tensione.jpg)

### Misura della corrente in alternata

In questo caso possiamo misurare valore di tensione in alternata, ad esempio la tensione che abbiamo nelle prese di casa (220V).

![misura batteria](images/volt-ac_orig.jpg)

> Vi consiglio di non farlo a meno che non siate dei provetti elettricisti in quanto la tensione 220V è pericolosa (letale).
> 

## Misura della corrente

Per fare una misura della corrente bisogna mettersi in serie con il circuito da misurare. In pratica, dovremmo interrompere il circuito ed inserirci con le nostre sonde nel circuito interrotto in modo che la corrente entri in una sonda, passi all'interno del multimetro e poi esca dall'altra sonda in modo da rientrare nel circuito.
Il selettore dovrà essere ruotato in modo da selezionare un fondo scala appropriato (da 20uA a 10A).

![corrente](images/corrente.jpg)
> NOTA: Nel caso di 10A, bisogna cambiare la posizione della sonda rossa nel punto di ingresso più a sinistra (vedi figura in cima al documento).


