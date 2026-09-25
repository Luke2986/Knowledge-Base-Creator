# Design system: ruota delle competenze PM

Strumento di riflessione, non dashboard. Calmo e disciplinato, con un solo punto di calore: la forma ambrata che si accende sulla ruota scura quando i punteggi salgono. Tutto il resto sta zitto intorno.

## Gerarchia visiva
1. Ruota radar
2. Le tre aree forti
3. Mosse generate
4. Storico

## Token

```css
:root{
  /* sfondo e superfici */
  --ink:#16243f;        /* testo forte, bottoni primari */
  --ink-soft:#46506a;   /* testo secondario */
  --paper:#f7f6f3;      /* sfondo pagina */
  --card:#ffffff;       /* card */

  /* pannello scuro della ruota */
  --panel:#15233f;
  --panel-soft:#22324f; /* gradiente radiale del pannello */
  --on-panel:#dfe5ef;
  --on-panel-soft:#9fb0c8;
  --grid:#34405d;       /* griglia del radar */

  /* accento primario: forza, riempimento ruota, azione AI */
  --amber:#e0a04a;
  --amber-strong:#cf852b;

  /* accento secondario: overlay del confronto */
  --teal:#7aa6a9;

  /* linee e stati */
  --line:#e6e3dc;
  --line-2:#d0ccc2;
  --error:#b23b3b;

  /* raggi */
  --r-card:14px;
  --r-control:10px;
  --r-pill:99px;

  /* tipografia */
  --font-display:'Fraunces', Georgia, serif;
  --font-body:'Inter', system-ui, sans-serif;
  --font-mono:'Space Mono', ui-monospace, monospace;
}
```

Mapping su Tailwind: usa questi valori nel tema, non i grigi di default. Sfondo pagina `--paper`, mai bianco pieno. La ruota è l'unica superficie scura.

## Colori e ruoli
Le card sono bianche su carta. La ruota vive su un pannello blu notte con gradiente radiale da `--panel-soft` in alto a `--panel`. L'ambra compare solo in tre punti: il riempimento dell'area attuale sulla ruota, il valore accanto agli slider, il bottone che genera le mosse. Il teal serve solo all'overlay della valutazione precedente, tratteggiato e tenue. Contrasto AA verificato: `--ink` su `--paper` e `--card`, `--on-panel` sul pannello.

## Tipografia
Fraunces peso 500, sentence case, su H1 e titoli di sezione, con misura. Inter 400 e 600 per il testo. Space Mono per numeri, punteggi, eyebrow ed etichette dati.

Scala: H1 da 40 a 48px, H2 24px, body 15px, descrizioni 13px, eyebrow 11px maiuscolo con letter-spacing .18em in `--amber-strong`, micro 12px. Body mai sotto 15px. Font da Google Fonts: Fraunces opsz 9..144 pesi 400/500/600, Inter 400/500/600, Space Mono 400/700, con font-display swap.

## Spaziatura, layout e breakpoint
Larghezza massima 1152px, centrata. Sotto 640px: padding laterale 20px, una colonna, ruota sopra gli slider. Da 640px: padding 32px. Da 1024px: due colonne, ruota a sinistra e slider a destra. Sezioni come card separate da 24px verticali, padding interno da 20 a 24px, slider distanti 20px l'uno dall'altro.

## Componenti
Slider: track 4px `--line-2`; thumb tondo 20px `--amber` con bordo bianco 2px e ombra morbida, scala a 1.12 in hover; focus con outline 2px `--amber-strong` e offset. Label associata via id, valore in mono `--amber-strong` a destra, descrizione dell'area sotto in 13px `--ink-soft`.

Radar: griglia `--grid`. Area attuale con traccia `--amber` spessore 2 e riempimento opacità .34. Overlay precedente con traccia `--teal` 1.5 tratteggiata, riempimento opacità .12, senza animazione. Ai vertici il nome breve e sotto il punteggio in mono ambra. Nomi brevi: Empatia, Dati & AI, Strategia, Leadership, Storytelling, Collaborazione, Sperimentazione, Consapevolezza. Sopra il grafico, eyebrow FORMA ATTUALE a sinistra e media a destra.

Card: sfondo `--card`, bordo 1px `--line`, raggio `--r-card`. Card delle aree forti su `#fbf9f4`.

Bottoni: primario `--ink` con testo bianco; azione AI `--amber-strong` con testo bianco; neutro bianco con bordo `--line-2`. Raggio `--r-control`, padding 9px 15px, focus con outline 2px `--amber-strong`, disabilitato a opacità .55.

Textarea: bordo `--line-2`, sfondo `#fffdf9`, padding da 10 a 12px, ridimensionabile in verticale, focus ambra. Placeholder che invita all'azione.

Chip punteggio: sfondo `#fff7ea`, testo `--amber-strong`, bordo `#f0dcb6`, pill, mono 12px, mostra il voto su dieci.

Mossa generata: riga su bianco, bordo `--line`, raggio 8px, padding da 8 a 10px, testo 13.5px `--ink`, elenco verticale sopra la textarea delle note.

## Stati
Vuoto: senza salvataggi lo storico non compare. Caricamento: il bottone delle mosse è disabilitato con uno spinner di 15px e il testo "Genero"; nelle tre card, al posto delle mosse, due righe skeleton grigio chiaro. Errore AI: riga `--error` sotto il bottone con il motivo e l'invito a riprovare. Storage non disponibile: nota tenue sopra la barra azioni che avverte che i salvataggi restano nella sessione.

## Movimento
Solo micro transizioni: thumb, hover dei bottoni, spinner, pulsazione lenta dello skeleton. Con prefers-reduced-motion tutto fermo.

## Accessibilità
Focus visibile su ogni elemento interattivo. Ogni slider con label e aria-label. Contrasto AA. Navigazione completa da tastiera.

## Voce dell'interfaccia
Rimando alle regole permanenti (00). Label del progetto: "Salva valutazione di oggi", "Esporta il piano", "Genera le mosse con l'AI", "Azzera", "Sovrapponi alla ruota", "Ricarica", "Elimina".
