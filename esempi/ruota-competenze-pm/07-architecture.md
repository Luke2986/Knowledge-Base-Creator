# Architettura: ruota delle competenze PM

## Principi
1. Interfaccia separata dalla logica.
2. AI separata dall'interfaccia.
3. Persistenza separata dai componenti.
4. Nessuna dipendenza inutile.
5. Ogni modulo si modifica senza rompere gli altri.

## Stack
React, Vite, TypeScript, Tailwind, shadcn/ui, imposti da Lovable. Recharts per il radar. Vedi 05.

## Dove sta la logica lato server
Una sola edge function su Lovable Cloud, `generate-moves`, per la chiamata al modello attraverso il gateway AI di Lovable. Lovable Cloud è attivo solo per funzione e secret, senza tabelle. Tutto il resto gira nel browser.

## Struttura cartelle
```text
src/
├─ pages/
│  └─ Home.tsx
├─ components/
│  ├─ RadarChart/
│  ├─ CompetencySlider/
│  ├─ GuideQuestions/
│  ├─ StrengthCard/
│  ├─ HistoryList/
│  └─ ActionBar/
├─ hooks/
│  └─ useAssessment.ts
├─ services/
│  ├─ ai.ts
│  ├─ export.ts
│  └─ storage.ts
├─ types/
│  └─ assessment.ts
├─ constants/
│  └─ competencies.ts
└─ utils/
   └─ ranking.ts

supabase/functions/
└─ generate-moves/
   └─ index.ts
```

## Modello dati
```ts
// src/types/assessment.ts, unica definizione riusata ovunque

type CompetencyKey =
  | "empatia"
  | "dati"
  | "strategia"
  | "leadership"
  | "storytelling"
  | "collaborazione"
  | "sperimentazione"
  | "consapevolezza";

// Le mosse sono stringhe ovunque: nel tipo, nel contratto e nell'output del 04.
type Moves = Partial<Record<CompetencyKey, string[]>>;

interface Assessment {
  id: string;                               // crypto.randomUUID()
  createdAt: string;                        // ISO 8601
  scores: Record<CompetencyKey, number>;    // interi da 1 a 10
  notes: Record<CompetencyKey, string>;     // massimo 1000 caratteri, una nota per area
  generatedMoves?: Moves;                   // solo le tre aree forti al momento della generazione
  averageScore: number;                     // un decimale
}
```

`src/constants/competencies.ts` contiene le otto aree in ordine, con chiave, nome, nome breve per il radar e descrizione, come nel master plan. L'ordine vale anche come regola di parità.

`src/utils/ranking.ts` restituisce le tre chiavi con il punteggio più alto; a parità vince la chiave che viene prima nell'ordine delle aree.

## Salvataggio nel browser
Chiave localStorage: `ruota-pm:assessments`, valore: array JSON di `Assessment` dal più recente. `storage.ts` espone `list`, `save`, `remove` e `isAvailable`; se `isAvailable` è falso, l'app lavora in memoria e mostra la nota prevista nel design system.

## Contratto della edge function `generate-moves`

Richiesta:
```json
{
  "areas": [
    { "key": "empatia", "score": 9, "notes": "..." },
    { "key": "strategia", "score": 8, "notes": "" },
    { "key": "storytelling", "score": 8, "notes": "..." }
  ]
}
```

Risposta 200, stessa forma dell'output del 04:
```json
{
  "empatia": ["mossa", "mossa"],
  "strategia": ["mossa", "mossa", "mossa"],
  "storytelling": ["mossa", "mossa"]
}
```

Errori: 400 se la richiesta non ha tre aree valide; 502 se il modello restituisce JSON non valido o chiavi diverse da quelle ricevute; 500 per il resto. Ogni errore ha un campo `message` leggibile che il frontend mostra nella riga rossa.

## Flussi utente

Compilazione: 1. l'utente muove gli slider; 2. la ruota e la media si aggiornano; 3. si ricalcola la top 3; 4. l'utente scrive le note.

Generazione AI: 1. clic su Genera le mosse con l'AI; 2. `ai.ts` invia le tre aree alla edge function; 3. caricamento con spinner e skeleton; 4. le mosse compaiono nelle card oppure compare l'errore.

Salvataggio: 1. clic su Salva valutazione di oggi; 2. si crea lo snapshot; 3. `storage.ts` lo scrive; 4. lo storico si aggiorna.

Confronto: 1. clic su Sovrapponi alla ruota in una voce dello storico; 2. il radar aggiunge la serie teal; 3. nuovo clic la toglie.

Export: 1. clic su Esporta il piano; 2. `export.ts` costruisce il markdown dallo stato corrente; 3. il browser scarica il file.

## Responsabilità dei moduli
components: solo rendering, mai fetch, localStorage o logica. services: AI, export, persistenza. hooks: `useAssessment` coordina stato, servizi e interfaccia.

## Regole di evoluzione
Quando arriva l'auth: modulo auth separato, il modello `Assessment` non cambia. Quando arriva il salvataggio in cloud: si sostituisce `storage.ts` con una versione che usa la tabella `assessments` con RLS, l'interfaccia non cambia, il formato dell'export resta compatibile. Quando arriva la multiutenza: si aggiunge `userId` al modello.

## Checklist architettura
- [ ] Componenti piccoli, nessun file oltre 300 righe
- [ ] Nessuna chiave nel client
- [ ] Interfaccia indipendente da persistenza e AI
- [ ] Tipi definiti una volta sola in `src/types/assessment.ts`
