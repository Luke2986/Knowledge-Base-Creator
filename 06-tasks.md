# Tasks

## Prompt 1: interfaccia con stato in memoria
- [ ] Layout della pagina con header. Fatto quando: eyebrow, titolo e riga introduttiva compaiono con i font del design system.
- [ ] Otto slider con nome, descrizione e valore. Fatto quando: ogni slider va da 1 a 10 e mostra il valore in mono ambra.
- [ ] Ruota radar. Fatto quando: la forma cambia mentre muovi uno slider, senza scatti.
- [ ] Media dei punteggi sopra la ruota. Fatto quando: la media cambia con gli slider e ha un decimale.
- [ ] Domande guida. Fatto quando: le tre domande del master plan sono visibili durante la compilazione.
- [ ] Top 3 con regola di parità. Fatto quando: con due aree a pari punteggio vince quella che viene prima nell'ordine delle aree.
- [ ] Card delle aree forti con chip e textarea. Fatto quando: le note restano legate all'area anche se la top 3 cambia.
- [ ] Validazione delle note. Fatto quando: oltre 1000 caratteri la textarea non accetta altro testo e lo dice.
- [ ] Bottone Azzera. Fatto quando: slider al valore iniziale e note vuote.
- [ ] Layout responsive. Fatto quando: sotto 640px una colonna, da 1024px due colonne.

## Prompt 2: salvataggio nel browser, storico e confronto
- [ ] Salvataggio snapshot. Fatto quando: dopo il salvataggio e il ricaricamento della pagina la voce è nello storico.
- [ ] Storico con data e media. Fatto quando: le voci sono in ordine dalla più recente.
- [ ] Ricarica ed elimina. Fatto quando: Ricarica riporta slider, note e mosse; Elimina toglie solo quella voce.
- [ ] Overlay di confronto. Fatto quando: la valutazione scelta compare in teal tratteggiato sotto la forma ambra.
- [ ] Stato storage non disponibile. Fatto quando: con storage bloccato compare la nota e l'app funziona nella sessione.
- [ ] Stato vuoto. Fatto quando: senza salvataggi lo storico non compare.

## Prompt 3: generazione AI delle mosse
- [ ] Lovable Cloud attivo senza tabelle. Fatto quando: la edge function si deploya e non esistono tabelle nel progetto.
- [ ] Edge function `generate-moves` con il 04 come system. Fatto quando: una richiesta di prova restituisce JSON con le tre chiavi.
- [ ] Controllo della risposta del modello. Fatto quando: una risposta con chiavi diverse o JSON non valido produce un errore leggibile e non rompe la pagina.
- [ ] Stato di caricamento. Fatto quando: bottone disabilitato con spinner e skeleton nelle card.
- [ ] Stato di errore. Fatto quando: con la rete disattivata compare la riga rossa con il motivo.
- [ ] Mosse nello snapshot. Fatto quando: una valutazione ricaricata dallo storico mostra le mosse.

## Prompt 4: export del piano
- [ ] Export markdown. Fatto quando: il file `piano-amplificazione-pm.md` si scarica al primo clic e contiene titolo, data, media, punteggi, mosse e note.
- [ ] Export senza mosse. Fatto quando: un'area senza mosse lo dice nel file invece di restare vuota.

## QA prima di chiudere l'MVP
- [ ] Mobile. Fatto quando: a 375px nessun elemento esce dallo schermo e gli slider si usano con il pollice.
- [ ] Accessibilità. Fatto quando: tutta la pagina si usa da tastiera con il focus visibile e il contrasto è AA.
- [ ] Tempi. Fatto quando: una valutazione completa richiede meno di 5 minuti e le mosse arrivano in meno di 10 secondi.
- [ ] Voce. Fatto quando: nessun testo dell'app e nessuna mossa contiene trattino lungo, emoji o parole bandite.
- [ ] Nessun segreto nel client. Fatto quando: la ricerca della chiave nel codice del browser non trova nulla.

## Dopo l'MVP
- [ ] Confronto a parole tra due valutazioni con una seconda chiamata AI
- [ ] Auth e tabella `assessments` con RLS
- [ ] Condivisione del piano via link
