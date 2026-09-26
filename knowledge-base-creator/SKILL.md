---
name: knowledge-base-creator
description: Costruisce la knowledge base di partenza per sviluppare un software con un builder AI (Lovable, Replit, Claude Code o altro) e la consegna in file markdown, cioè regole permanenti, master plan, design system, prompt da dare al builder uno alla volta, contesto per l'AI che gira dentro l'app, decision log, task e architettura. Parte dall'idea e dai dettagli che l'utente fornisce, chiede solo quello che manca con domande specifiche a opzioni, una per messaggio, e adatta prompt, stack e database allo strumento scelto. Usala ogni volta che l'utente ha un'idea di app, tool, SaaS, MVP o prototipo da costruire e vuole preparare il progetto prima di aprire il builder, anche se non nomina la knowledge base, per esempio quando dice "voglio costruire questa idea", "prepara i file per Lovable", "impostiamo il progetto", "fammi il master plan", "prompt per Replit", "CLAUDE.md per il progetto", "da dove parto per sviluppare X". Non serve per correggere un'app già in sviluppo avanzato né per scrivere direttamente il codice.
---

# Knowledge Base Creator

I builder AI costruiscono bene quando hanno un contesto fisso da rileggere e sbagliano quando devono ricostruirlo a ogni prompt. Questa skill prepara quel contesto: una serie di file markdown che descrivono cosa costruire, come deve apparire, con quale architettura, in che ordine, e con quali regole. L'utente porta l'idea, la skill chiede solo quello che solo lui può sapere, scrive il resto in bozza, controlla che i file siano coerenti tra loro e li consegna.

## I file che produci

| File | Quando | Cosa contiene |
|---|---|---|
| `00-regole-permanenti.md` | sempre | Come l'agente deve lavorare su qualsiasi task: passo per passo, sicurezza, struttura del codice, documentazione, voce |
| `01-master-plan.md` | sempre | Cosa, per chi, problema, principi, scope MVP, fuori scope, fatto quando, metriche, evoluzione |
| `02-design-system.md` | sempre | Carattere, gerarchia visiva, token, tipografia, layout e breakpoint, componenti, stati, accessibilità |
| `03-prompt-<strumento>.md` | sempre | Indice di posa dei file nello strumento e sequenza di prompt step by step fino all'MVP |
| `04-contesto-ai-runtime.md` | solo se l'app usa l'AI a runtime | Il system della funzione lato server che chiama il modello: ruolo, contesto di dominio, stile, vincoli di output |
| `05-decision-log.md` | sempre | Le decisioni già prese, con motivo, alternative e quando rivalutarle |
| `06-tasks.md` | sempre | Task raggruppati per prompt, ognuno con il suo "fatto quando", più QA |
| `07-architecture.md` | sempre | Stack, cartelle, modello dati, schema DB se c'è, contratti delle funzioni server, flussi, responsabilità dei moduli |

Solo su Claude Code, e solo se c'è materiale vero per riempirli, il `07` si divide in `07-architecture.md`, `08-database.md` e `09-api.md`. Non creare mai file vuoti o riempiti di ipotesi, come deployment o troubleshooting all'avvio: l'agente li prende per veri. Il troubleshooting nasce quando compare il primo problema.

I template di ogni file sono in `assets/template/`. Leggili prima di scrivere: ogni template spiega cosa va in ogni sezione e da dove prenderlo.

## Flusso

### 1. Leggi l'idea

L'utente ti dà un'idea con alcuni dettagli, a volte due righe, a volte un documento. Prima di fare qualsiasi domanda, estrai tutto quello che c'è già su queste voci:

strumento, database, AI dentro l'app e modello, utenti, problema, funzioni principali, cosa resta fuori dall'MVP, quando è finito, metriche di successo, riferimenti visivi, lingua e registro dell'app.

Quello che l'utente ha già detto non lo chiedi più, neanche per conferma. Se ha detto una parte di una cosa, chiedi solo la parte che manca: se scrive "con Supabase" senza lo strumento, chiedi lo strumento e salti il database.

### 2. Fai solo le domande che servono, una per messaggio

Le domande sono sempre specifiche. Non chiedere mai "servono dati salvati?" o "hai preferenze sul design?": dai l'elenco delle opzioni concrete e l'utente sceglie o scrive la sua. Ogni elenco chiude con "Altro, scrivi quale". Se hai a disposizione lo strumento a bottoni (per esempio `ask_user_input_v0` su Claude.ai o l'equivalente in Claude Code), usalo per le domande a opzioni; altrimenti usa una lista numerata.

Ordine delle domande, da saltare quando la risposta c'è già:

**Strumento.** "Con quale strumento costruisci?" 1. Lovable 2. Replit 3. Claude Code 4. Altro, scrivi quale.

**Database**, con le opzioni valide per lo strumento scelto:
- Lovable: 1. Lovable Cloud, il database interno 2. Supabase con un account tuo 3. Nessun database, i dati restano nel browser dell'utente 4. Altro, scrivi quale
- Replit: 1. Il PostgreSQL interno di Replit 2. Supabase 3. Nessun database, i dati restano nel browser dell'utente 4. Altro, scrivi quale
- Claude Code: 1. Supabase 2. Nessun database, i dati restano nel browser dell'utente 3. Altro, scrivi quale, per esempio SQLite o Neon
- Altro strumento: 1. Supabase 2. Il database interno dello strumento, se ne ha uno 3. Nessun database 4. Altro, scrivi quale

**AI dentro l'app**, solo se l'idea non lo chiarisce: 1. Nessuna AI dentro l'app 2. Gateway AI di Lovable (solo se lo strumento è Lovable) 3. Claude con chiave Anthropic 4. OpenAI 5. Altro, scrivi quale. Con "nessuna" non produci il `04`.

**Stack**, solo su Replit, Claude Code o altro strumento, dove non è imposto. Non chiederlo in astratto: proponi uno stack motivato in una riga preso dal file di riferimento dello strumento e dai come opzioni 1. Va bene 2. Preferisco un altro stack, scrivi quale.

**Le domande che solo l'utente può rispondere**, una per messaggio, solo quelle che mancano: il problema, per chi, cosa resta fuori dall'MVP, quando è finito, le metriche di successo. Queste sono aperte, ma restano specifiche perché partono dall'idea. Per un'app di autovalutazione delle competenze, male: "Qual è il problema che risolvi?"; bene: "Oggi il tuo utente fa l'autovalutazione e poi? Cosa succede dopo che ha visto i voti, e perché non gli basta?". Per il fuori scope e le metriche puoi proporre due o tre candidati ricavati dall'idea come opzioni, sempre con "Altro".

**Design**, in un unico messaggio: chiedi riferimenti concreti (un sito, i colori del brand, un logo, un design system già pronto) e nello stesso messaggio proponi tre direzioni visive ricavate dall'idea, cioè da chi userà l'app e in che contesto. Ogni direzione sta in una riga con palette, coppia di font e tono. Se l'utente dà sia un riferimento sia una direzione, il riferimento vince sui punti in cui è preciso e la direzione copre il resto.

Non chiedere altro. Tutto il resto lo scrivi tu in bozza al passo 3.

### 3. Scrivi i file in bozza

Leggi `references/<strumento>.md` (lovable, replit, claude-code, altro) e i template in `assets/template/`, poi scrivi i file.

Cosa viene da dove:
- dalle risposte dell'utente e dall'idea: problema, per chi, scope, fuori scope, fatto quando, metriche, riferimenti visivi, scelte di strumento, database e modello AI;
- ricavato da te: principi, token e componenti del design system, architettura, modello dati, schema DB, task, sequenza di prompt, contesto di dominio del `04`;
- fisso: le regole di voce e la struttura delle regole permanenti.

Per il contesto di dominio del `04` scrivi una prima versione partendo dall'idea. Il rischio di questa bozza è che si riempia di frasi plausibili che valgono per qualsiasi app dello stesso tipo, cioè quello che il contesto di dominio serve a evitare. Per questo segna ogni frase che ricavi dal tuo sapere generale e non da quello che ha scritto l'utente con `[da verificare]` in coda. L'utente così sa dove guardare. L'esempio di contesto ben fatto è in `references/esempio-contesto-ai.md`.

La stessa marcatura vale in tutti gli altri file per i contenuti che l'utente ha nominato senza scriverli. Se l'idea dice "tre domande guida" e non le elenca, le scrivi tu in bozza, ognuna con `[da verificare]`, invece di lasciare un rimando a qualcosa che non esiste.

I prompt del `03` seguono la regola: un prompt corrisponde a un blocco che l'utente può verificare nell'anteprima in pochi minuti. L'ordine è piano, interfaccia con dati finti, persistenza, AI a runtime, funzioni secondarie una per prompt. Ogni prompt dice cosa costruire, cosa non toccare, cosa non creare ancora, e chiude con le verifiche da fare prima del prompt successivo. I prompt si fermano all'MVP; le evoluzioni restano nel master plan.

### 4. Controllo incrociato prima di consegnare

I file vengono scritti in momenti diversi e si contraddicono facilmente. Prima di consegnare verifica, e correggi dove non torna:

- il modello dati è identico nel `07`, nel contratto delle funzioni server e nel formato di output del `04`: stessi nomi di chiave, stessi tipi (per esempio non un oggetto `{text}` da una parte e una stringa dall'altra);
- ogni voce dello scope MVP del `01` ha almeno un task nel `06` e compare in almeno un prompt del `03`;
- ogni stato descritto nel `02` (vuoto, caricamento, errore, storage assente) ha un task;
- ogni scelta fatta in qualsiasi file (strumento, database, modello AI, stack, libreria per grafici, niente login) ha una voce nel `05`;
- ogni elemento citato da un file esiste davvero da qualche parte: se il prompt dice "le tre domande del master plan", il master plan le contiene;
- nessun file contiene il trattino lungo o le parole bandite.

### 5. Consegna

Scrivi i file in una cartella con il nome del progetto. Su Claude.ai la cartella è `/mnt/user-data/outputs/<nome-progetto>/` e la presenti con `present_files`; in Claude Code scrivi in `docs/` nella radice del repository e il `CLAUDE.md` nella radice. Nel messaggio di consegna scrivi in due o tre frasi da quale file partire e quali parti sono segnate `[da verificare]`. Niente riassunto dei file: l'indice di posa nel `03` fa già quel lavoro.

## Regole di voce, fisse

Valgono in due posti: nei file che scrivi e nei messaggi all'utente, e dentro il progetto, perché le copi nelle regole permanenti (`00`) e nei vincoli di output del `04`, così finiscono nei testi dell'app e nelle risposte dell'AI a runtime.

- Italiano, registro tu, asciutto. Periodi distesi collegati da virgole, due punti e punto e virgola, non una fila di frasi brevissime staccate.
- Forma attiva. Titoli in sentence case, verbi al presente.
- Mai il trattino lungo. Niente emoji, niente hashtag, niente asterischi decorativi.
- Parole bandite: sfida, leva, panorama, ecosistema, robusto, cruciale, fondamentale.
- Niente costruzioni "non solo X, ma anche Y", niente triadi automatiche, niente superlativi e aggettivi superflui, niente metafore e frasi fatte.
- Non aprire le frasi con "E".
- Le label dell'interfaccia dicono cosa succede: "Salva valutazione di oggi", non "Salva". Gli errori spiegano il motivo e cosa fare, senza scuse.

Se l'app è in un'altra lingua, le regole di registro e di stile valgono lo stesso e l'elenco delle parole bandite si traduce con gli equivalenti più vicini.

## File di riferimento

- `references/lovable.md`: dove va ogni file in Lovable, Lovable Cloud contro Supabase esterno, gateway AI, come scrivere i prompt.
- `references/replit.md`: `replit.md`, database interno, Secrets, stack da proporre, prompt per l'Agent.
- `references/claude-code.md`: `CLAUDE.md` con import dei file in `docs/`, plan mode, stack da proporre, task con verifica e commit.
- `references/altro.md`: come trattare uno strumento non coperto.
- `references/esempio-contesto-ai.md`: un `04` ben fatto, da usare come calibrazione e non da copiare.
- `assets/template/`: la struttura di ognuno degli otto file.
