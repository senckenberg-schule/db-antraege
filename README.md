# Digitales Antragssystem — Dienstbefreiung & Schulveranstaltungen

Konzeption eines digitalen Workflows für

* **Dienstbefreiungsanträge** von Beschäftigten (Lehrkräfte und weiteres Personal) und
* **Anträge für Unterrichtsgänge, Exkursionen und Schulveranstaltungen**

an einer Schule mit **zwei Standorten**.

## Status

**Phase 1 — Fachkonzept.** Es wird noch keine Technologie festgelegt. Ziel dieser Phase ist
ein vollständiges, prüfbares Bild von Rollen, Workflow, Daten und Schutzbedarf. Erst danach
wird über die technische Umsetzung entschieden.

## Dokumente

| Dokument | Inhalt |
|---|---|
| [docs/01-fachkonzept.md](docs/01-fachkonzept.md) | Rollen, Antragsarten, Standortlogik, Workflow, Statusmodell, Benachrichtigungen |
| [docs/02-datenmodell.md](docs/02-datenmodell.md) | Entitäten, Formularfelder, Sichtbarkeit auf Feldebene |
| [docs/03-datenschutz-sicherheit.md](docs/03-datenschutz-sicherheit.md) | Rechtsgrundlagen, Schutzbedarf, technische und organisatorische Maßnahmen |
| [docs/04-anforderungskatalog.md](docs/04-anforderungskatalog.md) | MUSS/SOLL/KANN-Anforderungen als Entscheidungsgrundlage für die Umsetzung |
| [docs/05-offene-fragen.md](docs/05-offene-fragen.md) | Zu klärende Punkte vor der Umsetzungsentscheidung |

## Leitgedanken

1. **Ein Workflow, mehrere Antragsarten.** Der Genehmigungsablauf ist immer derselbe;
   die Antragsarten unterscheiden sich nur in ihren Formularfeldern und darin, wer
   nachgelagert informiert wird.
2. **Datensparsamkeit ist Teil der Fachlichkeit, nicht nur der Technik.** Wer einen
   Vertretungsplan schreibt, braucht den *Zeitraum* — nicht den *Grund* der Abwesenheit.
   Diese Trennung ist im Konzept verankert, nicht nachträglich aufgesetzt.
3. **Die E-Mail ist Signal, nicht Inhalt.** Benachrichtigungen enthalten keine
   personenbezogenen Details, sondern einen Link ins System.
4. **Der Antrag ist die Akte.** Jede Entscheidung, Rückfrage und Änderung hängt am
   Vorgang und ist nachvollziehbar — ohne dass daraus eine Verhaltenskontrolle wird.
