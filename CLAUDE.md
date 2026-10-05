# Claude Code – Projektanweisung

## Projekt
**KI-Brücke**

Repository: `kuhnkay45-ctrl/KI-Br-cke`  
Branch: `main`

## Ziel
Baue ausschließlich die kleine **KI-Brücke zu Linear** als Cloudflare Worker.

Die Brücke soll kontounabhängig funktionieren:
- Claude Code darf mit einem anderen Claude-Konto laufen als das Konto, das Linear benutzt.
- Google-/ChatGPT-/Claude-Konten sind keine technische Voraussetzung der Brücke.
- GitHub ist der gemeinsame Code-Stand.
- Cloudflare stellt die öffentliche Bridge-URL bereit.
- Linear wird serverseitig über einen geheimen `LINEAR_API_KEY` angesprochen.

## Ein Schlüssel für alle vertrauenswürdigen KIs

Es gibt genau einen wiederverwendbaren Zugangsschlüssel:

`BRIDGE_TOKEN`

Diesen Token kann Os verschiedenen vertrauenswürdigen KI-Umgebungen geben.

Der echte `LINEAR_API_KEY` darf niemals an diese KIs ausgegeben werden und liegt nur als Cloudflare-Secret vor.

## Unverhandelbare Schreibregel

Die Brücke ist **READ + CREATE/APPEND ONLY**.

Erlaubt:
- vorhandene Daten lesen
- neue Issues anlegen
- neue Kommentare anlegen
- neue Dokumente anlegen
- neue Projekte anlegen, sofern der aktuelle Linear-Kontext dies unterstützt
- weitere neue Objekte nur als ausdrücklich definierte Create-Endpunkte

Verboten:
- bestehende Issues ändern
- bestehende Kommentare ändern
- bestehende Dokumente überschreiben
- bestehende Projekte verändern
- löschen
- archivieren
- unarchivieren
- Status, Titel, Text oder andere bestehende Felder nachträglich verändern

Wichtig: Diese Regel technisch durch eine **feste Allowlist von Endpunkten** erzwingen. Kein beliebiger GraphQL-Proxy und kein Filter, der nur nach Wörtern sucht.

## Vor jeder Änderung
1. Lies `README.md`.
2. Lies `BRIDGE_SPEC.md`.
3. Lies `CLOUDFLARE_SETUP.md`.
4. Lies `IMPLEMENTATION_TASK.md`.
5. Prüfe den vorhandenen Code.
6. Baue keine zweite Parallelarchitektur.

## Grenzen
- Keine Inhalte aus anderen Fachprojekten übernehmen.
- Keine Secrets, API-Keys, Tokens, Cookies oder Passwörter committen.
- Keine unnötige Plattform oder Großarchitektur bauen.
- Keine Update-/Delete-Endpunkte implementieren.
- Bestehende sinnvolle Dateien nicht unnötig löschen.

## Implementierungsprinzip
Cloudflare Worker → kleine API → Linear-Adapter → Linear GraphQL API.

Secrets:
- `BRIDGE_TOKEN`
- `LINEAR_API_KEY`

Beide nur als Cloudflare-Secrets bzw. lokal in einer ignorierten `.dev.vars`.

## Git
- Änderungen nachvollziehbar committen.
- Standardziel ist `main`.
- Vor Push prüfen, dass keine Secrets im Diff liegen.
- Nach erfolgreicher Arbeit pushen.

## Priorität
**klein → sicher → read/create-only → testen → committen → pushen**
