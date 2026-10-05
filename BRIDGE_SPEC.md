# KI-Brücke – technische Grundspezifikation

## Zweck
Die **KI-Brücke** ist ein kleines öffentliches Programm, das Linear als gemeinsamen Arbeits- und Übergabepunkt für verschiedene KI-Umgebungen nutzbar macht.

Es geht ausschließlich um die Brücke selbst.

## Kontenmodell
ChatGPT, Codex, Claude und Claude Code dürfen auf unterschiedlichen Konten laufen.

Die Brücke darf **nicht** an Google-, ChatGPT- oder Claude-Logins gekoppelt sein.

GitHub enthält den Code. Cloudflare hostet die Brücke. Linear ist das Zielsystem.

## Architektur

```
verschiedene vertrauenswürdige KIs
          |
          | Authorization: Bearer BRIDGE_TOKEN
          v
    Cloudflare Worker
          |
          | LINEAR_API_KEY (nur serverseitig)
          v
      Linear GraphQL API
```

## Ein wiederverwendbarer Brückenschlüssel

Für alle vertrauenswürdigen KI-Umgebungen gibt es genau einen Zugangsschlüssel:

`BRIDGE_TOKEN`

Dieser Token ist der einzige Schlüssel, den Os an andere KI-Umgebungen weitergeben muss.

Der echte Linear-Schlüssel:

`LINEAR_API_KEY`

bleibt ausschließlich als Cloudflare-Secret gespeichert.

Falls der `BRIDGE_TOKEN` irgendwann öffentlich wird oder missbraucht wird, muss er in Cloudflare rotiert werden. Der Linear-Schlüssel muss dafür nicht weitergegeben werden.

## Berechtigungsmodell: READ + CREATE/APPEND ONLY

### Erlaubt
- Daten aus Linear lesen
- neue Issues anlegen
- neue Kommentare anlegen
- neue Dokumente anlegen
- neue Projekte anlegen, wenn Team/Workspace-Kontext eindeutig angegeben ist
- weitere Create-Endpunkte später gezielt ergänzen

### Verboten
- bestehende Objekte aktualisieren
- bestehende Texte oder Felder überschreiben
- bestehende Issues verändern
- bestehende Kommentare verändern
- bestehende Dokumente bearbeiten
- bestehende Projekte bearbeiten
- löschen
- archivieren
- unarchivieren

## Technische Durchsetzung

Kein generischer Linear-GraphQL-Proxy.

Stattdessen besitzt die Bridge nur **fest programmierte, erlaubte Routen**.

Beispiel:

```
GET  /health
GET  /v1/teams
GET  /v1/projects
GET  /v1/issues
GET  /v1/documents

POST /v1/issues
POST /v1/comments
POST /v1/documents
POST /v1/projects
```

Es existieren bewusst **keine**:

```
PUT
PATCH
DELETE
```

Routen.

Auch intern dürfen keine Linear-`update*`, `delete*`, `archive*` oder vergleichbare Mutationen aufgerufen werden.

## Linear-Anbindung

Linear nutzt:

`https://api.linear.app/graphql`

Für diese persönliche Brücke reicht zunächst ein Linear Personal API Key.

Dieser wird nur über das Cloudflare-Secret `LINEAR_API_KEY` eingebunden und niemals committed.

## Cloudflare

Die Brücke wird als Cloudflare Worker bereitgestellt.

GitHub-Repository:

`kuhnkay45-ctrl/KI-Br-cke`

Branch:

`main`

Cloudflare soll nach Möglichkeit über Workers Builds direkt mit dem GitHub-Repository verbunden werden, sodass Pushes auf `main` automatisch deployt werden.

## Sicherheit

Dieses Repository ist öffentlich.

Niemals committen:
- `BRIDGE_TOKEN`
- `LINEAR_API_KEY`
- OAuth-Secrets
- Access-/Refresh-Tokens
- GitHub-Tokens
- Claude-/Anthropic-Keys
- Google-Zugangsdaten
- private personenbezogene Rohdaten

## Nicht Teil dieses Projekts

Keine Fachlogik anderer Projekte in die KI-Brücke übernehmen.

Die Brücke ist nur die neutrale Verbindung zu Linear.
