# Reflex-PDF-Viewer — adapter agentowy

Ten plik jest adapterem. Kontekst cross-repo i ograniczenia spike'a są w `../CLAUDE.md`.
Pełny kontrakt procesowy (planowanie, commity, review, standardy implementacji) jest w `../Zotero/CLAUDE.md`.

## Co to jest ten repo

Fork `tomoki1207/vscode-pdfviewer` — PDF.js-based VS Code custom editor.
Ewoluuje w Reflex-aware PDF runtime surface na potrzeby spike'a (#184).

Aktualny stan:
- `viewType`: `reflex-zotero.pdfPreview` (niekonfliktowy, zmieniony w #187)
- `publisher`: `OtisRed` (zmieniony w #187)
- brak integracji z Reflex-Zotero (spike dopiero zaczęty)

## Tooling

```bash
npm ci          # instalacja zależności
npm run compile # tsc → out/
npm run watch   # tryb watch
npm run lint    # eslint
```

TypeScript (`^3.7`), target `out/src/extension.js`.

## Czego nie robić

- Nie implementuj logiki Zotero (item identity, metadata, Web API, Local API) w tym repo.
- Nie importuj kodu z `Reflex-Zotero` bezpośrednio — komunikacja wyłącznie przez `postMessage`.
- Nie vendoruj do Reflex-Zotero bez zamknięcia `decision:open` z #184.
- Nie zmieniaj `viewType` bez uzgodnienia — wpłynie na routing PDF w Extension Development Host.

## Punkty integracji (docelowe)

```
Viewer (webview) → postMessage → extension-host (Viewer) → API → Reflex-Zotero
```

Reflex-Zotero eksponuje komendy VS Code (`vscode.commands.executeCommand`) lub event bus — szczegóły do ustalenia w spike.
