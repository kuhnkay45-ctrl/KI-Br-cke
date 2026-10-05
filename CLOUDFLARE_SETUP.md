# Cloudflare Setup – KI-Brücke

## Ziel

Die KI-Brücke läuft als **Cloudflare Worker**.

Cloudflare speichert zwei Secrets:

- `BRIDGE_TOKEN` – der eine wiederverwendbare Schlüssel für vertrauenswürdige KIs
- `LINEAR_API_KEY` – der echte Linear Personal API Key, nur serverseitig

## Wichtig

Der `BRIDGE_TOKEN` darf von mehreren vertrauenswürdigen KI-Umgebungen verwendet werden.

Er gibt nur Zugriff auf die vom Worker fest erlaubten Routen.

Der Worker darf ausschließlich **lesen und neue Objekte anlegen/anhängen**. Keine Update-, Delete-, Archive- oder Überschreibfunktionen.

## Deployment

Cloudflare Workers kann direkt mit dem öffentlichen GitHub-Repository verbunden werden:

`kuhnkay45-ctrl/KI-Br-cke`

Produktionsbranch:

`main`

In Cloudflare:

1. Workers & Pages öffnen.
2. **Create application**.
3. **Import a repository**.
4. GitHub verbinden.
5. `kuhnkay45-ctrl/KI-Br-cke` wählen.
6. Deploy-Befehl: `npx wrangler deploy`.
7. Produktionsbranch: `main`.
8. Speichern und deployen.

Danach unter Worker → Settings → Variables and Secrets zwei Secrets anlegen:

- `BRIDGE_TOKEN`
- `LINEAR_API_KEY`

Alternativ per Wrangler:

```bash
npx wrangler secret put BRIDGE_TOKEN
npx wrangler secret put LINEAR_API_KEY
```

## Lokale Entwicklung

Lokale Secrets gehören in:

`.dev.vars`

Beispiel:

```text
BRIDGE_TOKEN=...
LINEAR_API_KEY=...
```

Diese Datei darf niemals committed werden.

## Aufruf durch eine KI

Die KI erhält:

- die öffentliche Worker-URL
- den `BRIDGE_TOKEN`

Sie erhält **nicht** den `LINEAR_API_KEY`.

Authentifizierung:

```http
Authorization: Bearer <BRIDGE_TOKEN>
```

## Rechtegarantie

Die Sicherheit darf nicht davon abhängen, dass eine KI sich an eine Textanweisung hält.

Der Worker selbst darf nur fest definierte Read- und Create-Endpunkte besitzen.

Keine generische Weiterleitung beliebiger GraphQL-Mutationen an Linear.
