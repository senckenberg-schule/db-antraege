# 07 — Formularfelder

Grundlage: der vorhandene Prototyp (`docs/bestand/antrag.html`) und die Entscheidungen aus
[00-entscheidungen.md](00-entscheidungen.md).

**Leitgedanke:** Der Bestand ist die Vorlage (E-2.3). Abweichungen erfolgen nur mit
konkretem Grund und werden einzeln begründet. Wortlaut und Reihenfolge bleiben erhalten,
wo es keinen Anlass zur Änderung gibt — vertraute Formulierungen senken die
Einführungshürde stärker als jede Schulung.

---

## Antragsart 1 — Dienst-/Unterrichtsbefreiung

### Abschnitt „Antragsteller/in"

| Feld | Typ | Pflicht | Gegenüber Prototyp |
|---|---|---|---|
| Name der Lehrkraft | — | — | **entfällt** — kommt aus der Anmeldung |
| Datum der Antragstellung | automatisch | — | unverändert |

### Abschnitt „Der Unterricht ist zu vertreten …"

| Feld | Typ | Pflicht | Gegenüber Prototyp |
|---|---|---|---|
| Einzelner Tag / Zeitraum | Umschalter | ✓ | unverändert |
| **Betroffener Standort** | Auswahl: Runkel · Villmar · Beide | ✓ | **neu**, in *beiden* Zweigen |
| Datum | Datum | ✓ | unverändert *(Einzeltag)* |
| Ganztags | Ankreuzfeld | — | unverändert *(Einzeltag)* |
| In folgenden Stunden | Freitext (`z. B. 1–3`) | — | unverändert, ausgeblendet bei „Ganztags" |
| Von / Bis | Datum | ✓ | unverändert *(Zeitraum)*; Checkbox „An beiden Standorten" entfällt |
| Betroffene Pausenaufsichten davor/danach | Freitext | — | **jetzt in beiden Zweigen** |

### Abschnitt „Begründung" (Auswahl, Pflicht)

| Auswahl | Zusatzfeld | Gegenüber Prototyp |
|---|---|---|
| **Fortbildung** | Ort und Thema (Pflicht) | unverändert |
| **Dienstliche Gründe** | — | unverändert |
| **Arztbesuch** | — | unverändert |
| **Persönliche Gründe** | Grund (Pflicht, kurz) | Hinweistext + Längenbegrenzung |
| **Sonstiges** | Grund (Pflicht, kurz) | Hinweistext + Längenbegrenzung |

### Abschnitt „Unterlagen für die Vertretung" (Auswahl, Pflicht)
Unverändert übernommen, im Wortlaut des Bestands:
* … liegen dem Antrag bei
* … werden den Kolleginnen/Kollegen ausgehändigt (vereinbarter Ablageort)
* … werden im Schulportal hinterlegt

### Anhang
Optional, PDF/JPG/PNG/DOC/DOCX, max. 10 MB — unverändert, aber **nur berechtigungsgeprüft
abrufbar** (nicht über eine erratbare Adresse).

### Datenschutzhinweis
**Neu.** Kurzer Hinweis nach Art. 13 DSGVO unter dem Formular: wer verarbeitet, wozu,
wie lange, wer sieht was. Ein Satz plus Link, nicht zwei Absätze Kleingedrucktes.

---

## Die Änderungen im Einzelnen

### Ä-1 Das Namensfeld entfällt
Im Prototyp ist der Name ein freies Textfeld. Damit kann jeder unter jedem Namen einen
Antrag stellen, und die Schulleitung sieht dem Antrag nicht an, ob er echt ist.

Nach der Anmeldung steht die Person fest und wird angezeigt, nicht abgefragt. **Ein Feld
weniger, das niemand ausfüllen muss — und der häufigste Tippfehler verschwindet mit ihm**
(„M. Müller", „Müller, Anna", „AM").

*Abhängigkeit:* Setzt die Anmeldung voraus (Schritt 8). Solange es sie nicht gibt, bleibt
das Feld als Übergangslösung bestehen.

### Ä-2 Standortauswahl ersetzt die Checkbox
Statt „An beiden Standorten" (nur im Zeitraum-Zweig, nur „beide" oder nichts) eine
Pflichtauswahl mit drei Möglichkeiten in beiden Zweigen:

```
Betroffener Standort *     ○ Runkel     ○ Villmar     ○ Beide Standorte
```

Grund: Die Auswahl entscheidet, welche der beiden Stundenplanungen die Meldung erhält
(E-5.7). Ein Antrag ohne eindeutigen Standort kann nicht zugestellt werden. Beim Einzeltag
war das im Prototyp gar nicht angebbar — und das ist der häufigste Fall.

### Ä-3 Pausenaufsichten auch bei mehrtägigen Anträgen
Im Prototyp erscheint das Feld nur beim Einzeltag. Bei einer dreitägigen Abwesenheit sind
aber ebenso Aufsichten betroffen — und eine nicht übergebene Pausenaufsicht ist ein
Aufsichtsproblem, kein Organisationsdetail.

### Ä-4 Hinweis und Längenbegrenzung bei den Freitext-Begründungen
Das Feld „Bitte Grund angeben" bei *Persönliche Gründe* und *Sonstiges* **bleibt ein
Pflichtfeld** — die Schulleitung muss entscheiden können, und dafür braucht sie den Anlass.

Ergänzt wird nur:
* ein Hinweis am Feld: *„Ein Stichwort genügt. Bitte keine Angaben zu Gesundheit,
  Diagnosen oder Erkrankungen Angehöriger."*
* eine Längenbegrenzung (Vorschlag: 200 Zeichen), die zur Kürze anhält.

*Warum nicht mehr:* Auf Papier war dieses Feld unkritisch. In einer Datenbank ist es die
Stelle, an der über Jahre Trauerfälle und familiäre Umstände zusammenlaufen — also
besondere Kategorien nach Art. 9 DSGVO. Den Grund ganz wegzulassen wäre aber falsch: Die
Schulleitung entscheidet über den Antrag und muss dafür wissen, worum es geht. Der
wirksame Schutz liegt deshalb nicht im Weglassen, sondern in zwei anderen Festlegungen,
die ohnehin gelten:

* **Sichtbarkeit:** Der Grund ist ausschließlich für die antragstellende Person und die
  Schulleitung sichtbar. Die Stundenplanung sieht ihn nie — weder in der Liste noch in
  der E-Mail.
* **Löschfrist:** Der Vorgang wird nach Ablauf gelöscht (Dokument 03), nicht dauerhaft
  archiviert.

**Positiv hervorzuheben:** *Arztbesuch* ist im Bestand bereits richtig gelöst — eigene
Auswahl, kein Detailfeld, keine Diagnose. Genau so bleibt es.

### Ä-5 Pflichtfeldprüfung auch auf dem Server
Der Prototyp prüft nur im Browser. Das genügt für einen Entwurf, nicht für den Betrieb:
Browserprüfungen lassen sich umgehen, und ein unvollständiger Datensatz in der Datenbank
ist später nicht mehr zu reparieren. Jede Prüfung wird serverseitig wiederholt.

---

## Zur Entscheidung

* **F-6.1** Mehrtägige Anträge gelten als **ganztägig** — es gibt kein Stundenfeld im
  Zeitraum-Zweig. Sonderfälle („Montag ab der 3. Stunde bis Mittwoch") wären zwei Anträge
  oder eine Anmerkung.
  *Empfehlung: so belassen.* Der Fall ist selten, und ein Stundenfeld über mehrere Tage
  ist missverständlich — es wäre unklar, ob es für jeden Tag oder nur für den ersten gilt.

* **F-6.2** Soll es ein freies Feld **„Anmerkungen"** am Ende geben?
  *Empfehlung: ja, optional.* Es fängt genau die Sonderfälle auf, für die sonst ein
  weiteres Formularfeld nötig wäre, und bleibt sichtbar auf die Entscheidungsebene begrenzt.

---

## Antragsart 2 — Unterrichtsgang / Veranstaltung

*Wird im nächsten Arbeitsschritt entworfen. Ein Formular dafür existiert im Bestand nicht.*
