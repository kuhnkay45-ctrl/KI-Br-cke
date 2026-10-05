# Claude Code – Projektanweisung

## Projekt
**KI-Brücke**

Repository: `kuhnkay45-ctrl/KI-Br-cke`  
Branch: `main`

## Ziel
Baue ausschließlich die kleine **KI-Brücke zu Linear**.

Die Brücke soll kontounabhängig funktionieren:
- Claude Code darf mit einem anderen Claude-Konto laufen als das Konto, das Linear benutzt.
- Google-/ChatGPT-Konten dürfen keine technische Voraussetzung der Brücke sein.
- Linear-Zugangsdaten werden ausschließlich über Konfiguration/Umgebungsvariablen eingebunden.
- GitHub ist der gemeinsame Code- und Übergabestand.

## Vor jeder Änderung
1. Lies `README.md`.
2. Lies `BRIDGE_SPEC.md`.
3. Prüfe den vorhandenen Code.
4. Falls Os/Claude einen aktuellen Programmstand oder konkreten Bauauftrag liefert, ist dieser für die Implementierung maßgeblich.
5. Baue keine zweite Parallelarchitektur.

## Grenzen
- Keine Inhalte aus BayBob, E-Mail Bob, Privat-Hub oder anderen Projekten übernehmen.
- Keine Secrets, API-Keys, Tokens, Cookies oder Passwörter committen.
- Keine unnötige Plattform oder Großarchitektur bauen.
- Keine erfundenen Anforderungen als beschlossen behandeln.
- Bestehende sinnvolle Dateien nicht unnötig löschen.

## Implementierungsprinzip
Die Linear-Anbindung muss hinter einer kleinen Adapter-Schicht liegen. Der Rest des Programms darf nicht von einem Google-, ChatGPT- oder Claude-Login abhängen.

Für einen ersten persönlichen Prototyp darf ein Linear Personal API Key über eine Umgebungsvariable verwendet werden. Wenn der aktuelle Auftrag OAuth verlangt, OAuth sauber implementieren.

## Git
- Änderungen nachvollziehbar committen.
- Standardziel ist `main`, solange kein anderer Auftrag vorliegt.
- Vor Push prüfen, dass keine Secrets im Diff liegen.
- Nach erfolgreicher Arbeit pushen.

## Priorität
**klein → funktionsfähig → Linear-Verbindung → testen → committen → pushen**
