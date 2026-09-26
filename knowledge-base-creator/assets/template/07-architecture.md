<!-- TEMPLATE. Stack e posizione della logica server dipendono da references/<strumento>.md. Le chiavi e i tipi qui sono la fonte di verità per 01, 03, 04 e 06. Su Claude Code, se database e API hanno materiale vero, sposta quelle sezioni in 08-database.md e 09-api.md. -->

# Architettura: <nome progetto>

## Principi
1. Interfaccia separata dalla logica.
2. AI separata dall'interfaccia.
3. Persistenza separata dai componenti.
4. Nessuna dipendenza inutile.
5. Ogni modulo si modifica senza rompere gli altri.

## Stack
<!-- Imposto o scelto, con il rimando alla voce del 05. -->

## Dove sta la logica lato server
<!-- Edge function su Lovable Cloud o Supabase, route del server su Replit o Claude Code, nessuna se l'app non ha backend. Dove vivono i segreti. -->

## Struttura cartelle
```text
<albero>
```

## Modello dati
```ts
// Tipi. Una sola definizione per ogni entità, riusata ovunque.
// Se un campo è una lista di testi, è string[] ovunque: nel tipo, nel contratto, nell'output del 04.
```

## Database
<!-- Solo se c'è: tabelle, colonne, relazioni, policy RLS per tabella. Se i dati stanno nel browser: chiave di localStorage, formato salvato, cosa succede se lo storage non è disponibile. -->

## Contratti delle funzioni lato server
<!-- Per ogni funzione: nome, richiesta, risposta, errori. La risposta della funzione AI è identica al formato di output del 04. -->

## Flussi utente
<!-- Per ogni flusso dell'MVP, i passaggi numerati. -->

## Responsabilità dei moduli
<!-- components: solo rendering. services: server, persistenza, AI, export. hooks: coordinano. -->

## Regole di evoluzione
<!-- Cosa cambia e cosa resta fermo quando arrivano auth, database, multiutenza. -->

## Checklist architettura
- [ ] Componenti piccoli, nessun file oltre 300 righe
- [ ] Nessuna chiave nel client
- [ ] Interfaccia indipendente da persistenza e AI
- [ ] Tipi definiti una volta sola
