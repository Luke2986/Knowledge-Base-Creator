# Regole permanenti

Queste regole valgono per ogni task di questo progetto. Se una richiesta le contraddice, fermati e chiedi prima di procedere.

## Come lavori
- Fai solo quello che il prompt chiede. Non aggiungere funzioni, pagine, tabelle, dipendenze o backend non richiesti.
- Un passo alla volta: finisci il blocco richiesto, verifica che funzioni, fermati e aspetta il prompt successivo.
- Prima di cambiare un file che il prompt non nomina, spiega perché serve e chiedi.
- Se una scelta non è coperta dalla knowledge di progetto, proponi due opzioni con il motivo e aspetta la decisione.
- Non inventare dati, endpoint o nomi: usa quelli scritti nell'architettura.

## Struttura del codice
- I componenti fanno solo rendering: niente fetch, niente localStorage, niente logica di business dentro i componenti.
- Chiamate al server, persistenza, AI ed export stanno in `src/services/`; gli hook in `src/hooks/` coordinano stato, servizi e interfaccia.
- File sotto le 300 righe. Se un file le supera, dividilo e dillo.
- Tipi condivisi in `src/types/`, mai ridefiniti in due file.
- Niente console.log nel codice che resta.

## Sicurezza
- Nessuna chiave o segreto nel codice client, mai. I segreti stanno nei secret di Lovable Cloud.
- Le chiamate al modello AI passano sempre da una edge function. Il browser non chiama mai il modello.
- Valida gli input prima di salvarli o mandarli alla edge function: punteggi interi da 1 a 10, note di testo con lunghezza massima.

## Documentazione
- Quando completi un task, segnalo come fatto in 06-tasks.
- Quando cambi una scelta registrata nel decision log, aggiungi una nuova voce nel 05, non modificare quelle vecchie.
- Quando cambi struttura, modello dati o contratti, aggiorna il 07 nello stesso task.

## Voce dei testi dell'app
- Italiano, registro tu, asciutto, forma attiva.
- Le label dicono cosa succede ("Salva valutazione di oggi", non "Salva"); gli errori spiegano il motivo e cosa fare, senza scuse.
- Mai il trattino lungo, niente emoji, niente punti esclamativi di entusiasmo.
- Parole da non usare mai: sfida, leva, panorama, ecosistema, robusto, cruciale, fondamentale.
- Niente "non solo X, ma anche Y", niente frasi che iniziano con "E".
- Titoli in sentence case.
