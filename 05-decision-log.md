# Decision log

Registra le decisioni di prodotto, UX e architettura.

## Regole
- Una decisione per blocco.
- Sempre il motivo e le alternative considerate.
- Sempre quando rivalutarla.
- Le decisioni storiche non si modificano: se cambi idea, aggiungi una nuova voce che rimanda alla vecchia.

---

## 2026-09-25: Lovable come strumento di costruzione

Decisione: costruire l'MVP su Lovable, con lo stack che impone (React, Vite, TypeScript, Tailwind, shadcn/ui).
Motivo: app a pagina singola, backend minimo, serve arrivare a un MVP usabile in pochi giorni.
Alternative considerate: Claude Code, scartato perché richiede di gestire deploy e segreti a mano per un'app che non ne ha bisogno.
Impatto: stack non negoziabile; la logica server sta nelle edge function.
Rivalutare quando: servono logiche server complesse o controllo fine sul codice.

---

## 2026-09-25: salvataggio in localStorage

Decisione: le valutazioni si salvano nel localStorage del browser.
Motivo: single user, nessun login, uso su un dispositivo.
Alternative considerate: Lovable Cloud con tabella `assessments`, rimandato perché richiede auth e RLS che l'MVP non usa.
Impatto: nessuna tabella; le valutazioni vivono in un solo browser e si perdono se l'utente cancella i dati del sito.
Rivalutare quando: serve usare l'app su più dispositivi, condividere il piano o aprirla a più utenti.

---

## 2026-09-25: gateway AI di Lovable per le mosse

Decisione: la edge function chiama il modello attraverso il gateway AI di Lovable. Lovable Cloud si attiva solo per edge function e secret.
Motivo: niente chiavi esterne da gestire, billing unificato, la via più rapida.
Alternative considerate: Claude con chiave Anthropic come secret, da preferire se le mosse non tengono lo stile richiesto.
Impatto: dipendenza dal gateway; il system è il 04 incollato per intero nella funzione.
Rivalutare quando: le mosse risultano generiche o fuori stile nei test del prompt 3.

---

## 2026-09-25: recharts per la ruota

Decisione: il radar si disegna con recharts.
Motivo: supporta radar con più serie, tick personalizzati e overlay, ed è già usato nei progetti Lovable.
Alternative considerate: SVG scritto a mano, più controllo ma più codice da mantenere.
Impatto: una dipendenza in più.
Rivalutare quando: i tick custom o l'overlay tratteggiato non si ottengono senza forzature.

---

## 2026-09-25: mosse solo sulle tre aree più alte

Decisione: l'AI genera le mosse solo per le tre aree col punteggio più alto; a parità vince l'ordine delle aree nel master plan.
Motivo: principio del prodotto, partire dai punti forti riduce l'attrito di introdurre l'AI nel lavoro quotidiano.
Alternative considerate: mosse su tutte le aree, scartato perché diluisce il piano; mosse sulle aree più basse, contrario al principio.
Impatto: una sola chiamata AI con tre aree.
Rivalutare quando: gli utenti chiedono mosse sulle aree deboli dopo aver completato il piano.

---

## 2026-09-25: export solo markdown, niente login

Decisione: l'export è un file markdown; niente login nell'MVP.
Motivo: il markdown si legge ovunque e basta per portare il piano fuori dall'app; il login non serve con il salvataggio nel browser.
Alternative considerate: PDF stilizzato della ruota, rimandato perché costa più del valore che aggiunge ora.
Impatto: nessuna libreria PDF, nessuna auth.
Rivalutare quando: arriva il salvataggio in cloud.

---

## Template

Decisione:
Motivo:
Alternative considerate:
Impatto:
Rivalutare quando:
