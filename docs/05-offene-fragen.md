# 05 — Offene Fragen und getroffene Annahmen

Das Fachkonzept ist vollständig durchgeplant. An den folgenden Stellen habe ich eine
Annahme getroffen, weil sie sich fachlich begründen lässt — sie sollte aber bestätigt oder
korrigiert werden, bevor wir über die Umsetzung sprechen.

---

## A — Annahmen, die ich getroffen habe

| # | Annahme | Begründung | Auswirkung bei Korrektur |
|---|---|---|---|
| A1 | **Die Schulleitung entscheidet allein und standortübergreifend.** Keine zweite Genehmigungsstufe. | Eine Person kann nur einmal abwesend sein; zwei getrennte Entscheidungen wären widersprüchlich. | Mehrstufiger Workflow — spürbar aufwändiger, betrifft Statusmodell und Benachrichtigungen |
| A2 | **Die Vertretungsplanung sieht den Antragsgrund nicht.** | Zweckbindung; für die Planung ist die Ursache ohne Belang. | Wenn der Grund doch gebraucht wird, muss das begründet und in der Dienstvereinbarung geregelt werden |
| A3 | **Krankmeldungen laufen weiter außerhalb des Systems.** | Gesundheitsdaten nach Art. 9 DSGVO; würde den Schutzbedarf und den Prüfaufwand erheblich erhöhen. | Deutlich strengere Anforderungen; DSFA dann sehr wahrscheinlich verpflichtend |
| A4 | **Benachrichtigungen gehen an Rollenpostfächer**, nicht an Einzelpersonen. | Urlaub und Personalwechsel unterbrechen den Prozess sonst. | Vertretungsregelungen müssen personenbezogen gepflegt werden |
| A5 | **Keine Teilgenehmigung** — abweichende Wünsche laufen über eine Rückfrage. | Antrag und Genehmigung bleiben deckungsgleich. | Zusätzlicher Status und Änderungslogik nötig |
| A6 | **Keine automatische Genehmigung durch Zeitablauf.** | Eine Genehmigung ist eine Entscheidung, kein Ausbleiben einer Entscheidung. | — |
| A7 | **Beteiligte sind ausschließlich Beschäftigte der Schule.** Keine Zugänge für Eltern oder Schülerinnen und Schüler. | Hält den Nutzerkreis und damit den Schutzbedarf klein. | Externer Zugang wäre ein eigenes Projekt |

---

## B — Fragen, die ich nicht selbst beantworten kann

### Organisation

1. **Wer entscheidet tatsächlich?** Nur die Schulleitung, oder sind stellvertretende
   Schulleitung / Abteilungsleitungen regulär beteiligt — und wenn ja: entscheidend
   oder vorprüfend?
2. **Gibt es je Standort eine eigene Leitung** mit eigener Entscheidungsbefugnis?
3. **Wer ist „Sekretariat" im Sinne des Workflows** — ein Sekretariat für beide Standorte
   oder zwei getrennte? Bei welchen Antragsarten wird es überhaupt gebraucht?
4. **Wer macht die Vertretungsplanung** — eine Person für beide Standorte oder je Standort
   eine? (Bestimmt, ob die Standorttrennung bei den Empfängern real wirkt.)
5. **Welche Antragsarten fehlen?** Meine Liste: Dienstbefreiung, Dienstreise/Fortbildung,
   Unterrichtsgang, mehrtägige Fahrt. Gibt es weitere eigenständige Anträge
   (Raumnutzung, Schlüssel, Mehrarbeit, Arbeitszeitkonto, Wettbewerbe)?
6. **Welche Fristen gelten an Ihrer Schule?** Meine Werte (5 Werktage / 10 Werktage /
   6 Wochen) sind Erfahrungswerte, keine Vorgabe.
7. **Wie viele Anträge fallen pro Schuljahr ungefähr an?** Das beeinflusst die
   Technologiewahl deutlich — 200 Anträge im Jahr rechtfertigen eine andere Lösung als 3.000.
8. **Gibt es einen Genehmigungsvorbehalt des Staatlichen Schulamts** bei bestimmten
   Anträgen (z. B. Fahrten ins Ausland)? Dann bräuchte der Workflow einen externen Schritt.

### Technik und Umfeld

9. **Welches Anmeldeverfahren steht zur Verfügung?** Schulportal Hessen, Microsoft 365,
   IServ, eigener Verzeichnisdienst — oder nichts Zentrales? Das ist die wichtigste
   technische Vorfrage.
10. **Welches Vertretungsplanwerkzeug ist im Einsatz** (Untis/WebUntis, DAVINCI, anderes)
    und gibt es dort eine Importmöglichkeit?
11. **Welche Hosting-Optionen bestehen?** Angebot des Schulträgers, Landesangebot,
    eigener Server, bestehende Verträge mit Schuldienstleistern?
12. **Wer betreibt und pflegt das System langfristig** — und wer vertritt diese Person?
13. **Gibt es bereits eine eingeführte Plattform** mit Formular- und Workflow-Funktionen,
    auf der aufgesetzt werden könnte?

### Recht und Beteiligung

14. **Ist der Personalrat schon informiert?** Empfehlung: jetzt einbinden, mit diesen
    Dokumenten als Grundlage.
15. **Wer ist die/der zuständige Datenschutzbeauftragte** und wurde bereits Kontakt
    aufgenommen?
16. **Gibt es bereits eine Dienstvereinbarung** zu digitalen Werkzeugen, an die angeknüpft
    werden kann?

---

## C — Nächste Schritte

1. Die Fragen unter B klären — besonders **1, 4, 9 und 11**, weil sie das Konzept und die
   Technologiewahl direkt verändern.
2. Konzept mit Schulleitung, Personalrat und Datenschutzbeauftragten abstimmen.
3. Erst danach: Umsetzungsvarianten anhand von [04-anforderungskatalog.md](04-anforderungskatalog.md)
   bewerten und entscheiden.
