# 06 — Bestandsaufnahme: vorhandener Prototyp

Grundlage: `docs/bestand/antrag.html` (Stand: vom Auftraggeber übergeben).
Es handelt sich **nicht um ein Papierformular**, sondern um eine bereits gebaute
Weboberfläche der Johann-Christian-Senckenberg-Schule mit der Bezeichnung
„Dienstbefreiungssystem".

Erkennbarer Umfang laut Navigation: `Start` · `Antrag stellen` · `Schulleiter` · `Archiv`,
Formularversand per `POST /api/antrag` gegen ein Backend, das aus dieser Datei nicht
hervorgeht.

**Das ist eine sehr gute Ausgangslage.** Der Prototyp zeigt, wie an der Schule tatsächlich
gedacht und formuliert wird — das ist mehr wert als jede Annahme von außen. Die folgenden
Punkte sind deshalb keine Kritik an der Arbeit, sondern die Liste dessen, was beim Übergang
vom Prototyp zum Regelbetrieb noch zu klären ist.

---

## 1. Die Feldstruktur des Bestands

### Abschnitt „Antragsteller/in"
| Feld | Typ | Pflicht |
|---|---|---|
| Name der Lehrkraft | Freitext | ✓ |
| Datum der Antragstellung | automatisch (heutiges Datum) | — |

### Abschnitt „Der Unterricht ist zu vertreten …"
Umschalter: **einzelner Tag** oder **Zeitraum (mehrere Tage)**

| Feld | Typ | Sichtbar bei |
|---|---|---|
| Datum | Datum | Einzeltag |
| Ganztags | Checkbox | Einzeltag |
| In folgenden Stunden | Freitext (`z. B. 1–3`) | Einzeltag, wenn nicht ganztags |
| Betroffene Pausenaufsichten davor/danach | Freitext | Einzeltag |
| Von / Bis | Datum | Zeitraum |
| **An beiden Standorten** | Checkbox | **nur Zeitraum** |

### Abschnitt „Begründung" (Auswahl, Pflicht)
| Auswahl | Zusatzfeld |
|---|---|
| **Fortbildung** | Ort und Thema (Pflicht) + Hinweis auf Bestätigung/Programm |
| **Dienstliche Gründe** | — (Dienstbesprechung / Teamsitzung / Klassenkonferenz) |
| **Arztbesuch** | — („da kein Termin in der unterrichtsfreien Zeit möglich ist") |
| **Persönliche Gründe** | „Bitte Grund angeben" (Pflicht, Freitext) |
| **Sonstiges** | „Bitte Grund angeben" (Pflicht, Freitext) |

### Abschnitt „Unterlagen für die Vertretung" (Auswahl, Pflicht)
* … liegen dem Antrag bei
* … werden den Kolleginnen/Kollegen ausgehändigt (vereinbarter Ablageort)
* … werden im Schulportal hinterlegt

Zusätzlich: optionaler Anhang (PDF, JPG, PNG, DOC, DOCX; max. 10 MB).

---

## 2. Was der Bestand besser macht als unser Entwurf

Drei Punkte übernehmen wir unverändert — sie sind näher an der Praxis als das, was in
[01-fachkonzept.md](01-fachkonzept.md) stand:

1. **Die Überschrift „Der Unterricht ist zu vertreten …".** Sie fragt nicht nach der
   Abwesenheit einer Person, sondern nach dem, was daraus folgt. Genau darum geht es
   der Schule, und genau das braucht die Vertretungsplanung.
2. **„Pausenaufsichten davor/danach".** Im Entwurf nicht enthalten, in der Praxis
   unverzichtbar — eine vergessene Pausenaufsicht ist ein Aufsichtsproblem, kein
   Organisationsdetail.
3. **„Unterlagen für die Vertretung" mit drei konkreten Wegen.** Deutlich besser als ein
   abstraktes Feld „Vertretungsregelung": Die drei Antworten sind die, die es real gibt.

---

## 3. Strukturelle Korrektur an unserem Entwurf

Der Entwurf hatte **Dienstbefreiung (A)** und **Fortbildung/Dienstreise (B)** als getrennte
Antragsarten geführt. Der Bestand macht es anders und besser: Es gibt **einen** Antrag auf
Dienst-/Unterrichtsbefreiung, und *Fortbildung* ist eine **Begründung** darin.

Das ist fachlich stimmiger — aus Sicht der Vertretungsplanung ist beides derselbe Vorgang
(eine Person fehlt, Unterricht ist zu vertreten), und für die antragstellende Person ist es
ein Formular statt zweier fast identischer.

**Überarbeitetes Antragsartenmodell:**

| Antragsart | Kern | Begründungen / Varianten |
|---|---|---|
| **1 — Dienst-/Unterrichtsbefreiung** | Eine Person ist abwesend, Unterricht ist zu vertreten | Fortbildung · Dienstliche Gründe · Arztbesuch · Persönliche Gründe · Sonstiges |
| **2 — Unterrichtsgang / Veranstaltung** | Lerngruppen sind unterwegs, Begleitpersonen fehlen im Unterricht | eintägig · mehrtägig (Fahrt) · schulintern (Projekttag, Fest) |

Damit ersetzt dieses Modell E-2.1 im Entscheidungsprotokoll. Der Startumfang aus E-2.2
bleibt unverändert gültig — er entspricht jetzt schlicht „beide Antragsarten".

**Für Antragsart 2 existiert noch kein Formular.** Das ist der Teil, den wir neu entwerfen.

---

## 4. Offene Punkte für den Regelbetrieb

Nach Wichtigkeit geordnet.

### 4.1 Keine Anmeldung — Identität wird behauptet, nicht nachgewiesen

„Name der Lehrkraft" ist ein freies Textfeld. Wer die Seite erreicht, kann einen Antrag
unter jedem beliebigen Namen stellen, und die Schulleitung kann am Antrag nicht erkennen,
ob er echt ist. Ebenso ist nichts davor, dass jemand fremde Anträge im Archiv einsieht.

Für einen Prototyp ist das völlig in Ordnung. Für den Regelbetrieb ist es der Punkt, der
zuerst gelöst werden muss — und er ist nicht nachrüstbar wie ein weiteres Feld: An der
Anmeldung hängt die gesamte Berechtigungslogik (wer sieht welchen Antrag, wer darf
entscheiden, wer sieht das Archiv).

→ **Das ist die zentrale Frage für Schritt 8** und der Grund, warum wir „welches
Anmeldeverfahren steht zur Verfügung" früh klären sollten.

### 4.2 Standortangabe ist unvollständig

Zwei Lücken:

* Die Checkbox „An beiden Standorten" erscheint **nur im Zeitraum-Zweig**. Bei einem
  Antrag für einen einzelnen Tag — dem häufigsten Fall — lässt sich der Standort gar
  nicht angeben.
* Die Checkbox kennt nur „beide". Ist sie nicht gesetzt, bleibt offen, **welcher** der
  beiden Standorte gemeint ist. Das System kann daraus nicht ableiten, welches Sekretariat
  zu informieren ist — und genau das ist laut Entscheidung E-1.4 die einzige Stelle, an der
  die Standortangabe den Empfängerkreis steuert.

→ Wird in **Schritt 3** gelöst.

### 4.3 „Persönliche Gründe" führt in ein Pflicht-Freitextfeld

Auf Papier unkritisch. In einer durchsuchbaren Datenbank ist dieses eine Feld die Stelle,
an der Trauerfälle, Erkrankungen von Angehörigen und familiäre Umstände landen — also
besondere Kategorien personenbezogener Daten nach Art. 9 DSGVO, für die deutlich strengere
Regeln gelten.

Bemerkenswert: **„Arztbesuch" ist im Bestand gut gelöst** — eigene Auswahl, kein Detailfeld,
keine Diagnose. Genau so soll es sein. Die Lücke ist nur „Persönliche Gründe".

→ Lösungsvorschlag in Schritt 6: Unterkategorien statt Freitext (z. B. familiärer Anlass ·
Behördentermin · Umzug · Prüfung), Freitext nur noch optional und mit sichtbarem Hinweis.

### 4.4 Stunden und Klassen nur als Freitext

`In folgenden Stunden` ist ein Textfeld („z. B. 1–3"), betroffene Klassen werden gar nicht
erfasst. Für die Dienstbefreiung trägt das noch. Für den Unterrichtsgang — der laut E-2.2
in Stufe 1 gehört — reicht es nicht: Dort müssen Lerngruppen, Begleitpersonen und
Vertretungsbedarf strukturiert vorliegen, sonst muss die Vertretungsplanung sie wieder
von Hand zusammensuchen.

### 4.5 Weitere Punkte

| Punkt | Bemerkung |
|---|---|
| Kein Datenschutzhinweis im Formular | Art. 13 DSGVO — ergänzen |
| Anhang ohne erkennbare Zugriffsbeschränkung | Muss berechtigungsgeprüft ausgeliefert werden, nicht frei abrufbar |
| Keine Fristprüfung | Aus Schritt 4/6 zu ergänzen |
| Keine Stornierung nach Genehmigung erkennbar | Wichtigster fehlender Statusübergang (siehe Entwurf) |
| Kein Rückfrage-Verlauf im Antragsformular sichtbar | Liegt evtl. in der Schulleiter-Ansicht — noch zu prüfen |
| Pflichtfeldprüfung nur im Browser | Muss serverseitig wiederholt werden |
| Bestätigung nennt nur „Der Schulleiter wurde per E-Mail informiert" | Inhalt dieser Mail ist zu prüfen (siehe Dokument 03, Abschnitt 5.4) |

---

## 5. Was wir als Nächstes wissen müssen

1. **Wie weit ist das System wirklich?** Gibt es das Backend hinter `/api/antrag`, die
   Schulleiter-Ansicht und das Archiv bereits — und läuft davon etwas im Schulbetrieb?
2. **Wer hat es gebaut und wer pflegt es?**
3. **Wo läuft es** (Schulserver, Hosting, lokal)?

Davon hängt ab, ob wir ein bestehendes System weiterentwickeln oder ein neues auf Basis der
guten Vorarbeit bauen. Das ist eine andere Frage als die Technologiewahl — und sie sollte
vor Schritt 8 beantwortet sein.
