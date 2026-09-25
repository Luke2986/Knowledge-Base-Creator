# Master plan: ruota delle competenze PM

## Cosa stiamo costruendo
Un'app web per l'autovalutazione delle competenze da Product Manager. L'utente dà un voto da 1 a 10 a otto aree, vede la propria forma su una ruota radar e fa generare dall'AI le mosse concrete per rendere più forti le tre aree in cui è già forte. Esporta il piano e rifà la valutazione nel tempo per vedere se i numeri si spostano.

## Per chi
Product Manager e aspiranti tali che fanno il punto sulle proprie competenze una o due volte l'anno. Single user all'avvio, su un solo dispositivo.

## Il problema
Le autovalutazioni si fermano allo specchio: vedi i voti e finisce lì. Qui l'output è una decisione, cioè dove puntare l'AI per rendere più forti i punti in cui sei già forte.

## Principi
1. Parti dai punti forti, non dalle lacune: le mosse si generano sulle tre aree più alte, perché introdurre l'AI dove sei già solido riduce l'attrito.
2. Ogni mossa si può iniziare entro sette giorni, altrimenti non è una mossa.
3. L'AI propone, l'utente decide: le note personali pesano più di qualsiasi suggerimento generato.
4. Il grafico serve a vedere la forma, non è il risultato: il risultato è il piano esportato.

## Le otto aree
Le chiavi sono identiche nel 07 e nel 04.

1. `empatia`, empatia col cliente e discovery: capire a fondo bisogni, problemi latenti e contesto degli utenti.
2. `dati`, padronanza dei dati e dell'AI: analisi dei dati, esperimenti, capire cosa l'AI può e non può fare.
3. `strategia`, pensiero strategico e prioritizzazione: gestire i trade-off, definire la visione, ordinare il lavoro, compreso il product sense.
4. `leadership`, leadership cross-funzionale: allineare ingegneri, designer e stakeholder di business.
5. `storytelling`, storytelling e comunicazione: una narrazione adattata a team, senior management e stakeholder esterni.
6. `collaborazione`, collaborazione di team: lavorare in team multidisciplinari con fiducia e responsabilità condivisa.
7. `sperimentazione`, mentalità sperimentale e di apprendimento: iterazione, fallimento come dato, discovery continua.
8. `consapevolezza`, consapevolezza di sé e direzione di carriera: chiarezza su valori, forze e traiettoria di crescita.

## Scope MVP
Otto slider da 1 a 10, ognuno con nome e descrizione. Ruota radar che si aggiorna in tempo reale. Tre domande guida visibili durante la compilazione:

1. In quale area i colleghi ti chiedono aiuto senza che tu lo offra? [da verificare]
2. Quale parte del lavoro fai bene anche nelle settimane peggiori? [da verificare]
3. L'ultimo feedback positivo che hai ricevuto, a quale area si riferiva? [da verificare]

Sezione punti di forza con le tre aree più alte e un campo note per area. Generazione AI di 2 o 3 mosse per ognuna delle tre aree. Export del piano in markdown. Salvataggio della valutazione con data nel browser, storico con possibilità di ricaricare ed eliminare, confronto con una valutazione precedente sovrapposta sulla ruota. Bottone per azzerare la valutazione in corso.

## Fuori scope per ora
Login e multiutenza, perché l'uso previsto è personale e su un dispositivo. App mobile nativa. PDF stilizzato della ruota: l'export markdown basta. Conteggi e badge sui progressi.

## Fatto quando
Muovi gli slider e la ruota si forma senza scatti. Generi le mosse e arrivano 2 o 3 frasi azionabili per area, in italiano asciutto. Esporti un markdown leggibile fuori dall'app. Salvi, ricarichi e sovrapponi due valutazioni sulla stessa ruota.

## Metriche di successo
Valutazione completata in meno di 5 minuti. Mosse generate in meno di 10 secondi. Export riuscito al primo tentativo.

## Evoluzione, oltre l'MVP
Prima il confronto a parole tra due valutazioni, cosa è cresciuto e cosa è rimasto fermo, con una seconda chiamata AI che riusa il contesto di dominio: è il pezzo che chiude il ciclo. Poi auth con salvataggi in cloud, quando serve usare l'app su più dispositivi. Infine la condivisione del piano via link.

## Voce e lingua
Rimando alle regole permanenti (00), sezione voce dei testi dell'app.
