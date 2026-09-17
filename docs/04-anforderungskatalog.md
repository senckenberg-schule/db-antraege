# 04 — Anforderungskatalog

Dieser Katalog ist die **Entscheidungsgrundlage für die Technologiewahl**. Jede
Umsetzungsvariante — Eigenentwicklung, Standardsoftware, Baukasten auf vorhandener
Schulplattform — wird später an genau dieser Liste gemessen.

Priorisierung: **MUSS** (ohne das ist das System nutzlos oder unzulässig) ·
**SOLL** (deutlicher Mehrwert, verzichtbar in Stufe 1) · **KANN** (später).

---

## F — Funktionale Anforderungen

| ID | Anforderung | Prio |
|---|---|---|
| F-01 | Anmeldung mit dem dienstlichen Konto (SSO) | MUSS |
| F-02 | Antragsformular je Antragsart mit Pflichtfeldprüfung | MUSS |
| F-03 | Auswahl der betroffenen Standorte (einer oder beide) durch die antragstellende Person | MUSS |
| F-04 | Entscheidung durch die Schulleitung: genehmigen / ablehnen / Rückfrage, **jeweils mit Kommentar** | MUSS |
| F-05 | Kommentarverlauf am Vorgang, nicht editierbar nach dem Absenden | MUSS |
| F-06 | Automatische Benachrichtigung gemäß Benachrichtigungsmatrix, standortabhängig | MUSS |
| F-07 | Statusübersicht für die antragstellende Person („Wo steht mein Antrag?") | MUSS |
| F-08 | Arbeitsvorrat für die Schulleitung, sortiert nach Beginn des beantragten Zeitraums | MUSS |
| F-09 | **Reduzierte Sicht für Vertretungsplanung und Sekretariat (Feldebene)** | MUSS |
| F-10 | Vertretung der Schulleitung mit identischen Rechten | MUSS |
| F-11 | Zurückziehen vor der Entscheidung | MUSS |
| F-12 | **Stornieren nach der Genehmigung inkl. Benachrichtigung aller zuvor Informierten** | MUSS |
| F-13 | Fristprüfung mit Hinweis und Begründungspflicht bei Unterschreitung (keine Blockade) | SOLL |
| F-14 | Begleitpersonen benennen und deren Zustimmung einholen (Art. C/D) | SOLL |
| F-15 | Erinnerung an die Schulleitung bei überfälligen Anträgen | SOLL |
| F-16 | Änderungsantrag zu einem genehmigten Vorgang | SOLL |
| F-17 | Anlagen hochladen (Einladung, Elterninfo, Fahrtenkonzept) | SOLL |
| F-18 | Serientermine in einem Antrag | SOLL |
| F-19 | Export der genehmigten Abwesenheiten für die Vertretungsplanung (Datei) | SOLL |
| F-20 | Konflikthinweis bei Überschneidungen (Lerngruppe/Person/Zeitraum) | SOLL |
| F-21 | Aggregierte Kennzahlen ohne Personenbezug | SOLL |
| F-22 | Tageszusammenfassung statt Einzelmails für STP/SEK | KANN |
| F-23 | Automatische Übergabe an das Vertretungsplanwerkzeug (Schnittstelle) | KANN |
| F-24 | Kalenderexport (ICS) für Schulveranstaltungen | KANN |
| F-25 | Neue Antragsart ohne Programmierung konfigurierbar | KANN |
| F-26 | Vorprüfung/Empfehlung durch Abteilungsleitung vor der Entscheidung | KANN |
| F-27 | Druck-/PDF-Ansicht eines Vorgangs für die Ablage | KANN |

## D — Datenschutz und Sicherheit

| ID | Anforderung | Prio |
|---|---|---|
| D-01 | Verarbeitung ausschließlich in der EU, AV-Vertrag vorhanden | MUSS |
| D-02 | Serverseitige Berechtigungsprüfung **auf Feldebene** | MUSS |
| D-03 | Keine personenbezogenen Inhalte in Benachrichtigungs-E-Mails | MUSS |
| D-04 | Transportverschlüsselung durchgängig; Verschlüsselung der Datenträger und Backups | MUSS |
| D-05 | Automatischer Löschlauf nach konfigurierten Fristen | MUSS |
| D-06 | Protokollierung sicherheitsrelevanter Vorgänge, getrennt und zweckgebunden | MUSS |
| D-07 | **Keine personenbezogene Auswertung von Abwesenheiten — technisch ausgeschlossen** | MUSS |
| D-08 | Keine Erhebung von Gesundheitsdaten; Formulardesign lenkt aktiv davon weg | MUSS |
| D-09 | Zwei-Faktor-Authentifizierung mindestens für SL, SL-V, ADM | MUSS |
| D-10 | Keine Fremdressourcen (Tracking, CDN, Analyse) | MUSS |
| D-11 | Administration ohne fachlichen Zugriff auf Antragsinhalte | SOLL |
| D-12 | Datenschutzhinweis nach Art. 13 DSGVO im Formular | MUSS |
| D-13 | Unterstützung der Betroffenenrechte (Auskunft, Berichtigung, Löschung) | MUSS |
| D-14 | Getestete Wiederherstellung aus dem Backup | MUSS |

## Q — Qualität und Betrieb

| ID | Anforderung | Prio |
|---|---|---|
| Q-01 | Bedienbar auf dem Smartphone — Anträge entstehen selten am Schreibtisch | MUSS |
| Q-02 | Ein Antrag in unter 3 Minuten ausfüllbar; Entscheidung in unter 30 Sekunden | MUSS |
| Q-03 | Barrierearme Bedienung (Tastatur, Kontrast, Screenreader-Grundlagen) | SOLL |
| Q-04 | Betrieb und Pflege durch **mindestens zwei** Personen leistbar | MUSS |
| Q-05 | Dokumentation für Betrieb und Fachadministration | MUSS |
| Q-06 | Datenexport in offenem Format — kein Anbieter-Einschluss | SOLL |
| Q-07 | Definierter Papier-Rückfallweg bei Ausfall | SOLL |
| Q-08 | Automatisierte Tests mindestens für Berechtigungslogik und Statusübergänge | SOLL |

---

## Die fünf Kriterien, an denen sich die Technologiewahl entscheidet

Wenn wir in die nächste Phase gehen, zählen erfahrungsgemäß nicht die Funktionen — die kann
fast jede Lösung. Es zählen diese fünf:

1. **Feldgenaue Berechtigungen (D-02, F-09).** Viele einfache Formular- und
   Workflow-Werkzeuge kennen nur „Vorgang sichtbar / nicht sichtbar". Damit lässt sich die
   reduzierte Sicht der Vertretungsplanung nicht sauber abbilden — und das ist kein Detail,
   sondern der Kern des Datenschutzkonzepts.
2. **Hosting-Ort und AV-Vertrag (D-01).** Scheidet die Hälfte der naheliegenden Werkzeuge
   sofort aus. Sollte deshalb **zuerst** geprüft werden, nicht zuletzt.
3. **Wartbarkeit durch mehr als eine Person (Q-04).** Ein System, das nur eine Person
   betreiben kann, ist ein Risiko für die Schule — unabhängig von seiner Qualität.
4. **Löschautomatik (D-05).** Werkzeuge, die kein automatisches Löschen nach Fristen
   beherrschen, erzeugen dauerhaften manuellen Aufwand, der erfahrungsgemäß unterbleibt.
5. **Akzeptanz im Kollegium (Q-01, Q-02).** Ein System, das umständlicher ist als eine
   Mail an die Schulleitung, wird umgangen. Dann hat die Schule beide Verfahren parallel —
   das schlechteste aller Ergebnisse.

---

## Stufenplan (Vorschlag)

| Stufe | Inhalt | Nutzen |
|---|---|---|
| **Stufe 1** | Antragsarten A und C, vollständiger Workflow, alle MUSS-Anforderungen, Benachrichtigungen, reduzierte Sichten | Der Großteil des Alltagsnutzens; echte Erprobung mit realen Anträgen |
| **Stufe 2** | Antragsarten B und D, Anlagen, Begleitpersonen-Zustimmung, Änderungsanträge, Export für die Vertretungsplanung | Abdeckung der aufwändigen Fälle |
| **Stufe 3** | Schnittstelle Vertretungsplan, Kalender, Kennzahlen, konfigurierbare Antragsarten | Automatisierung und Entlastung |

**Empfehlung:** Stufe 1 zunächst über ein Schulhalbjahr mit einer kleinen Gruppe erproben
(Schulleitung, Vertretungsplanung beider Standorte, eine Fachschaft), parallel zum bisherigen
Verfahren. Erst danach schulweit einführen. Das reduziert das Risiko, die Beteiligung von
Personalrat und Datenschutz belastbar zu machen, auf ein überschaubares Maß — und liefert
echte Argumente statt Annahmen.
