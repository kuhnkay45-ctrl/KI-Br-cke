# Bauauftrag – KI-Brücke

## Aufgabe

Implementiere die KI-Brücke als kleinen Cloudflare Worker für Linear.

## Muss-Funktionen

### Authentifizierung
Jeder geschützte Request benötigt:

`Authorization: Bearer <BRIDGE_TOKEN>`

Vergleiche serverseitig mit dem Cloudflare-Secret `BRIDGE_TOKEN`.

### Linear
Verwende serverseitig das Secret:

`LINEAR_API_KEY`

gegen:

`https://api.linear.app/graphql`

### Öffentlicher Health-Endpunkt

`GET /health`

liefert nur Statusinformationen und keine Secrets.

### Lesen

Implementiere feste, sichere Lese-Endpunkte, mindestens:

- `GET /v1/teams`
- `GET /v1/projects`
- `GET /v1/issues`
- `GET /v1/documents`

Sinnvolle Query-Parameter für Suche/Filter sind erlaubt.

### Neu anlegen / anhängen

Implementiere feste Create-Endpunkte, mindestens:

- `POST /v1/issues`
- `POST /v1/comments`
- `POST /v1/documents`
- `POST /v1/projects`

Jeder Endpunkt darf ausschließlich die passende Linear-Create-Mutation aufrufen.

## Striktes Verbot

Nicht implementieren:

- PUT
- PATCH
- DELETE
- generischen GraphQL-Proxy
- Update-Mutationen
- Delete-Mutationen
- Archive-/Unarchive-Mutationen
- Funktionen, die vorhandene Texte oder Felder ersetzen

Neue Kommentare an vorhandenen Issues sind ausdrücklich erlaubt, weil dabei ein **neues Objekt** angelegt wird.

## Fehlerbehandlung

- klare HTTP-Statuscodes
- Linear GraphQL `errors` auswerten
- keine Secrets in Fehlermeldungen oder Logs
- ungültige Eingaben validieren

## Sicherheit

- CORS bewusst konfigurieren; nicht als Ersatz für Authentifizierung behandeln
- keine Secrets committen
- `.dev.vars` ignorieren
- Timing-sicheren Tokenvergleich verwenden, soweit in Workers praktikabel
- Request-Größen begrenzen
- keine beliebigen GraphQL-Queries vom Client entgegennehmen

## Tests

Mindestens testen:

1. `/health` funktioniert ohne Token.
2. geschützte Route ohne Token → 401.
3. falscher Token → 401.
4. Lese-Endpunkt mit korrektem Token funktioniert.
5. Create-Endpunkt legt ein neues Objekt an.
6. es existiert kein Update-/Delete-Endpunkt.
7. unbekannte Route → 404.
8. Secrets erscheinen nicht in Responses.

## Cloudflare

Nutze aktuelles Wrangler und eine aktuelle Worker-Konfiguration.

Cloudflare empfiehlt für neue Projekte `wrangler.jsonc`.

Deklariere die erforderlichen Secrets:

- `BRIDGE_TOKEN`
- `LINEAR_API_KEY`

## Abschluss

Wenn Tests erfolgreich sind:

1. Secret-Check durchführen.
2. Commit erstellen.
3. Nach `main` pushen.
4. Kurze Deploy-Anleitung im README/CLOUDFLARE_SETUP aktuell halten.
