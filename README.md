# ProgettoAudio
Installazione:
Aprire il file Matlab “Codice.m”.
Importare tutti i file audio nella stessa cartella.

Utilizzo:
Andare a inserire il titolo della file audio, ad esempio “furelise.wav” o “speech.wav”, nella linea 8 di audioread, per inserire il segnale di input.
Modificare “sFactor” a piacere, per rallentare o velocizzare la traccia.
Avviare il programma.

Descrizione:
L’applicativo va a rallentare o velocizzare una traccia audio WAVE, senza alternarne il pitch, utilizzando la tecnica WSOLA.
Una volta caricato un file audio, vengono dichiarate le variabili L, Sout, sFactor e delta_k.
Viene settato il primo frame dell’output.
Il ciclo while esterno si occupa di aggiornare l'indice del frame da analizzare.
Nel ciclo interno con delta_k definiamo un range in cui prendere i frame intorno a quello scalato. Per ognuno di questi frame calcoliamola correlazione con il frame che avremo analizzato se non avessimo fatto uno scalamento nel tempo. Per ogni correlazione prendiamo solamente il valore mediano (quello per cui i frame sono sovrapposti) e lo inseriamo in un vettore buffer.
Poi cerchiamo il valore massimo nel vettore buffer per individuare l'indice del frame più simile a quello non scalato.
Individuato il frame, lo modelliamo con una finestra di Hanning (per pesarlo) e lo sommiamo al vettore output.

Nel caso in cui sFactor (scaling factor) sia minore di 1, l'algoritmo sopra descritto creava una traccia rallentata ma la troncava alla durata del file in ingresso. Per rimediare abbiamo fatto la correlazione con il frame precedente a quello sotto analisi invece del frame non scalato, altrimenti alla metà del file in uscita non avremmo potuto fare la correlazione con nessun frame perchè il frame in ingresso era giunto al termine.
Il risultato è accettabile.

La traccia viene riprodotta e salvata in un file chiamato 'track.wav'.
