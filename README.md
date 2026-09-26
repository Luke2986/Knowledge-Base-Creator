# Knowledge Base Creator

Una skill per Claude che trasforma un'idea di software nella knowledge base da dare a un builder AI prima di scrivere una riga di codice. Tu porti l'idea con i dettagli che hai già, la skill ti fa solo le domande che mancano, una per messaggio e con le opzioni già pronte, poi scrive otto file markdown coerenti tra loro e adattati allo strumento con cui costruisci.

Funziona con Lovable, Replit e Claude Code, e gestisce anche strumenti diversi cercando dove tengono il contesto permanente.

## Perché serve

I builder AI costruiscono bene quando hanno un contesto fisso da rileggere e sbagliano quando devono ricostruirlo a ogni prompt: aggiungono funzioni non richieste, creano backend che non servono, cambiano il modello dati a metà strada. Questa skill prepara quel contesto prima di aprire il builder, e divide la costruzione in prompt piccoli da verificare uno alla volta, così l'agente non prova a fare tutto insieme.

## Cosa produce

| File | Quando | Contenuto |
|---|---|---|
| `00-regole-permanenti.md` | sempre | Come l'agente lavora su ogni task: un passo alla volta, sicurezza, struttura del codice, documentazione, voce dei testi |
| `01-master-plan.md` | sempre | Cosa, per chi, problema, principi, scope MVP, fuori scope, fatto quando, metriche, evoluzione |
| `02-design-system.md` | sempre | Gerarchia visiva, token CSS, tipografia, breakpoint, componenti, stati, accessibilità |
| `03-prompt-<strumento>.md` | sempre | Dove incollare ogni file nello strumento e la sequenza di prompt fino all'MVP, ognuno con le sue verifiche |
| `04-contesto-ai-runtime.md` | solo se l'app usa l'AI | Il system della funzione lato server che chiama il modello: ruolo, contesto di dominio, stile, formato di output |
| `05-decision-log.md` | sempre | Le decisioni già prese, con motivo, alternative e quando rivalutarle |
| `06-tasks.md` | sempre | Task raggruppati per prompt, ognuno con la condizione che dice quando è fatto |
| `07-architecture.md` | sempre | Stack, cartelle, modello dati, schema del database, contratti delle funzioni server, flussi |

Su Claude Code, quando c'è materiale sufficiente, l'architettura si divide anche in `08-database.md` e `09-api.md`. La skill non crea mai file vuoti o riempiti di ipotesi.

## Come funziona

1. Legge l'idea ed estrae quello che hai già deciso: strumento, database, AI, utenti, funzioni, riferimenti visivi. Quello che hai detto non te lo chiede più.
2. Ti fa solo le domande che mancano, con opzioni specifiche per il tuo caso. Se scegli Replit, per il database vedi le opzioni di Replit; se scegli Lovable, quelle di Lovable.
3. Ti chiede solo quello che puoi sapere tu, cioè problema, per chi, cosa resta fuori, quando è finito, metriche, e scrive in bozza il resto: architettura, modello dati, task, token del design system.
4. Per il design ti chiede riferimenti concreti e nello stesso messaggio ti propone tre direzioni visive ricavate dall'idea.
5. Segna con `[da verificare]` le frasi che ricava dal sapere generale invece che da quello che hai scritto tu, così sai dove guardare.
6. Prima di consegnare controlla che i file non si contraddicano: stesso modello dati ovunque, un task per ogni voce dello scope, una voce nel decision log per ogni scelta.

## Strumenti e database supportati

| Strumento | Contesto permanente | Database |
|---|---|---|
| Lovable | workspace knowledge e project knowledge | Lovable Cloud, Supabase con account proprio, nessuno |
| Replit | `replit.md` e cartella `docs/` | PostgreSQL interno, Supabase, nessuno |
| Claude Code | `CLAUDE.md` con import da `docs/` | Supabase, SQLite, Neon o altro, nessuno |
| Altro | lo cerca nella documentazione dello strumento o te lo chiede | Supabase, database interno, nessuno |

"Nessuno" significa dati salvati nel browser con localStorage, adatto a un MVP single user senza login.

## Installazione

Su Claude.ai carica il file `knowledge-base-creator.skill` dalla sezione Skills delle impostazioni.

In Claude Code copia la cartella `knowledge-base-creator/` di questo repository in `~/.claude/skills/` per averla in tutti i progetti, oppure in `.claude/skills/` dentro un singolo repository:

```bash
git clone https://github.com/Luke2986/Knowledge-Base-Creator.git
mkdir -p ~/.claude/skills && cp -R Knowledge-Base-Creator/knowledge-base-creator ~/.claude/skills/
```

## Come si usa

Descrivi l'idea con i dettagli che hai, anche pochi. Per esempio:

```text
Voglio costruire su Lovable un'app per l'autovalutazione delle competenze
da Product Manager: otto slider, una ruota radar e l'AI che suggerisce
come usare l'AI sulle tre aree più forti. Niente login, salvo nel browser.
```

```text
Prepara i file per un tool su Replit: l'albergatore incolla una recensione
di Google o Booking e ottiene tre bozze di risposta nel tono della struttura.
```

La skill si attiva anche senza nominarla, con richieste come "voglio costruire questa idea", "prepara i file per Lovable", "impostiamo il progetto" o "fammi il master plan".

## Struttura del repository

```text
Knowledge-Base-Creator/
├─ README.md
├─ knowledge-base-creator.skill      pacchetto da caricare su Claude.ai
├─ knowledge-base-creator/           la skill, da copiare in Claude Code
│  ├─ SKILL.md
│  ├─ references/
│  │  ├─ lovable.md
│  │  ├─ replit.md
│  │  ├─ claude-code.md
│  │  ├─ altro.md
│  │  └─ esempio-contesto-ai.md
│  └─ assets/
│     └─ template/
│        ├─ 00-regole-permanenti.md
│        ├─ 01-master-plan.md
│        ├─ 02-design-system.md
│        ├─ 03-prompt-strumento.md
│        ├─ 04-contesto-ai-runtime.md
│        ├─ 05-decision-log.md
│        ├─ 06-tasks.md
│        └─ 07-architecture.md
└─ esempi/
   └─ ruota-competenze-pm/           i file prodotti dalla skill per un'app su Lovable
```

La cartella `esempi/` mostra cosa consegna la skill: sono gli otto file generati per un'app di autovalutazione delle competenze da Product Manager, costruita su Lovable con salvataggio nel browser e AI a runtime.

## Voce e lingua

La skill scrive in italiano, registro tu, con regole di voce fisse che finiscono anche nei testi dell'app e nelle risposte dell'AI a runtime: niente trattino lungo, niente emoji, niente costruzioni "non solo X, ma anche Y", e un elenco di parole bandite. Se preferisci altre regole, modificale in `knowledge-base-creator/SKILL.md` e in `knowledge-base-creator/assets/template/00-regole-permanenti.md`.

## Limiti

La skill prepara il progetto, non scrive il codice e non serve per rimettere in ordine un'app già in sviluppo avanzato. Le informazioni sugli strumenti riflettono lo stato di Lovable, Replit e Claude Code a settembre 2026: le piattaforme cambiano spesso, quindi i file in `knowledge-base-creator/references/` vanno aggiornati quando cambia il modo in cui gestiscono contesto, database o segreti.

## Autore

Luca Versilia, product manager e digital strategist.
