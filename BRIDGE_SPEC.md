# KI-Brücke – technische Grundspezifikation

## Zweck
Die **KI-Brücke** ist ein kleines Programm, das Linear als gemeinsamen Arbeits- und Übergabepunkt nutzbar macht, obwohl die beteiligten KI-Umgebungen auf unterschiedlichen Konten laufen können.

Es geht ausschließlich um die Brücke selbst, nicht um die Inhalte einzelner Fachprojekte.

## Kontenmodell
Es existieren getrennte Arbeitsumgebungen:

- eine Umgebung/Konto für ChatGPT und Linear,
- ein anderes bzw. älteres Claude-Konto, das für Claude Code genutzt werden kann,
- ein GitHub-Konto/Repository als neutraler gemeinsamer Code-Stand.

Diese Konten müssen nicht zusammengeführt werden.

### Entscheidende Regel
Die Brücke darf **nicht an Google-Login, ChatGPT-Login oder Claude-Login gekoppelt sein**.

Claude Code kann den Code entwickeln und nach GitHub pushen, solange seine lokale GitHub-Umgebung Schreibzugriff auf dieses Repository hat.

Linear wird separat authentifiziert.

## Linear-Anbindung
Linear stellt eine GraphQL-API bereit.

Für einen persönlichen kleinen Prototyp ist ein **Personal API Key** der einfachste Zugang. Der Schlüssel darf nur lokal bzw. über Umgebungsvariablen eingebunden werden.

Beispielname:

`LINEAR_API_KEY`

Er darf niemals ins öffentliche Repository geschrieben werden.

Wenn die Brücke später von mehreren Nutzern/Workspaces verwendet werden soll, kann auf OAuth 2.0 umgestellt werden.

## Minimale Architektur
Die Implementierung soll so klein wie möglich bleiben.

Empfohlene Trennung:

```
UI / CLI / Aufrufer
        |
        v
Bridge-Service
        |
        v
Linear-Adapter
        |
        v
Linear API
```

Der Linear-Adapter kapselt:
- Authentifizierung,
- API-Aufrufe,
- Fehlerbehandlung,
- Übersetzung zwischen internen Daten und Linear.

Der Rest des Programms kennt keinen Google-/ChatGPT-/Claude-Login.

## Funktionsumfang
Der konkrete Funktionsumfang kommt aus dem jeweils aktuellen Auftrag von Os/Claude.

Nicht eigenmächtig zusätzliche große Funktionen bauen.

Als technische Basis muss die Brücke aber:
1. Linear-Verbindung prüfen können.
2. verständliche Fehler melden können.
3. Zugangsdaten ausschließlich außerhalb des Repositories beziehen.
4. später um weitere Linear-Lese-/Schreiboperationen erweitert werden können.

## Öffentliche Repository-Regel
Dieses Repository ist absichtlich öffentlich.

Daher niemals committen:
- Linear API Keys,
- OAuth Client Secrets,
- Access-/Refresh-Tokens,
- GitHub-Tokens,
- Claude-/Anthropic-Keys,
- Google-Zugangsdaten,
- private personenbezogene Daten.

## Zusammenarbeit
GitHub ist die Übergabestelle.

Ein sinnvoller Ablauf ist:

```
ChatGPT / Claude
      ↓ Auftrag
Claude Code
      ↓ Code + Tests
GitHub KI-Brücke
      ↓ gemeinsamer Stand
andere KI / Entwickler
```

Linear ist die externe Arbeitsplattform, die über die Brücke angesprochen wird.

## Nicht Teil dieses Projekts
- BayBob
- E-Mail Bob
- Privat-Hub
- andere Bob-Projekte
- deren Datenmodelle oder Fachlogik

Sie dürfen später Nutzer der Brücke sein, gehören aber nicht in den Kern der KI-Brücke.
