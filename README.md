# KI-Brücke

Die **KI-Brücke** ist ein kleines öffentliches Projekt, das verschiedene KI-Umgebungen mit **Linear** verbindet.

## Prinzip

```
ChatGPT / Codex / Claude / andere KI
               |
               | BRIDGE_TOKEN
               v
        Cloudflare Worker
               |
               | LINEAR_API_KEY
               v
             Linear
```

- GitHub enthält den gemeinsamen Code-Stand.
- Cloudflare hostet die Brücke.
- Linear wird serverseitig angebunden.
- Google-, ChatGPT- und Claude-Konten müssen nicht zusammengeführt werden.

## Ein Schlüssel

Für vertrauenswürdige KI-Umgebungen gibt es einen wiederverwendbaren Schlüssel:

`BRIDGE_TOKEN`

Der echte Linear-Schlüssel bleibt ausschließlich in Cloudflare verborgen.

## Rechte

Die Brücke ist **READ + CREATE/APPEND ONLY**.

Erlaubt:
- lesen
- neue Dinge anlegen
- neue Kommentare bzw. neue Einträge hinzufügen

Nicht erlaubt:
- vorhandene Dinge überschreiben
- vorhandene Dinge ändern
- löschen
- archivieren

Diese Einschränkung wird durch feste API-Endpunkte erzwungen, nicht durch Anweisungen an die KI.

## Repository

- Repository: `kuhnkay45-ctrl/KI-Br-cke`
- Branch: `main`
- Sichtbarkeit: öffentlich

## Für Claude Code

Zuerst lesen:

1. `CLAUDE.md`
2. `BRIDGE_SPEC.md`
3. `CLOUDFLARE_SETUP.md`
4. `IMPLEMENTATION_TASK.md`

Danach implementieren, testen, committen und nach `main` pushen.

## Sicherheit

Niemals Secrets oder private Zugangsdaten committen.
