# 08 — Datenschutz: Umsetzung und Beteiligung

> **Kein Rechtsrat.** Die Texte in diesem Dokument sind Entwürfe zur Vorlage bei der
> zuständigen Datenschutzbeauftragten bzw. dem Datenschutzbeauftragten und beim
> Personalrat. Sie ersetzen deren Prüfung nicht. Paragrafenangaben sind zu verifizieren.

Dieses Dokument setzt die Entscheidungen aus [00-entscheidungen.md](00-entscheidungen.md)
um. Es ersetzt die allgemeinen Teile von [03-datenschutz-sicherheit.md](03-datenschutz-sicherheit.md),
wo beide sich widersprechen.

---

## 1. Warum die Löschfrist in diesem System besonders viel trägt

Nach Entscheidung **E-6.4** sehen vier Personen den vollständigen Antragsinhalt
einschließlich der Freitext-Begründung: Schulleitung, Stellvertretung und die beiden
Stundenplanungen. Das ist sachlich begründet und ein kleiner Kreis.

Damit verlagert sich der Schutz aber fast vollständig auf die **Zeit**. Der Unterschied
zwischen dem bisherigen Papierverfahren und einer Datenbank ist nicht, *wer* liest —
es ist, *wie lange* und *wie leicht auffindbar*. Ein Zettel verschwand irgendwann in einem
Ordner und praktisch aus dem Zugriff. Ein Datensatz bleibt durchsuchbar, bis ihn jemand
löscht.

**Die Löschfrist stellt genau diesen verlorenen Zustand wieder her.** Sie ist damit die
tragende Maßnahme dieses Konzepts, nicht eine Formalie am Rand.

---

## 2. Vorschlag Löschfristen

| Was | Frist | Beginn | Begründung |
|---|---|---|---|
| **Anträge beider Antragsarten**, einschließlich Kommentarverlauf, Entscheidung und Anhängen | **12 Monate** | Ende des beantragten Zeitraums | Deckt das laufende und das folgende Schuljahr, in dem noch Rückfragen entstehen können. Danach besteht kein Zweck mehr |
| Entwürfe, die nie eingereicht wurden | 90 Tage | letzte Bearbeitung | Angefangen und liegengelassen — kein Verarbeitungszweck |
| Protokolldaten (Anmeldungen, Zugriffe, Statusänderungen) | 6 Monate | Eintrag | Ausreichend zur Klärung von Störungen und Missbrauch, zu kurz für eine Verhaltensauswertung |
| Benutzerkonten ausgeschiedener Personen | sofort deaktivieren, Löschung nach Ablauf aller zugehörigen Antragsfristen | Ausscheiden | Kein Zugang ohne Beschäftigungsverhältnis |

**Der Löschlauf läuft automatisch.** Eine Frist, die jemand von Hand anstoßen muss, wird
nicht eingehalten — erst recht nicht in einem System, das nebenher betrieben wird.
Protokolliert wird die Tatsache der Löschung, nicht der gelöschte Inhalt.

### Das „Archiv" entfällt — *entschieden (E-7.2)*

Der Menüpunkt **Archiv** aus dem Prototyp wird nicht umgesetzt. Ein eigener Bereich dieses
Namens suggeriert Dauerhaftigkeit und widerspricht damit der Löschfrist. Was gebraucht
wird, leistet ein Filter *abgeschlossene anzeigen* in den vorhandenen Listen — und der
weckt diese Erwartung nicht.

---

## 3. Datenschutzhinweis für das Formular (Entwurf)

Zur Einblendung unter dem Formular, ausklappbar. Bewusst kurz — ein Hinweis, den niemand
liest, erfüllt seinen Zweck nicht.

> **Hinweise zum Datenschutz**
>
> **Wer verarbeitet Ihre Daten?** Die Johann-Christian-Senckenberg-Schule, vertreten durch
> die Schulleitung. Fragen zum Datenschutz beantwortet [Datenschutzbeauftragte/r, Kontakt].
>
> **Wozu?** Um Ihren Antrag zu bearbeiten, darüber zu entscheiden und die Vertretung des
> Unterrichts zu organisieren. Rechtsgrundlage ist die Erfüllung dienstlicher Aufgaben
> (Art. 6 Abs. 1 lit. c und e DSGVO in Verbindung mit § 23 HDSIG und dem Hessischen
> Schulgesetz).
>
> **Wer sieht Ihren Antrag?** Die Schulleitung und ihre Vertretung. Nach der Genehmigung
> zusätzlich die Stundenplanung des betroffenen Standorts — sie benötigt die Angaben, um
> die Vertretung zu planen und die Abwesenheit im Stundenplanprogramm einzutragen.
> Abgelehnte oder zurückgezogene Anträge sieht die Stundenplanung nicht.
>
> **Wie lange?** Ihr Antrag wird 12 Monate nach Ende des beantragten Zeitraums automatisch
> gelöscht, einschließlich aller Anhänge und Kommentare.
>
> **Was Sie bitte nicht angeben:** Angaben zu Erkrankungen, Diagnosen oder zur Gesundheit
> von Angehörigen. Für die Entscheidung genügt der Anlass. Laden Sie bitte keine
> ärztlichen Bescheinigungen hoch.
>
> **Keine Auswertung.** Ihre Anträge werden nicht dazu verwendet, Ihr Verhalten oder Ihre
> Leistung zu bewerten. Es gibt keine personenbezogenen Abwesenheitsstatistiken.
>
> **Ihre Rechte:** Auskunft, Berichtigung, Löschung und Einschränkung der Verarbeitung
> (Art. 15–18 DSGVO) sowie Beschwerde beim Hessischen Beauftragten für Datenschutz und
> Informationsfreiheit.

---

## 4. Eckpunkte für eine Dienstvereinbarung (Entwurf)

Das System ist eine technische Einrichtung, die objektiv geeignet ist, Verhalten und
Leistung von Beschäftigten zu überwachen — unabhängig davon, dass es nicht so gemeint ist.
Damit ist es **mitbestimmungspflichtig** (§ 74 HPVG, Ziffer prüfen). Eine Dienstvereinbarung
ist der übliche und der für alle Seiten günstigste Weg: Sie schafft Klarheit und nimmt dem
Kollegium die Sorge.

**Vorgeschlagene Punkte:**

1. **Zweckbindung.** Das System dient ausschließlich der Bearbeitung von Anträgen auf
   Dienst-/Unterrichtsbefreiung und für Unterrichtsgänge sowie der Organisation der
   Vertretung. Jede andere Nutzung ist ausgeschlossen.
2. **Auswertungsverbot.** Personenbezogene Auswertungen über die Bearbeitung des
   Einzelfalls hinaus finden nicht statt — insbesondere keine Statistik über
   Abwesenheitstage, Antragshäufigkeit oder Ablehnungsquoten einzelner Beschäftigter.
   Aggregierte Zahlen ohne Personenbezug bleiben zulässig.
3. **Zugriffskreis abschließend benannt.** Schulleitung, stellvertretende Schulleitung und
   die beiden Stundenplanungen — gebunden an die **Funktion**, nicht an die Person.
   Erweiterungen bedürfen der erneuten Beteiligung des Personalrats.
4. **Keine Krankmeldungen.** Das System nimmt keine Krankmeldungen und keine Atteste
   entgegen. Gesundheitsdaten werden nicht erhoben.
5. **Löschfristen** wie in Abschnitt 2, automatisch vollzogen.
6. **Protokolldaten.** Werden ausschließlich zur Sicherheit und Fehlerklärung verwendet,
   nicht zur Bewertung von Beschäftigten, und nach 6 Monaten gelöscht. Zugriff nur für
   Administration und Datenschutzbeauftragte.
7. **Keine automatisierte Entscheidung.** Über jeden Antrag entscheidet ein Mensch. Es gibt
   keine Genehmigung durch Zeitablauf.
8. **Freiwilligkeit der Angaben.** Über den Anlass hinaus sind keine Einzelheiten
   anzugeben; ein Stichwort genügt.
9. **Einsichtsrecht des Personalrats** in die Systemkonfiguration (Rollen, Fristen,
   Auswertungen) auf Verlangen.
10. **Rückfallweg.** Bei Ausfall des Systems bleibt der bisherige Weg zulässig; niemandem
    entsteht ein Nachteil aus einer Störung.

---

## 5. Verzeichnis von Verarbeitungstätigkeiten (Zuarbeit)

Vorbereitete Angaben für den Eintrag nach Art. 30 DSGVO:

| Feld | Inhalt |
|---|---|
| Bezeichnung | Antragsverfahren Dienst-/Unterrichtsbefreiung und Unterrichtsgänge |
| Verantwortlicher | Johann-Christian-Senckenberg-Schule, vertreten durch die Schulleitung |
| Zweck | Bearbeitung und Entscheidung über Anträge Beschäftigter; Organisation der Unterrichtsvertretung |
| Rechtsgrundlage | Art. 6 Abs. 1 lit. c, e DSGVO i. V. m. § 23 HDSIG, Hessisches Schulgesetz |
| Betroffene | Lehrkräfte und Lehrkräfte im Vorbereitungsdienst der Schule |
| Datenkategorien | Name, dienstliche E-Mail, Standort; Zeitraum und Stunden der Abwesenheit; Anlass (Kategorie und Kurztext); Lerngruppen; Begleitpersonen; Entscheidung und Kommentare; Anhänge |
| Besondere Kategorien (Art. 9) | **Nicht vorgesehen.** Formularhinweise und Verzicht auf Attest-Upload wirken darauf hin |
| Empfänger | Ausschließlich intern: Schulleitung, Stellvertretung, Stundenplanung des betroffenen Standorts. Keine Übermittlung an Dritte |
| Auftragsverarbeiter | [Hosting, Mailversand — in Schritt 8 festzulegen] |
| Drittlandtransfer | Keiner |
| Löschfristen | Siehe Abschnitt 2 |
| Technische Maßnahmen | Siehe [03-datenschutz-sicherheit.md](03-datenschutz-sicherheit.md), Abschnitt 5 |

---

## 6. Schwellwertprüfung Datenschutz-Folgenabschätzung

Die Prüfung nach Art. 35 DSGVO ist **in jedem Fall durchzuführen und zu dokumentieren** —
auch wenn sie zum Ergebnis kommt, dass keine DSFA nötig ist.

| Spricht für eine DSFA | Spricht dagegen |
|---|---|
| Systematische Verarbeitung von Beschäftigtendaten | Sehr kleiner Betroffenenkreis (ein Kollegium) |
| Bewertender Charakter (Entscheidung über Anträge, Ablehnungsbegründungen) | Keine automatisierte Entscheidung, keine Profilbildung |
| Abhängigkeitsverhältnis Beschäftigte–Dienstherr | Kurze Löschfristen, kleiner Zugriffskreis |
| Angaben mit Bezug zu persönlichen Lebensumständen im Freitextfeld | Keine besonderen Kategorien vorgesehen |

**Einschätzung:** Eine vollständige DSFA ist eher nicht erforderlich, die dokumentierte
Prüfung aber Pflicht. Die Entscheidung trifft die/der Datenschutzbeauftragte.

---

## 7. Reihenfolge der Beteiligung

Der häufigste Fehler in solchen Projekten ist, Personalrat und Datenschutz erst das
fertige System zu zeigen. Dann wird aus einer Beratung eine Genehmigungshürde.

| Wann | Wer | Was |
|---|---|---|
| **Jetzt** | Datenschutzbeauftragte/r | Konzept vorlegen, Löschfristen und Zugriffskreis abstimmen, Schwellwertprüfung anstoßen |
| **Jetzt** | Personalrat | Vorhaben vorstellen, Eckpunkte der Dienstvereinbarung besprechen |
| Vor der Erprobung | beide | Datenschutzhinweis und Dienstvereinbarung abstimmen |
| Vor der Erprobung | Schulleitung | Verzeichnis von Verarbeitungstätigkeiten eintragen |
| Vor dem Regelbetrieb | Personalrat | Dienstvereinbarung abschließen |
| Vor dem Regelbetrieb | Kollegium | Kurzinformation: was das System tut — und was es ausdrücklich nicht tut |

**Der Zeitpunkt ist günstig:** Es gibt noch kein laufendes System und keine echten Daten
(E-2.4). Beide Gremien beraten also über ein Vorhaben, nicht über vollendete Tatsachen —
das ist die Situation, in der Beteiligung am wenigsten Reibung erzeugt.

---

## 8. Offene Punkte

Alle geklärt:

* Archiv entfällt (E-7.2)
* Löschfrist 12 Monate bestätigt (E-7.1)
* Personalrat vorhanden, noch nicht informiert → Anschreiben in
  [09-vorlagen-beteiligung.md](09-vorlagen-beteiligung.md)
* Datenschutzbeauftragte/r vorhanden, noch kein Kontakt → ebenda
* Keine bestehende Dienstvereinbarung — die vorgeschlagene wäre die erste. Das bedeutet
  etwas mehr Aufwand beim ersten Mal, aber auch: Der Rahmen kann passend zugeschnitten
  werden, statt sich an eine vorhandene Vereinbarung anlehnen zu müssen.
