# Cose Aperte — PWA MVP

PWA offline-first per raccogliere le cose in sospeso e ridurle a un prossimo passo minimo.

## Cosa include

- Home mobile ispirata al mockup.
- Panoramica desktop con sidebar, riepilogo, colonne per area e focus del giorno.
- Dettaglio/modifica di ogni cosa aperta.
- Stati: Aperta, In corso, Bloccata, In attesa, Da decidere, Chiusa, Archiviata.
- Salvataggio locale con `localStorage`.
- Installabilità PWA con `manifest.webmanifest`.
- Offline tramite `sw.js`.
- Nessun framework e nessuna build.

## Come provarla in locale

Apri una cartella terminale dentro `cose-aperte-pwa` e avvia un piccolo server:

```bash
python -m http.server 8080
```

Poi apri:

```text
http://localhost:8080
```

## Come pubblicarla su GitHub Pages

1. Crea un repository GitHub.
2. Carica tutti i file e le cartelle nella root del repository.
3. Vai su Settings → Pages.
4. Source: Deploy from a branch.
5. Branch: `main`, folder `/root`.
6. Apri il link generato da GitHub Pages.

## File principali

- `index.html`: shell HTML.
- `styles.css`: UI responsive e layout.
- `app.js`: logica, stato, CRUD, localStorage.
- `manifest.webmanifest`: configurazione PWA.
- `sw.js`: cache offline.
- `icons/`: icone PWA.

## Limite intenzionale dell'MVP

I dati restano solo sul dispositivo/browser. Non c'è login, cloud sync o backend.
