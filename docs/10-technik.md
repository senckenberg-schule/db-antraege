# 10 — Technische Umsetzung

Erst jetzt, nach sieben fachlichen Schritten, lässt sich sinnvoll über Technik reden. Die
Entscheidungen aus [00-entscheidungen.md](00-entscheidungen.md) grenzen das Feld bereits
stark ein.

---

## 1. Was wir jetzt über das System wissen

| Merkmal | Wert | Bedeutung für die Technik |
|---|---|---|
| Benutzer insgesamt | ein Kollegium (Lehrkräfte + Vorbereitungsdienst) | klein |
| Benutzer mit besonderen Rechten | **vier** — Schulleitung, Stellvertretung, zwei Stundenplanungen | sehr überschaubares Rechtemodell |
| Antragsarten | **zwei**, gleiches Gerüst, drei abweichende Felder | ein Formularmechanismus, zwei Konfigurationen |
| Zustände | **sieben**, keine Nebenwege, keine automatischen Übergänge | einfacher Workflow, keine Workflow-Engine nötig |
| Rollen mit eingeschränkter Sicht | nur noch Standortbindung der Stundenplanung | einfache Berechtigungslogik |
| Menge | einzelne Vorgänge pro Tag | Leistungsfragen spielen keine Rolle |
| Schnittstellen in Stufe 1 | **nur** Anmeldung und E-Mail-Versand | keine Kopplung an Fremdsysteme nötig |
| Betrieb | eine Person, nebenher, mit KI-Unterstützung | **das bestimmende Kriterium** |

**Der Umfang ist klein.** Das ist keine Nebenbemerkung: Es schließt aus, dass eine
aufwändige Lösung angemessen wäre, und es macht eine überschaubare tragfähig.

---

## 2. Die Anmeldung ist der Angelpunkt

Alles andere lässt sich später ändern. Die Anmeldung nicht — an ihr hängt die gesamte
Berechtigungslogik: wer welchen Antrag sieht, wer entscheiden darf, wessen Name unter
einem Antrag steht.

Im Prototyp gibt es sie nicht; der Name ist ein freies Textfeld. Damit kann jeder unter
jedem Namen einen Antrag stellen, und die Schulleitung sieht dem Antrag nicht an, ob er
echt ist. Für einen Entwurf ist das in Ordnung — für ein Verfahren, in dem
Dienstbefreiungen genehmigt werden, nicht.

### Die drei Wege, in der Reihenfolge ihrer Eignung

**1. Anmeldung über ein vorhandenes dienstliches Konto (bevorzugt)**
Schulportal Hessen, Microsoft 365, IServ oder ein anderer Verzeichnisdienst — was immer an
der Schule bereits existiert und von allen genutzt wird.

*Vorteile:* kein zweites Passwort, das jemand vergisst; beim Ausscheiden einer Person
schließt sich der Zugang von selbst; **keine eigene Passwortdatenbank**, die zum
Angriffsziel werden könnte. Für den nebenher laufenden Betrieb ist das der entscheidende
Punkt — die aufwändigste Daueraufgabe entfällt vollständig.

**2. Anmeldelink an die dienstliche E-Mail-Adresse**
Adresse eingeben, einmalig gültigen Link erhalten, anklicken. Kein Passwort.

*Wann sinnvoll:* wenn es kein zentrales Anmeldeverfahren gibt. Es gibt nichts zu vergessen,
nichts zurückzusetzen und keine Passwörter zu speichern. Die Sicherheit hängt am
dienstlichen Postfach — aber das gilt für jedes „Passwort vergessen" ebenso.

*Bedingungen:* Link nur an dienstliche Adressen, einmalig verwendbar, kurze Gültigkeit
(etwa 15 Minuten).

**3. Eigene Konten mit Passwort (nur als letzter Ausweg)**
*Warum ungern:* Jedes vergessene Passwort landet bei der Person, die das System nebenher
betreibt. Passwörter werden wiederverwendet. Ausgeschiedene Konten bleiben offen, wenn sie
niemand schließt. Und es entsteht eine Passwortdatenbank, die es sonst nicht gäbe.

*Wenn es nicht anders geht:* Zwei-Faktor-Authentifizierung für die vier Konten mit
besonderen Rechten ist dann keine Empfehlung mehr, sondern Voraussetzung.

---

## 3. Kriterien für die Auswahl

Aktualisiert gegenüber [04-anforderungskatalog.md](04-anforderungskatalog.md) um das,
was wir inzwischen wissen.

| # | Kriterium | Warum es entscheidet |
|---|---|---|
| 1 | **Wartbar durch eine zweite Person** | Das System hängt an einer Person (E-2.4). Standardtechnologie und gute Dokumentation schlagen jede elegante Lösung. Langweilig ist hier ein Qualitätsmerkmal |
| 2 | **Verarbeitung in der EU, AV-Vertrag verfügbar** | Beschäftigtendaten. Scheidet viele naheliegende Werkzeuge sofort aus — deshalb **zuerst** prüfen, nicht zuletzt |
| 3 | **Anmeldung an vorhandene Konten anbindbar** | Siehe Abschnitt 2 |
| 4 | **Automatische Löschung nach Frist** | Tragende Datenschutzmaßnahme (E-7.1). Ohne Automatik unterbleibt sie |
| 5 | **Berechtigungen serverseitig, nicht nur in der Oberfläche** | Ausblenden ist kein Schutz |
| 6 | **Bedienbar auf dem Smartphone** | Anträge entstehen im Lehrerzimmer und auf dem Flur, nicht am Schreibtisch |
| 7 | **Datenexport in offenem Format** | Kein Einschluss bei einem Anbieter; Wechsel muss möglich bleiben |

**Was ausdrücklich nicht zählt:** Leistungsfähigkeit, Skalierbarkeit, Modernität der
Technik. Bei einzelnen Vorgängen pro Tag ist jede ernsthafte Lösung schnell genug.

---

## 4. Offene Auskünfte

Ohne diese drei Angaben lässt sich keine Empfehlung aussprechen:

* **F-8.1** Welches zentrale Anmeldeverfahren steht an der Schule zur Verfügung?
  Schulportal Hessen, Microsoft 365, IServ, ein eigener Verzeichnisdienst — oder nichts
  Zentrales?
* **F-8.2** Welche Hosting-Möglichkeiten bestehen? Angebot des Schulträgers oder des
  Landes, ein eigener Server an der Schule, ein gemieteter Server — oder ist das offen?
* **F-8.3** Welches Vertretungsplanprogramm ist im Einsatz (Untis/WebUntis, DAVINCI,
  anderes)? Für Stufe 1 nicht nötig, aber es zeigt, in welcher Umgebung das System später
  steht.

---

## 5. Auswertung der Auskünfte

### 5.1 Anmeldung: Schulportal Hessen — vielversprechend, aber zu prüfen

Das Schulportal Hessen ist die naheliegende Wahl: Es ist an der Schule eingeführt, alle
Lehrkräfte haben dort ein Konto, und es ist als Landesangebot datenschutzrechtlich bereits
bewertet. Damit wären Kriterium 3 und ein guter Teil von Kriterium 2 auf einen Schlag
erfüllt.

**Was ungeprüft ist:** ob das Schulportal eine Anmeldung **für externe Anwendungen**
anbietet. Ein Portal zu haben heißt nicht automatisch, dass sich andere Programme dagegen
anmelden können — dafür braucht es eine dafür vorgesehene Schnittstelle
(OpenID Connect / OAuth 2 oder vergleichbar).

**Konkret zu klären** — beim Schulportal-Support oder der zuständigen Stelle des Landes:

1. Können sich externe Anwendungen gegen das Schulportal anmelden lassen, und über welches
   Verfahren?
2. Falls ja: Wer beantragt den Zugang, und ist das für eine schuleigene Anwendung
   überhaupt vorgesehen?
3. Welche Angaben liefert die Anmeldung mit — Name, dienstliche E-Mail, Rolle,
   Standortzugehörigkeit?

**Die dritte Frage ist die wichtigere:** Liefert die Anmeldung auch den **Stammstandort**
und eine **Rollenangabe**, ersparen wir uns eine eigene Benutzerverwaltung fast vollständig.
Tut sie es nicht, brauchen wir eine kleine eigene Liste, wer Schulleitung und wer
Stundenplanung ist — kein großer Aufwand, aber eine Pflegeaufgabe mehr.

**Falls es nicht geht:** Weg 2 aus Abschnitt 2 — Anmeldelink an die dienstliche Adresse.
Das Verfahren ist so einfach, dass es kein Rückschritt ist.

### 5.2 Hosting: Nextcloud ist kein Ort für diese Anwendung

> **Wichtige Klarstellung.** Eine „Wolke" auf Nextcloud-Basis — auch die IServ-Wolke — ist
> ein **Dateispeicher**. Sie kann Dokumente ablegen, teilen und versionieren. Sie kann
> **keine eigenständige Webanwendung mit Datenbank ausführen**.

Dieses System braucht laufenden Programmcode, eine Datenbank, Sitzungsverwaltung,
Mailversand und einen zeitgesteuerten Löschlauf. Nichts davon leistet ein Dateispeicher.
Ein Antragssystem „in der Wolke abzulegen" wäre bestenfalls eine Sammlung von Formularen
in Dateiform — also genau der Zustand, den wir ablösen wollen.

**Zu klären ist deshalb, was an der Schule tatsächlich vorhanden ist:**

| Möglichkeit | Bedeutung |
|---|---|
| **IServ als vollständige Schulplattform** | Dann gibt es dort auch eine Anmeldung (IServ unterstützt gängige Verfahren) — eine **ernsthafte Alternative zum Schulportal**, ggf. sogar Betriebsmöglichkeiten. Lohnt die Prüfung |
| **Nur eine Dateiablage auf Nextcloud-Basis** | Für dieses Vorhaben nicht nutzbar, weder zur Anmeldung noch zum Betrieb |

### 5.3 Empfehlung zum Hosting, solange die Frage offen ist

In dieser Reihenfolge prüfen:

| Rang | Möglichkeit | Vorteil | Nachteil |
|---|---|---|---|
| **1** | Angebot des **Schulträgers** oder des **Landes** | Vertragliches und Betrieb geregelt, Datenschutzprüfung meist vorhanden, kein Wartungsaufwand für die Schule | Muss erfragt werden; Wartezeit |
| **2** | **Gemieteter Server in Deutschland** mit Auftragsverarbeitungsvertrag | Günstig, volle Kontrolle, schnell verfügbar | **Sie sind dann der Betreiber**: Updates, Sicherung, Wiederherstellung, Sicherheitsmeldungen — dauerhaft, nicht einmalig |
| **3** | Server an der Schule | Daten bleiben im Haus | Ausfallsicherheit, Sicherung und Erreichbarkeit von außen sind ohne IT-Betreuung schwer zu gewährleisten |

**Zu Rang 2 eine Warnung, die zum Kernkriterium gehört:** Einen Server zu mieten ist
leicht; ihn über Jahre gepflegt zu halten, ist die eigentliche Aufgabe. Wenn es dazu kommt,
sollte von Anfang an eine zweite Person eingewiesen sein und die Einrichtung dokumentiert
werden — sonst entsteht genau die Abhängigkeit, die in E-2.4 als Risiko benannt ist.

### 5.4 Untis: eine kleine Festlegung mit täglichem Nutzen

Im Einsatz ist **Untis**. Für Stufe 1 bleibt die Übergabe manuell (E-2.2) — die
Stundenplanung liest den Vorgang und trägt ihn im Programm ein.

**Daraus folgt eine Abstimmung, die wenig kostet und täglich hilft:** Die fünf
Begründungskategorien des Formulars — *Fortbildung · Dienstliche Gründe · Arztbesuch ·
Persönliche Gründe · Sonstiges* — sollten mit den **Absenzgründen in Untis** abgeglichen
werden.

Stimmen sie überein, kann die Stundenplanung die Angabe **unverändert übernehmen**, statt
sie bei jedem Vorgang zu übersetzen. Das war schließlich die Begründung dafür, dass die
Stundenplanung den Grund überhaupt sieht (E-6.4) — dann sollte er auch in der Form
vorliegen, in der er gebraucht wird.

→ **F-8.4** Welche Absenzgründe sind in Untis hinterlegt? Weichen sie ab, passen wir die
Auswahlliste des Formulars an — nicht umgekehrt.

Eine spätere automatische Übergabe an Untis bleibt möglich und ist Stufe 3. Sie sollte den
Beginn nicht aufhalten: Sie ist erfahrungsgemäß der aufwändigste Teil und darf den Nutzen
der übrigen Funktionen nicht verzögern.

---

## 6. Geprüft und verworfen: VIDIS als Anmeldung

**Frage:** Ließe sich eine VIDIS-Anmeldung selbst bauen?

**Antwort: technisch ja, fachlich nein.** VIDIS löst das umgekehrte Problem.

### Was VIDIS ist

VIDIS („Vernetzte Identitäten für Schulen", betrieben vom FWU) ist ein **Vermittler**
zwischen den Identitätssystemen der Länder — Landesportale, IServ, Schullogin und andere —
und **Anbietern digitaler Bildungsangebote**. Der Zweck: Ein Anbieter kann eine Anmeldung
ermöglichen, **ohne personenbezogene Daten der Schülerinnen, Schüler und Lehrkräfte zu
erhalten**. Die Daten bleiben beim Identitätssystem der Schule bzw. des Landes.

Technisch ist es ein OpenID-Connect-Verfahren. Einen OIDC-Client zu bauen ist
Standardarbeit — daran scheitert es nicht.

### Der Grund, warum es hier nicht passt

**VIDIS übermittelt bewusst keinen Namen und keine E-Mail-Adresse.** Ein Dienstanbieter
erhält üblicherweise nur:

| Übermittelt | Nicht übermittelt |
|---|---|
| ein sicheres **Pseudonym**, das der Anbieter nicht auflösen kann | Name |
| die **Rolle** (Lehrkraft oder Schülerin/Schüler) | E-Mail-Adresse |
| die **Schulzugehörigkeit** | alles Weitere |

Für ein Lernangebot ist das genau richtig: Der Anbieter muss nicht wissen, wer übt.

**Unser System braucht das Gegenteil.** Es muss zwingend wissen, **wer** den Antrag stellt:

* Der Name steht auf dem Antrag und ist die Grundlage der Entscheidung.
* Die Stundenplanung muss wissen, **wer** fehlt — sonst kann sie nichts planen.
* Benachrichtigungen brauchen eine E-Mail-Adresse.

Mit einem Pseudonym müssten wir zusätzlich eine eigene Liste führen, die Pseudonyme mit
Namen und dienstlichen Adressen verbindet — also **genau die Benutzerverwaltung, die die
Anmeldung ersparen sollte**, nur mit einem Zwischenschritt mehr.

Hinzu kommt: Die Rollenangabe unterscheidet Lehrkraft und Lernende. Sie unterscheidet
**nicht** Schulleitung von Stundenplanung. Diese vier Zuordnungen müssten wir ohnehin
selbst pflegen — das gilt allerdings für jede Lösung und wiegt nicht schwer.

### Und die Zulassung

Der Teilnahmeprozess richtet sich an **Anbieter von Bildungsangeboten für den schulischen
Kontext**. Vorausgesetzt werden unter anderem ein eigener Anmeldebereich, eine
Webanwendung, die Anbindbarkeit als OpenID-Connect-Client, ein Vertragsverhältnis sowie
eine **fertig programmierte** Anwendung zu Beginn des Verfahrens.

Ob ein **schulinternes Verwaltungsverfahren einer einzelnen Schule** darunter fällt, ist
zweifelhaft — es ist kein Bildungsangebot im Sinne des Programms. Nachfragen kostet nichts,
aber darauf planen sollte man nicht. Selbst wenn die Zulassung gelänge, bliebe der
inhaltliche Einwand oben bestehen, und der ist der schwerwiegendere.

### Die bessere Richtung

**VIDIS steht *vor* genau den Systemen, die wir brauchen** — Schulportal Hessen, IServ.
Statt den Vermittler anzusprechen, der Daten absichtlich zurückhält, gehen wir direkt an
die Quelle: mehr Attribute, ein Zwischenschritt weniger, kein Zulassungsverfahren.

**Es bleibt also bei Abschnitt 5.1:** zuerst klären, ob sich das Schulportal Hessen oder
IServ unmittelbar als Anmeldung nutzen lässt. Der Anmeldelink an die dienstliche Adresse
bleibt der tragfähige Rückfallweg.

*Quellen: [Teilnahmeprozess für Anbieter](https://www.vidis.schule/teilnahmeprozess/),
[Whitepaper zur Anbindung an VIDIS für Service Provider](https://www.vidis.schule/wp-content/uploads/sites/10/2024/08/Erweiterte-Inbetriebnahmephase-Whitepaper-zur-Anbindung-an-VIDIS-fuer-Service-Provider-v60-20240813_112511.pdf),
[Was ist VIDIS? — Schullogin-Dokumentation](https://docs.schullogin.de/98-Hilfestellungen/0003-VIDIS-Allgemein/Index.html),
[VIDIS – schulisches ID-Management (Sachsen-Anhalt)](https://ozg.sachsen-anhalt.de/fileadmin/Bibliothek/Schulung/Praesentationen_TF_Konferenz_Bildung/VIDIS_-_schulisches_ID-Management.pdf)*

---

## 7. Anmeldung: Entwurf „ohne Anmeldung" und was daraus folgt

**Vorstellung des Auftraggebers:** Kein Anmeldeverfahren. Der Link wird intern im
Schulportal hinterlegt. Die antragstellende Person gibt ihre E-Mail-Adresse an und erhält
eine Bestätigungsmail; darin ein Link, um zu melden, dass sie den Antrag **nicht** gestellt
hat.

### 7.1 Ein Link im Schulportal schützt die Anwendung nicht

Das ist der Punkt, an dem der Entwurf nicht aufgeht. Ein Link, der im Schulportal steht,
führt zu einer Adresse im Internet. Wer diese Adresse kennt oder errät, ruft sie
**unmittelbar** auf — ohne je das Schulportal gesehen zu haben, von jedem Gerät aus.

**„Hinter dem Portal verlinkt" ist nicht dasselbe wie „hinter dem Portal geschützt."**
Das Portal reicht keinen Schutz an die verlinkte Anwendung weiter. Es ist eine Bequemlichkeit
für das Kollegium, keine Zugangssperre. Adressen verbreiten sich zudem: über den Verlauf
des Browsers, über Lesezeichen, über weitergeleitete Mails.

### 7.2 Zwei Fragen, die auseinandergehalten werden müssen

| | Ohne Anmeldung machbar? |
|---|---|
| **Einen Antrag stellen** | Ja — mit der E-Mail-Bestätigung als Nachweis (7.3) |
| **Anträge lesen und entscheiden** | **Nein** |

Die zweite ist die kritische. Ohne jede Zugangsprüfung wären die Seiten der Schulleitung
und die Vorgangsansichten **für jeden im Internet erreichbar** — einschließlich der
Begründungen, der Anhänge und der Entscheidungskommentare des gesamten Kollegiums.

Ein unter falschem Namen gestellter Antrag ist ärgerlich. Ein offen im Netz stehender
Bestand von Dienstbefreiungsanträgen wäre ein Datenschutzvorfall mit Meldepflicht.

**Für die vier Personen mit besonderen Rechten ist eine Zugangsprüfung daher nicht
verhandelbar.** Das Gute: Sie erfordert weder Passwörter noch eine Benutzerverwaltung
(7.4).

### 7.3 Besser: Bestätigungslink statt Widerspruchslink

Die Idee mit der E-Mail ist richtig — sie lässt sich mit demselben Aufwand deutlich
wirksamer bauen, wenn man sie umdreht:

| | Widerspruchslink („Das war ich nicht") | **Bestätigungslink** („Antrag bestätigen") |
|---|---|---|
| Antrag erreicht die Schulleitung | sofort | erst nach dem Klick |
| Fälschung unter fremdem Namen | wird **nachträglich** entdeckt, wenn jemand die Mail liest und reagiert | **nicht möglich** — es bräuchte Zugriff auf das fremde Postfach |
| Aufwand für die antragstellende Person | kein Klick | **ein Klick** |
| Aufwand in der Umsetzung | gleich | gleich |

**Empfehlung: Bestätigungslink.** Er verhindert den Fehler, statt ihn zu reparieren.
Der Unterschied ist an einer Schule nicht theoretisch — ein Antrag im Namen einer Lehrkraft
ist ein naheliegender Streich, und der Widerspruchsweg funktioniert nur, wenn die
betroffene Person die Mail rechtzeitig liest.

Ablauf:

1. Formular ausfüllen, dienstliche E-Mail-Adresse angeben, absenden
2. Antrag liegt im Zustand *unbestätigt* — **niemand sonst sieht ihn**
3. Mail mit Bestätigungslink (einmalig gültig, 24 Stunden)
4. Nach dem Klick: Antrag gilt als gestellt, Schulleitung wird benachrichtigt
5. Unbestätigte Anträge werden nach 24 Stunden automatisch gelöscht

*Nebeneffekt:* Ein Tippfehler in der Adresse fällt sofort auf — die Bestätigung kommt nicht
an, der Antrag geht nicht raus. Beim Widerspruchsverfahren liefe der Antrag mit falscher
Adresse weiter, und die Rückmeldungen erreichten niemanden.

### 7.4 Dieselbe Mechanik ergibt die Anmeldung für die vier Konten

Der Bestätigungslink **ist** bereits ein Anmeldeverfahren — nur an einen einzelnen Vorgang
gebunden statt an eine Sitzung. Für Schulleitung, Stellvertretung und die beiden
Stundenplanungen wird derselbe Mechanismus einmal weiterverwendet:

```
Anmeldung
Dienstliche E-Mail-Adresse:  [ ____________________ ]     [ Link anfordern ]

→ Link kommt per Mail, einmalig gültig, 15 Minuten
→ Klick öffnet eine Sitzung (Vorschlag: 12 Stunden)
```

* **Kein Passwort.** Nichts zu vergessen, nichts zurückzusetzen, nichts zu speichern.
* **Keine Benutzerverwaltung.** Es genügt eine Liste von **vier** Adressen in der
  Konfiguration, die festlegt, wer Schulleitung und wer Stundenplanung ist. Kein
  Registrierungsverfahren, keine Kontoverwaltung.
* **Kein fremder Dienst**, kein Zulassungsverfahren, keine Abhängigkeit vom Schulportal.
* **Derselbe Code** wie beim Bestätigungslink — der Aufwand fällt ohnehin an.

Damit ist der Wunsch „ohne Anmeldung" fachlich erfüllt: Für das Kollegium gibt es keine,
und für die vier Konten entsteht keine Verwaltungsaufgabe.

### 7.5 Ohne Anmeldung ebenfalls nötig

| Maßnahme | Grund |
|---|---|
| **Nur dienstliche Adressen zulassen** (Prüfung auf die Schuldomäne) | Verhindert Anträge von außerhalb und begrenzt den Missbrauch eines offen erreichbaren Formulars |
| **Begrenzung der Absendeversuche** je Adresse und je Aufrufer | Ein offen erreichbares Formular mit Mailversand wird sonst zum Werkzeug für Massenmails |
| **Vorgangslinks als lange Zufallszeichenfolge** | Der Link ist der Nachweis — er darf nicht erratbar oder hochzählbar sein |
| Kein Verzeichnis, keine Suche ohne Sitzung | Ein gültiger Link darf nur den **einen** Vorgang öffnen |
| Anhänge nur über geprüfte Auslieferung | Siehe E-6.7 |

### 7.6 Was ohne Anmeldung entfällt

Ehrlich benannt:

* **Keine Übersicht „Meine Anträge".** Ohne Sitzung kann das System niemanden wiedererkennen.
  Wer seinen Antrag ansehen will, braucht den Link aus der Mail. Die Mail wird damit zum
  Aufbewahrungsort — wer sie löscht, kommt an seinen Vorgang nicht mehr heran.
* **Keine Stornierung ohne Link.** Die Stornierung (E-4.3) läuft über denselben Link.
  Geht er verloren, muss die Schulleitung stornieren.
* **Der Name bleibt ein Eingabefeld.** Die Bestätigung weist die **E-Mail-Adresse** nach,
  nicht die Person. Wer Zugriff auf ein fremdes dienstliches Postfach hat, kann weiterhin
  in fremdem Namen handeln — das ist deutlich schwerer als ein Tippen ins Namensfeld, aber
  kein Ausschluss.

*Anmerkung:* Käme später doch eine Anmeldung über Schulportal oder IServ hinzu, entfielen
diese drei Einschränkungen — und die Mechanik aus 7.3 bliebe unverändert nutzbar. Die
Entscheidung verbaut nichts.
