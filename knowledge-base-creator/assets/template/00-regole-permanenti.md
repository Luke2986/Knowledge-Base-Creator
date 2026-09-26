<!-- TEMPLATE. Fisso per struttura e quasi tutto il contenuto: adatta solo i punti marcati ADATTA allo strumento e al database. Su Lovable diventa la workspace knowledge, su Replit la prima parte di replit.md, su Claude Code la prima parte di CLAUDE.md. Tienilo sotto le 80 righe: viene letto a ogni task. -->

# Regole permanenti

Queste regole valgono per ogni task di questo progetto. Se una richiesta le contraddice, fermati e chiedi prima di procedere.

## Come lavori
- Fai solo quello che il prompt chiede. Non aggiungere funzioni, pagine, tabelle, dipendenze o backend non richiesti.
- Un passo alla volta: finisci il blocco richiesto, verifica che funzioni, fermati e aspetta il prompt successivo.
- Prima di cambiare un file che il prompt non nomina, spiega perché serve e chiedi.
- Se una scelta non è coperta dalla documentazione di progetto, proponi due opzioni con il motivo e aspetta la decisione.
- Non inventare dati, endpoint o nomi di tabella: usa quelli scritti nell'architettura.

## Struttura del codice
- I componenti fanno solo rendering: niente fetch, niente accesso allo storage, niente logica di business dentro i componenti.
- Chiamate al server, persistenza, AI ed export stanno nei servizi; gli hook coordinano stato, servizi e interfaccia.
- File sotto le 300 righe. Se un file le supera, dividilo e dillo.
- Tipi condivisi in un solo posto, mai ridefiniti in due file.
- Niente console.log nel codice che resta.

## Sicurezza
- Nessuna chiave o segreto nel codice client, mai. ADATTA: dove vivono i segreti (secret di Lovable Cloud / Supabase, Replit Secrets, .env.local escluso da git).
- ADATTA se c'è un database con utenti: ogni tabella con dati personali ha policy RLS; nessuna query dal client senza policy.
- Valida gli input dell'utente prima di salvarli o mandarli al modello.
- Le chiamate al modello AI passano sempre da una funzione lato server. ADATTA: edge function su Lovable, route del server su Replit e Claude Code.

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
