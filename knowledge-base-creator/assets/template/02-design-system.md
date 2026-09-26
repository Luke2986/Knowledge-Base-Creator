<!-- TEMPLATE. Parti dai riferimenti dell'utente o dalla direzione scelta. Token concreti, mai "colori eleganti": Lovable e gli altri builder applicano meglio valori esatti. -->

# Design system: <nome progetto>

<!-- Una frase sul carattere dell'interfaccia e sull'unico elemento che deve attirare l'attenzione. -->

## Gerarchia visiva
<!-- Elenco numerato degli elementi della schermata principale in ordine di importanza. -->

## Token

```css
:root{
  /* sfondo e superfici */
  /* testo */
  /* accento primario: dove compare e solo lì */
  /* accento secondario, se serve */
  /* linee e stati: errore, successo */
  /* raggi */
  /* tipografia: display, body, mono se servono numeri */
}
```

<!-- Mapping su Tailwind: usa questi valori nel tema, non i grigi di default. -->

## Colori e ruoli
<!-- Per ogni colore: dove compare. Contrasto AA verificato su testo e bottoni. -->

## Tipografia
<!-- Font, pesi, scala in px per H1, H2, body, descrizioni, micro. Body mai sotto 15px. Caricamento con font-display swap. -->

## Spaziatura, layout e breakpoint
<!-- Larghezza massima, padding per breakpoint, colonne per breakpoint con i valori espliciti (per esempio mobile sotto 640px, tablet, desktop da 1024px). -->

## Componenti
<!-- Per ogni componente usato nell'MVP: aspetto, hover, focus, disabilitato. Solo quelli che servono. -->

## Stati
<!-- Vuoto, caricamento (skeleton o spinner, e dove), errore, successo, dati assenti o storage non disponibile. Ogni stato ha un task nel 06. -->

## Movimento
<!-- Solo micro transizioni, e cosa succede con prefers-reduced-motion. -->

## Accessibilità
<!-- Focus visibile, label, contrasto, navigazione da tastiera, responsive. -->

## Voce dell'interfaccia
Rimando alle regole permanenti (00). Qui solo le label specifiche del progetto, già scritte.
