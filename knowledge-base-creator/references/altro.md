# Altro strumento

Quando l'utente sceglie uno strumento non coperto (Bolt, Cursor, v0, Windsurf, Base44 o altro), le cose da scoprire sono tre, e non le devi inventare.

1. Dove lo strumento tiene il contesto permanente: un campo di istruzioni di progetto, un file di regole nel repository, niente. Se non lo sai con certezza, cercalo nella documentazione ufficiale con la ricerca web. Se non trovi una risposta affidabile, chiedilo all'utente con opzioni: 1. Un campo istruzioni o knowledge nelle impostazioni 2. Un file di regole nel progetto 3. Non lo so, scrivi il `03` in modo che io incolli il contesto nel primo prompt.
2. Se ha un database interno e quale.
3. Se ha una modalità piano e un modo di tornare a una versione precedente.

Con queste tre risposte scrivi il `03` come per gli altri strumenti. Se lo strumento non ha un contesto permanente, il prompt 0 contiene per intero le regole permanenti e il master plan condensato, e ogni prompt successivo si apre con "rileggi le regole del primo messaggio".

Lo stack segue lo strumento: se lo impone, lo registri nel `05` come vincolo; se è libero, proponi come per Claude Code.
