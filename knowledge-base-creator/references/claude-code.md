# Claude Code

## Stack
Non imposto. Proponi uno stack motivato in una riga e chiedi solo conferma. Proposte di partenza:
- app web con backend e Supabase: Next.js con TypeScript e Tailwind, client Supabase, deploy su Vercel;
- app web senza backend: React, Vite, TypeScript e Tailwind;
- prototipo locale con database: SQLite con Drizzle.
Il motivo va legato all'idea, non allo stack in sé: per esempio "Next.js perché ti servono route server per chiamare il modello senza esporre la chiave".

## Dove va ogni file
- `CLAUDE.md` nella radice del repository: regole permanenti (`00`) più un indice breve che importa i file di progetto con la sintassi `@docs/01-master-plan.md`. Tienilo corto, perché viene caricato a ogni sessione.
- `docs/`: tutti gli altri file della knowledge base. Claude Code li apre quando il task lo richiede, quindi qui ha senso dividere il `07` in `07-architecture.md`, `08-database.md` e `09-api.md`, ma solo se c'è materiale vero per ognuno.
- `04-contesto-ai-runtime.md` diventa il system della route server che chiama il modello, caricato da file nel codice.
- Segreti in `.env.local`, esclusi da git, con un `.env.example` che elenca le variabili senza valori. Nel `06` c'è un task per questo.

L'indice di posa nel `03` dice: crea `CLAUDE.md` con questo contenuto, metti gli altri file in `docs/`, poi avvia Claude Code nella cartella e dai il prompt 0.

## Database
- Supabase: client con chiave pubblica nel browser solo se ci sono policy RLS su ogni tabella; tutto il resto passa dal server con la chiave di servizio, che non esce mai dal server. Migrazioni versionate nel repository.
- Nessun database: localStorage.
- Altro (SQLite, Neon, altro Postgres): stringa di connessione nelle variabili d'ambiente, migrazioni nel repository.

## Come scrivere i prompt
Su Claude Code i prompt sono task. Ognuno ha:
- l'obiettivo in una frase e i file di `docs/` da leggere prima;
- cosa costruire e cosa non toccare;
- i comandi di verifica da lanciare alla fine (build, lint, test se ci sono);
- la richiesta di aggiornare `docs/06-tasks.md` e, se è cambiata una scelta, `docs/05-decision-log.md`;
- un commit con un messaggio che dice cosa è stato fatto.

Il prompt 0 va in plan mode: Claude Code legge `CLAUDE.md` e `docs/`, propone il piano e aspetta l'approvazione.

Nella sezione "Se qualcosa si rompe": `git` è la rete di sicurezza, quindi si torna all'ultimo commit che funzionava e si riformula il task più stretto.
