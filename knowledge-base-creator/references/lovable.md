# Lovable

## Stack
Imposto dallo strumento: React, Vite, TypeScript, Tailwind, componenti shadcn/ui. Non proporre alternative e non fare la domanda sullo stack. Nel `07` scrivi lo stack come dato di fatto e nel `05` registralo come vincolo dello strumento.

## Dove va ogni file
Lovable ha due livelli di contesto permanente: la workspace knowledge, unica e condivisa da tutti i progetti, e la project knowledge del singolo progetto. Lovable applica meglio istruzioni brevi e concrete, quindi la knowledge va condensata: i file completi restano la fonte, nella knowledge va la versione essenziale.

- `00-regole-permanenti.md` va nella workspace knowledge. Si incolla una volta sola: se l'utente ce l'ha già da un progetto precedente, la aggiorna invece di duplicarla.
- `01-master-plan.md` e `02-design-system.md` vanno nella project knowledge, condensati: scopo, utenti, scope, fuori scope, token e regole di componente. Via i paragrafi discorsivi.
- `07-architecture.md` va nella project knowledge per le parti che l'agente deve rispettare: struttura cartelle, modello dati, nomi delle tabelle, contratti delle funzioni.
- `04-contesto-ai-runtime.md` non va mai nella knowledge. È il system della edge function che chiama il modello, guida l'AI che risponde dentro l'app a runtime e non l'agente che costruisce. Nel prompt che integra l'AI chiedi di incollarlo per intero nella funzione.
- `03`, `05` e `06` restano all'utente: il `03` lo usa per dare i prompt, il `05` e il `06` per tenere traccia. Se il progetto è sincronizzato su GitHub, conviene salvarli anche nel repository in `docs/`.

L'indice di posa nel `03` deve dire queste cose in modo operativo: "Apri le impostazioni del workspace, sezione Knowledge, incolla il contenuto di 00".

## Database
- Lovable Cloud: backend predefinito dei nuovi progetti, costruito sullo stack di Supabase. Tabelle, auth, storage, edge functions e secret si gestiscono dall'editor, senza account Supabase separato. Scegli questa strada quando l'utente non ha motivi per possedere il backend.
- Supabase con account proprio: stessa tecnologia, ma il progetto Supabase è dell'utente, con la dashboard completa e la possibilità di portare il backend altrove. Il collegamento si fa dalle integrazioni di Lovable. Nel `05` la voce deve spiegare perché si è scelto l'uno o l'altro.
- Nessun database: localStorage del browser. Va bene per single user su un solo dispositivo, senza login. Nel `05` il "rivalutare quando" è: serve sincronizzazione tra dispositivi, multiutenza o condivisione.

Con database e utenti multipli, l'architettura deve prevedere le policy RLS su ogni tabella con dati personali, e il prompt della persistenza deve chiederle esplicitamente.

## AI a runtime
Sempre dietro una edge function, mai chiamata dal browser, la chiave resta un secret lato server.
- Gateway AI di Lovable: niente chiavi esterne da gestire, billing unificato. La via più rapida.
- Claude: chiave Anthropic come secret, chiamata dalla stessa edge function.
- Altri provider: stesso schema, chiave come secret.

## Come scrivere i prompt
- Il prompt 0 va in modalità piano: l'agente legge la knowledge e propone il piano, senza toccare il codice. L'utente lo confronta con il `06` prima di passare alla costruzione.
- Il prompt dell'interfaccia chiede "solo frontend, dati finti, niente edge function, niente tabelle".
- Un prompt, un blocco verificabile nell'anteprima. Mai due funzioni nello stesso prompt.
- Ogni prompt ripete in una riga cosa non creare ancora: backend, auth, tabelle, funzioni che arrivano dopo.
- Nella sezione "Se qualcosa si rompe" del `03`: se un prompt rompe l'app, meglio ripristinare la versione precedente dalla cronologia e riformulare il prompt più stretto, invece di accumulare prompt di correzione sopra un codice rotto.
