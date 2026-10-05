# KI-Brücke

Die **KI-Brücke** ist ein kleines, öffentliches Projekt für die Zusammenarbeit zwischen unterschiedlichen KI-Umgebungen.

## Ziel

Die Brücke soll **Linear** als gemeinsamen Arbeits- und Übergabepunkt nutzbar machen, auch wenn ChatGPT, Claude und Claude Code auf unterschiedlichen Konten laufen.

Die Konten müssen nicht zusammengeführt werden.

## Technisches Prinzip

```
ChatGPT / Claude
      ↓ Auftrag
Claude Code
      ↓ Code + Tests
GitHub: KI-Brücke
      ↓
Linear-Adapter
      ↓
Linear
```

- **GitHub** enthält den gemeinsamen Code-Stand.
- **Claude Code** kann den Code entwickeln und nach GitHub pushen.
- **Linear** wird separat authentifiziert.
- Google-, ChatGPT- und Claude-Logins sind keine feste technische Abhängigkeit der Brücke.

## Repository

- Repository: `kuhnkay45-ctrl/KI-Br-cke`
- Branch: `main`
- Sichtbarkeit: öffentlich

## Für Claude Code

Lies zuerst:

1. `CLAUDE.md`
2. `BRIDGE_SPEC.md`
3. den vorhandenen Code

Danach den jeweils aktuellen Auftrag umsetzen.

## Sicherheit

Dieses Repository ist öffentlich.

**Niemals committen:**

- API-Keys
- OAuth-Secrets
- Access-/Refresh-Tokens
- GitHub-Tokens
- Claude-/Anthropic-Keys
- Google-Zugangsdaten
- private personenbezogene Daten

Lokale Secrets gehören in Umgebungsvariablen bzw. lokale Konfigurationsdateien, die durch `.gitignore` ausgeschlossen sind.

## Abgrenzung

Dieses Repository enthält ausschließlich die **KI-Brücke**.

Andere Fachprojekte gehören nicht in den Kern dieses Repositories.
