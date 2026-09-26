# Prompt per Lovable

## Indice di posa
1. Impostazioni del workspace, sezione Knowledge: incolla il contenuto di `00-regole-permanenti.md`. Se ci sono già le regole da un progetto precedente, aggiornale invece di duplicarle.
2. Impostazioni del progetto, sezione Knowledge: incolla la versione condensata di `01-master-plan.md` (cosa, per chi, otto aree con chiavi, scope, fuori scope), `02-design-system.md` (token, componenti, stati, breakpoint) e `07-architecture.md` (cartelle, modello dati, contratto della edge function).
3. `04-contesto-ai-runtime.md` non va nella knowledge: guida l'AI che risponde dentro l'app, non l'agente che la costruisce. Lo incolli nella edge function al prompt 3.
4. `05-decision-log.md` e `06-tasks.md` restano a te per tenere traccia.

## Come usare questi prompt
Uno alla volta, nell'ordine. Dopo ogni prompt fai le verifiche elencate e passa al successivo solo se tornano tutte.

## Prompt 0: il piano
In modalità piano.

> Leggi la knowledge del workspace e del progetto. Proponi il piano di costruzione in quattro fasi: interfaccia con stato in memoria, salvataggio nel browser con storico e confronto, generazione AI delle mosse, export markdown. Per ogni fase elenca i file che creerai. Non scrivere codice.

Verifica: il piano ha quattro fasi in quest'ordine, rispetta la struttura cartelle del 07 e non aggiunge login, tabelle o pagine in più.

## Prompt 1: interfaccia con stato in memoria

> Costruisci la single page seguendo il design system in knowledge: token, font, componenti, breakpoint. Dall'alto: header con eyebrow mono, titolo in Fraunces e una riga che invita a dare un voto da 1 a 10 a ogni area senza idealizzarsi, partendo dai punti alti. Corpo a due colonne da 1024px in su: a sinistra la ruota radar con recharts su pannello blu notte, a destra gli otto slider con nome, descrizione e valore in mono ambra, con le otto aree e le chiavi della knowledge. La ruota si aggiorna mentre muovi gli slider. Sotto, le tre domande guida del master plan. Poi la sezione punti di forza: le tre aree col punteggio più alto, a parità vince l'ordine delle aree, con chip del voto e textarea per le note. Barra azioni con i bottoni Salva valutazione di oggi, Esporta il piano e Azzera: per ora funziona solo Azzera, gli altri due sono visibili e disabilitati. Stato in memoria con un hook `useAssessment`. Non creare ancora salvataggio nel browser, edge function, backend o tabelle.

Verifica prima di proseguire:
- la ruota cambia forma mentre muovi uno slider, senza scatti;
- con due aree a pari punteggio la top 3 segue l'ordine delle aree;
- sotto 640px la pagina è a una colonna con la ruota sopra;
- Azzera riporta tutti gli slider al valore iniziale e svuota le note;
- ogni slider si usa da tastiera con il focus visibile.

## Prompt 2: salvataggio nel browser, storico e confronto

> Aggiungi il salvataggio con localStorage attraverso `src/services/storage.ts`, seguendo il modello dati e la chiave di storage del 07. Salva valutazione di oggi crea uno snapshot con data, punteggi, note e media. Sotto la barra azioni mostra lo storico con data e media per ogni voce, con i comandi Ricarica, Sovrapponi alla ruota ed Elimina. Sovrapponi mostra la valutazione scelta come overlay teal tratteggiato. Se localStorage non è disponibile, mostra la nota tenue prevista negli stati del design system. Non creare backend, tabelle o login.

Verifica prima di proseguire:
- salvi, ricarichi la pagina del browser e la valutazione è nello storico;
- Ricarica riporta slider e note allo snapshot;
- l'overlay teal compare sotto la forma ambra e sparisce quando lo togli;
- Elimina rimuove solo quella voce;
- in una finestra con storage bloccato compare la nota e l'app non si rompe.

## Prompt 3: generazione AI delle mosse

> Attiva Lovable Cloud solo per edge function e secret, senza creare tabelle. Crea la edge function `generate-moves` secondo il contratto nel 07: riceve le tre aree forti con chiave, punteggio e note, chiama il modello attraverso il gateway AI di Lovable e restituisce un oggetto con, per ogni chiave, un array di 2 o 3 stringhe. Come system usa per intero il testo che ti incollo qui sotto, senza riassumerlo. La funzione controlla che la risposta sia JSON valido con esattamente le chiavi ricevute; se non lo è, restituisce un errore leggibile. Nel frontend, `src/services/ai.ts` chiama la funzione e il bottone Genera le mosse con l'AI mostra lo stato di caricamento con spinner e skeleton, poi le mosse dentro ogni card sopra la textarea. In caso di errore, riga rossa sotto il bottone con il motivo. Le mosse generate entrano nello snapshot quando salvi.
>
> [incolla qui il contenuto di 04-contesto-ai-runtime.md]

Verifica prima di proseguire:
- arrivano 2 o 3 mosse per ognuna delle tre aree in meno di 10 secondi;
- nessuna mossa contiene emoji, trattino lungo o parole bandite;
- una nota scritta in una card cambia le mosse di quell'area;
- con la rete disattivata compare la riga di errore e il bottone torna attivo;
- salvi, ricarichi dallo storico e le mosse ci sono;
- nel codice del browser non c'è nessuna chiave.

## Prompt 4: export del piano

> Attiva Esporta il piano attraverso `src/services/export.ts`. Il file markdown contiene titolo, data, media, i punteggi area per area e, per ognuna delle tre aree forti, nome, voto, mosse generate e note personali. Il file si scarica come `piano-amplificazione-pm.md`. Niente trattino lungo nel testo del file. Non toccare gli altri servizi.

Verifica prima di proseguire:
- il file si scarica al primo clic;
- aperto in un editor qualsiasi si legge senza markup rotto;
- se le mosse non sono ancora state generate, l'export lo dice nella sezione dell'area invece di lasciarla vuota.

## Se qualcosa si rompe
Se un prompt rompe l'app, ripristina la versione precedente dalla cronologia di Lovable e riformula il prompt più stretto, per esempio dividendolo in due. Evita di accumulare prompt di correzione sopra un codice rotto.
