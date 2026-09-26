# Replit

## Stack
Non imposto. Proponi uno stack motivato in una riga e chiedi solo conferma. Proposta di partenza per un'app web con backend: React e Vite nel frontend, Express nel server, Drizzle come ORM sul PostgreSQL, tutto nello stesso progetto. Motivo da dare all'utente: è lo stack che l'Agent di Replit gestisce con meno attrito, con un solo progetto da deployare. Se l'app non ha backend, basta React e Vite.

## Dove va ogni file
Il contesto permanente dell'Agent sta nel file `replit.md` nella radice del progetto, che l'Agent rilegge a ogni sessione.

- `replit.md` contiene le regole permanenti (`00`) e un riassunto operativo di master plan, design system e architettura, con il rimando ai file completi.
- Tutti i file della knowledge base vanno anche in `docs/` nel progetto, così l'Agent li apre quando il task lo richiede.
- `04-contesto-ai-runtime.md` diventa il system della route del server che chiama il modello, per esempio caricato da `server/prompts/` come file di testo. Non va nel `replit.md`.

L'indice di posa nel `03` dice: crea `replit.md` con questo contenuto, crea la cartella `docs/` con questi file, poi dai il prompt 0.

## Database
- PostgreSQL interno: si attiva dal progetto e inserisce da solo `DATABASE_URL` e le altre credenziali nelle variabili d'ambiente, con database di sviluppo e di produzione separati. Alcune guide segnalano che il database va in sospensione dopo pochi minuti senza query: aggiungi al `06` un task per gestire la riconnessione e nel `05` una nota da verificare sulla documentazione aggiornata.
- Supabase: le credenziali vanno nei Secrets di Replit, mai nel codice. Con utenti multipli, policy RLS su ogni tabella con dati personali.
- Nessun database: localStorage, come per gli altri strumenti.

Su Replit non ci sono edge functions: la logica lato server, comprese le chiamate al modello AI, sta nelle route del server dell'app. Il `07` lo deve dire in modo esplicito, perché i modelli tendono a proporre edge functions per abitudine.

## AI a runtime
Chiave del provider nei Secrets, chiamata solo dal server, mai dal browser. Il contratto della route (richiesta e risposta) va nel `07` identico al formato di output del `04`.

## Come scrivere i prompt
- Prompt 0: chiedi all'Agent di leggere `replit.md` e i file in `docs/` e di rispondere con un piano, senza scrivere codice. Se l'Agent ha una modalità piano, usala.
- Stessa sequenza degli altri strumenti: interfaccia con dati finti, persistenza, AI, funzioni secondarie una per prompt.
- Ogni prompt chiude con le verifiche e con "aggiorna `replit.md` se hai cambiato struttura o decisioni".
- Nella sezione "Se qualcosa si rompe": torna al checkpoint precedente e riformula il prompt più stretto, invece di accumulare correzioni.
