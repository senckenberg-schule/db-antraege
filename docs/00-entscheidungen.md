# 00 — Entscheidungsprotokoll

Laufendes Protokoll der gemeinsam getroffenen Entscheidungen. **Dieses Dokument ist
maßgeblich.** Die Dokumente 01–05 sind der ursprüngliche Entwurf mit Annahmen; sie werden
nach Abschluss der fachlichen Schritte (1–6) auf diesen Stand gebracht.

---

## Schritt 1 — Beteiligte und Rollen · *entschieden*

### E-1.1 Entscheidungsbefugnis
**Die Schulleitung entscheidet allein und standortübergreifend.** Keine Vorprüfung durch
Abteilungs- oder Standortleitungen, keine zweite Genehmigungsstufe.
→ Ein Antrag = eine Entscheidung.

### E-1.2 Vertretung der Schulleitung
**Die stellvertretende Schulleitung erhält dieselben Entscheidungsrechte**, nutzt sie aber
nur bei Abwesenheit der Schulleitung.

*Umsetzungshinweis:* Technisch ist das **eine** Rolle mit Entscheidungsrecht, die zwei
Personen innehaben. Eine Ein-/Ausschaltmechanik („Vertretungsmodus") wird bewusst **nicht**
gebaut — sie erzeugt genau dann Reibung, wenn sie gebraucht wird (die Schulleitung ist
krank und kann den Modus nicht mehr aktivieren). Stattdessen: Beide sehen den Arbeitsvorrat,
die Absprache wer entscheidet ist eine organisatorische, keine technische.

*Folge für die Übersicht:* Jeder Antrag zeigt sichtbar, **wer** entschieden hat.

### E-1.3 Vertretungs-/Stundenplanung
**Eine Person für beide Standorte.**

*Wesentliche Vereinfachung:* Damit ist der Standort für die Stundenplanung kein
Verteilkriterium, sondern nur **Inhalt** der Meldung (welche Lerngruppen an welchem Haus).
Die Standortweiche wirkt nur noch beim Sekretariat (E-1.4).

*Risiko, das dadurch entsteht:* Auch hier hängt eine Funktion an einer einzelnen Person.
Die Benachrichtigung geht deshalb an ein **Rollenpostfach**, nicht an eine persönliche
Adresse, und die Übersicht genehmigter Abwesenheiten ist auch für die Schulleitung
einsehbar — damit bei Ausfall jemand übernehmen kann.

### E-1.4 Sekretariat
**Zwei Sekretariate, je Standort eines.** Aufgabe im Workflow: **ausschließlich
Kenntnisnahme** — wissen, wer wann nicht im Haus ist (Telefon, Besucher, Auskunft).
Keine Kostenabwicklung, keine Veranstaltungsorganisation über dieses System.

*Folge — sehr geringer Datenbedarf:* Das Sekretariat erhält nur
**Name · Zeitraum · Standort · Antragsart**. Kein Anlass, keine Lerngruppen, keine Stunden,
keine Kommentare, keine Kosten. Das ist die schlankeste Sicht im ganzen System.

*Dies ist die einzige Stelle, an der die Standortauswahl den Empfängerkreis steuert.*

### E-1.5 Antragsberechtigte
**Lehrkräfte und Lehrkräfte im Vorbereitungsdienst.** Verwaltungspersonal, Hausmeisterei
und weiteres Personal bleiben zunächst im bisherigen Verfahren.

### Rollenübersicht nach Schritt 1

| Rolle | Anzahl | Standortbindung | Rechte |
|---|---|---|---|
| Antragstellende Person | alle Lehrkräfte + LiV | — | eigene Anträge stellen, ergänzen, zurückziehen, stornieren |
| Schulleitung | 1 | keine (beide Standorte) | entscheiden, alle Anträge sehen |
| Stellvertretende Schulleitung | 1 | keine | identisch — für Abwesenheitsfälle |
| Vertretungsplanung | 1 | keine (beide Standorte) | genehmigte Abwesenheiten in reduzierter Sicht |
| Sekretariat | 2 | **je Standort** | Minimalsicht, nur eigener Standort |
| Administration | 1–2 | — | Benutzer/Stammdaten, kein Zugriff auf Antragsinhalte |

### Offen aus Schritt 1 — später zu klären

* **O-1.1** Wer wickelt Reisekosten und Busbestellungen ab, wenn nicht das Sekretariat?
  Läuft das ganz außerhalb des Systems? (→ relevant in Schritt 2 bei Fortbildungen und Fahrten)
* **O-1.2** Sonderfall Vorbereitungsdienst: Bei Lehrkräften im Vorbereitungsdienst ist neben
  der Schule ggf. das Studienseminar zu beteiligen. Braucht der Workflow dafür etwas —
  oder bleibt das ein Vorgang außerhalb des Systems? (→ Schritt 4)
* **O-1.3** Wer übernimmt die Administration (Benutzerverwaltung, Stammdaten)? (→ Schritt 8)

---

## Schritt 2 — Antragsarten und Startumfang · *in Arbeit*

### E-2.1 Antragsarten im Endausbau
Bestätigt sind alle vier Arten des Entwurfs:

| Art | Bezeichnung | Kern |
|---|---|---|
| **A** | Dienstbefreiung | eine Person, persönlicher Anlass |
| **B** | Fortbildung / Dienstreise | eine Person, dienstlicher Anlass, Kostenbezug |
| **C** | Unterrichtsgang / Exkursion | Lerngruppen + Begleitpersonen, eintägig |
| **D** | Mehrtägige Fahrt / Großveranstaltung | wie C, zusätzlich Übernachtung, Kosten, Beschlusslage |

**Offen:** Die antragstellende Person hat auf ein bestehendes Dokument mit weiteren
Antragsarten verwiesen („siehe Anhang"). Das Dokument liegt noch nicht vor.
→ Liste ist bis dahin **nicht abschließend**.

### E-2.2 Startumfang Stufe 1
**Dienstbefreiung (A) + Unterrichtsgang (C).**

*Begründung:* A und C sind die beiden Gegenpole des Datenmodells — eine Person ohne
Lerngruppenbezug gegenüber ganzen Lerngruppen mit Begleitpersonen und Vertretungsbedarf.
Trägt das Konzept beide, sind B und D im Wesentlichen Varianten davon (B ≈ A mit Kosten,
D ≈ C mit Übernachtung).

*Folge für die Umsetzung:* Die Struktur für **betroffene Lerngruppen, Begleitpersonen und
Vertretungsbedarf** gehört in Stufe 1, nicht in eine Ausbaustufe. Sie nachträglich
einzuziehen wäre der teuerste denkbare Umbau.

### E-2.3 Bestehende Formulare sind Vorlage, nicht Beiwerk
An der Schule existieren **eigene, eingeführte Papierformulare**. Die digitalen Formulare
werden daran ausgerichtet: gleiche Felder, gleiche Reihenfolge, gleiche Bezeichnungen.

*Begründung:* Vertraute Formulierungen senken die Einführungshürde stärker als jede
Schulung. Abweichungen erfolgen nur mit konkretem Grund und werden einzeln begründet —
typischerweise: Pflichtfeld statt leer lassbarer Zeile, Auswahlliste statt Freitext
(Datenschutz), neue Standortauswahl.

### Offen aus Schritt 2
* **O-2.1** Bestehende Formulare liegen noch nicht vor → Feldabgleich ausstehend (Schritt 6)
* **O-2.2** Weitere Antragsarten aus dem angekündigten Dokument prüfen

---

## Schritt 2 — *abgeschlossen*

### E-2.4 Ausgangslage des vorhandenen Prototyps
* **Nur die Oberfläche existiert**, kein Backend hinter `/api/antrag`; Schulleiter-Ansicht
  und Archiv sind Platzhalter.
* Erstellt vom Auftraggeber selbst mit KI-Unterstützung; Pflege ebenfalls dort.
* Läuft bisher **nur lokal**, nicht erreichbar, **keine echten Daten**.

**Folge — der günstigste denkbare Zeitpunkt:** Anmeldung, Berechtigungen, Löschkonzept und
Datenschutzhinweis können eingebaut werden, *bevor* der erste echte Antrag existiert.
Keine Migration, keine Altdaten, kein Umbau im laufenden Betrieb.

**Folge für die Technologiewahl (Q-04):** Das System hängt an einer Person. Daraus folgt
kein Abbruch, aber ein Kriterium: **Standardtechnologie und gute Dokumentation vor
eleganter Lösung** — damit im Vertretungsfall jemand anderes übernehmen kann. Wird in
Schritt 8 als Entscheidungskriterium geführt.

---

## Schritt 3 — Standortlogik · *entschieden*

Ausgangsproblem: Im Prototyp erscheint „An beiden Standorten" nur im Zeitraum-Zweig und
kennt nur „beide" — bei einem Einzeltag ist der Standort gar nicht angebbar, und bei nicht
gesetzter Checkbox bleibt offen, *welcher* Standort gemeint ist.

### E-3.1 Form der Angabe
**Pflichtauswahl mit drei Möglichkeiten, sichtbar in beiden Zweigen** (Einzeltag *und*
Zeitraum):

```
Betroffener Standort *     ○ Standort A     ○ Standort B     ○ Beide Standorte
```

Sobald eine Anmeldung existiert, wird der Stammstandort vorbelegt — als Vorschlag,
immer änderbar.

### E-3.2 „Beide" ist bei Einzeltagen ein Regelfall, kein Sonderfall
Lehrkräfte unterrichten **regelmäßig an einem Tag an beiden Standorten**. Die Auswahl
„Beide" muss daher auch beim Einzeltag zur Verfügung stehen.

**Keine Aufteilung der Stunden je Standort.** Die Standortangabe beantwortet nur die Frage
*„in welchem Haus fehlt diese Person?"* — sie steuert damit das Sekretariat. Welche Stunde
an welchem Haus liegt, ergibt sich aus dem Stundenplan und ist der Vertretungsplanung
ohnehin bekannt. Ein zweites Stundenfeld je Standort würde das Formular verkomplizieren,
ohne eine Frage zu beantworten, die jemand tatsächlich hat.

### E-3.3 Standortangabe ist auch bei Unterrichtsgängen zwingend — *korrigiert*

> **Korrektur.** Eine frühere Fassung dieses Punktes sah vor, den Standort bei Antragsart 2
> automatisch aus den gewählten Lerngruppen abzuleiten. Das ist **nicht möglich:**
> An beiden Standorten existieren **gleichlautende Lerngruppenbezeichnungen**.

**„9b" identifiziert keine Lerngruppe.** Eindeutig ist erst das Paar
**Standort + Bezeichnung** — also `9b (Standort A)` gegenüber `9b (Standort B)`.

Daraus folgt für **alle** Antragsarten: Die Standortauswahl aus E-3.1 ist eine
**Pflichtangabe und wird nirgends abgeleitet.**

### E-3.4 Lerngruppen als Freitextfeld — *Entscheidung des Auftraggebers*

Die Lerngruppen werden **frei eingetragen**, nicht aus einer Liste gewählt.

**Begründung (maßgeblich):**
1. Mal ist eine einzelne Lerngruppe betroffen, mal mehrere — Freitext bildet beides ohne
   Umschweife ab.
2. **Eine gepflegte Lerngruppenliste müsste jedes Schuljahr angepasst werden.** Das ist
   wiederkehrender Aufwand, der bei einem von einer Person betriebenen System
   erfahrungsgemäß irgendwann unterbleibt — und eine veraltete Liste ist schlechter als
   gar keine, weil man ihr vertraut.

**Warum das tragfähig ist:** Der eigentliche Grund für eine Liste war die Verwechslung
gleichnamiger Lerngruppen beider Standorte. Dieses Problem löst bereits das **Pflichtfeld
Standort** aus E-3.1. `9b` im Freitext zusammen mit `Standort A` im Auswahlfeld ist
ebenso eindeutig wie ein Listeneintrag.

```
Betroffener Standort *   ○ Standort A   ○ Standort B   ○ Beide Standorte
Betroffene Lerngruppen * [ 9b, 10a                                      ]
                           Vorschläge erscheinen beim Tippen
```

### E-3.5 Selbstlernende Vorschläge statt gepflegter Liste

Das Feld ist Freitext, schlägt aber beim Tippen Werte vor, **die bereits in früheren
Anträgen vorkamen** (im laufenden Schuljahr, am gewählten Standort).

*Der Punkt daran:* Die Vorschlagsliste entsteht von selbst aus dem, was das Kollegium
einträgt, und veraltet von selbst mit dem Schuljahreswechsel. **Niemand pflegt sie.**
Nach wenigen Wochen wirkt sie wie eine gepflegte Lerngruppenliste, ohne je eine geworden zu
sein. Wer etwas Neues eintippt, wird nicht gehindert — Vorschlag, keine Vorschrift.

Zusätzlich beim Speichern: stille Normalisierung (Leerzeichen zusammenfassen, Trennzeichen
vereinheitlichen). **Keine Prüfung, keine Ablehnung, keine Fehlermeldung** — das Feld darf
niemanden aufhalten.

### E-3.6 Was wir dafür aufgeben

Ehrlich benannt, damit es später keine Überraschung ist:

| Entfällt | Bedeutung |
|---|---|
| Automatischer Konflikthinweis („für 9b liegt am selben Tag bereits ein Unterrichtsgang vor") | War als SOLL geplant, nicht als MUSS. Freitext lässt sich nicht zuverlässig vergleichen. |
| Auswertung nach Lerngruppen | Etwa „wie viele Unterrichtsgänge hatte die 9b". Aggregierte Kennzahlen je Antragsart und Standort bleiben möglich. |
| Einheitliche Schreibweise | `9b`, `9 b`, `9B` stehen nebeneinander. Die Normalisierung mildert das, beseitigt es nicht. |

Die Anzeigeregel bleibt bestehen: Lerngruppen werden **immer zusammen mit dem Standort**
des Antrags ausgegeben — in Übersichten, im Archiv und in Benachrichtigungen. Nie nur „9b".

### E-3.7 Sprachregelung: „Lerngruppe", nicht „Klasse"

Durchgängig in Formular, Oberfläche, Benachrichtigungen und allen Dokumenten heißt es
**Lerngruppe**.

*Grund:* „Klasse" trifft nur einen Teil der Fälle. Betroffen sind ebenso Kurse,
jahrgangsübergreifende Gruppen, Fachgruppen und Teilgruppen — die Bezeichnung muss alles
davon selbstverständlich einschließen, statt es als Sonderfall erscheinen zu lassen.

Feste Begriffe („Klassenfahrt", „Klassenkonferenz") bleiben davon unberührt.

### Wirkung der Standortangabe — Zusammenfassung

| Empfänger | Wirkt der Standort? |
|---|---|
| Schulleitung | nein — entscheidet standortübergreifend (E-1.1) |
| Vertretungsplanung | nein als Verteilkriterium — eine Zuständigkeit für beide Häuser (E-1.3); der Standort ist dort **Inhalt** und zur Unterscheidung gleichnamiger Lerngruppen unverzichtbar |
| **Sekretariat** | **ja** — bestimmt, welches der beiden Sekretariate informiert wird (E-1.4) |

Die Standortauswahl hat damit genau **einen** verteilungsrelevanten Zweck. Das ist wenig —
aber es ist der Grund, warum die Angabe eindeutig sein muss und nicht als „beide ja/nein"
genügt.

### Offen aus Schritt 3
* **O-3.1** Wie heißen die beiden Standorte im Sprachgebrauch des Kollegiums?
  (Platzhalter „Standort A / B" bis zur Klärung)
