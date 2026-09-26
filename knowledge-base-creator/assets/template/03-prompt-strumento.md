<!-- TEMPLATE. Il nome del file diventa 03-prompt-lovable.md, 03-prompt-replit.md, 03-prompt-claude-code.md o 03-prompt-<strumento>.md. Leggi prima references/<strumento>.md. -->

# Prompt per <strumento>

## Indice di posa
<!-- Istruzioni operative, in ordine, su dove va ogni file prima del primo prompt. Esempio Lovable: "1. Impostazioni del workspace, Knowledge: incolla 00. 2. Impostazioni del progetto, Knowledge: incolla la versione condensata di 01, 02 e 07. 3. Il 04 non va nella knowledge: lo incolli nella edge function al prompt 4." Distingui sempre il contesto che guida l'agente che costruisce da quello che guida l'AI dentro l'app. -->

## Come usare questi prompt
Uno alla volta, nell'ordine. Dopo ogni prompt fai le verifiche elencate sotto e passa al successivo solo se tornano tutte. Se una non torna, correggi quel punto prima di andare avanti.

## Prompt 0: il piano
<!-- In modalità piano se lo strumento ce l'ha. Chiede di leggere il contesto e proporre il piano di costruzione per fasi, senza scrivere codice. -->

> <testo del prompt>

Verifica: il piano segue l'ordine di questo file e non aggiunge funzioni fuori dallo scope del master plan.

## Prompt 1: <interfaccia con dati finti>

> <testo del prompt: cosa costruire, con riferimento esplicito al design system; cosa non creare ancora (backend, tabelle, funzioni server, AI)>

Verifica prima di proseguire:
- <verifiche osservabili nell'anteprima, legate ai task del 06>

## Prompt 2: <persistenza>
<!-- Database scelto o localStorage. Se c'è un database con utenti: tabelle, policy RLS, niente accesso dal client senza policy. -->

## Prompt 3: <AI a runtime, se c'è>
<!-- Funzione lato server, chiave come segreto, contenuto del 04 come system per intero, formato di risposta identico al contratto del 07, gestione di caricamento ed errore, risposta non valida del modello. -->

## Prompt 4 e successivi: <funzioni secondarie, una per prompt>

## Se qualcosa si rompe
<!-- Istruzione specifica per lo strumento: ripristino di versione, checkpoint o commit, poi riformulare il prompt più stretto. -->
