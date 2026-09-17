# 11 — Hosting: konkrete Möglichkeiten

> Preise sind **Größenordnungen** und vor einer Entscheidung beim Anbieter zu prüfen.
> Die Auswahl beschränkt sich auf Anbieter mit **Serverstandort Deutschland** und
> verfügbarem **Auftragsverarbeitungsvertrag** — beides ist für Beschäftigtendaten
> nicht verhandelbar.

---

## 1. Die eigentliche Entscheidung: gemanagt oder selbst verwaltet

Alles andere ist nachrangig gegenüber dieser einen Frage.

| | **Root-Server / VPS** | **Managed Hosting** |
|---|---|---|
| Wer pflegt Betriebssystem und Sicherheitsupdates | **Sie** | der Anbieter |
| Wer richtet Firewall, Webserver, Datenbank, TLS ein | **Sie** | weitgehend vorhanden |
| Wer sorgt für Sicherungen | **Sie** | im Angebot enthalten |
| Wer reagiert auf eine Sicherheitslücke im System | **Sie**, zeitnah | der Anbieter |
| Kosten | ~4–10 €/Monat | ~10–30 €/Monat |
| Freiheit | vollständig | eingeschränkt |

**Empfehlung für dieses Vorhaben: Managed Hosting.**

Die Begründung steht schon in E-2.4: Das System wird von **einer Person nebenher** betreut.
Ein Root-Server ist dabei keine Ersparnis, sondern eine Daueraufgabe — Sicherheitsupdates
kommen nicht in den Ferien, sondern wenn sie kommen. Ein seit acht Monaten ungepatchter
Server mit den Dienstbefreiungsanträgen des Kollegiums ist ein schlechteres Ergebnis als
zehn Euro mehr im Monat.

Die Preisdifferenz beträgt etwa **150 € im Jahr**. Gemessen an dem, was ein
Datenschutzvorfall an Arbeit und Vertrauen kostet, ist das keine ernsthafte Größe.

---

## 2. Zuerst fragen — kostet nichts außer zwei Wochen

Bevor irgendetwas gemietet wird, sollten diese drei Stellen gefragt werden. Wenn eine
davon etwas anbietet, sind Vertrag, Betrieb und Datenschutzprüfung meist bereits geregelt.

| Wen | Was fragen |
|---|---|
| **Schulträger** (Landkreis Limburg-Weilburg, Schulverwaltungs- bzw. IT-Amt) | Gibt es eine Möglichkeit, eine schuleigene Webanwendung zu betreiben? Besteht ein Rahmenvertrag mit einem Hoster? |
| **Medienzentrum des Landkreises** | Werden Schulen bei eigenen digitalen Werkzeugen unterstützt? Gibt es dort Serverkapazität? |
| **IServ-Betreuung der Schule** (falls IServ als Plattform vorhanden) | Lässt sich eine eigene Anwendung dort betreiben oder anbinden? |

**Realistische Einschätzung:** Die Wahrscheinlichkeit ist nicht hoch — Schulträger
betreiben selten fremde Anwendungen. Aber die Frage kostet zwei E-Mails, und eine Zusage
würde Ihnen dauerhaft die gesamte Betriebslast abnehmen. Das ist den Versuch wert.

**Wichtig:** Diese Anfrage gehört ohnehin zur Beteiligung (Dokument 09). Wer später fragt,
warum ein Verfahren der Schule auf einem privat gemieteten Server läuft, soll die Antwort
bekommen: „Wir haben zuerst beim Schulträger angefragt."

---

## 3. Konkrete Anbieter

### 3.1 Managed Hosting — empfohlen

| Anbieter | Standort | Größenordnung | Besonderheit |
|---|---|---|---|
| **Uberspace** | Mainz | ab ca. 5–10 €/Monat (Preis selbst wählbar) | Sehr flexibel für ein gemanagtes Angebot: PHP, Python und Node.js laufen, eigene Hintergrundprozesse und zeitgesteuerte Aufgaben sind möglich, Datenbank inklusive. Technisch orientierte Dokumentation, sehr gute Erfahrungen bei kleinen Projekten. **Für dieses Vorhaben die naheliegendste Wahl** |
| **Mittwald** | Espelkamp | ca. 15–30 €/Monat | Mehr Komfort und ein Support, der bei Problemen tatsächlich hilft. Oberfläche statt Kommandozeile. Sinnvoll, wenn Sie sich möglichst wenig mit Betrieb befassen wollen |
| **IONOS** | Karlsruhe / Montabaur | ca. 5–20 €/Monat | Großer Anbieter, breites Angebot, sehr unterschiedliche Tarife — genau prüfen, welche Laufzeitumgebungen und welche Datenbank enthalten sind |

### 3.2 Root-Server / VPS — nur mit dauerhafter Betreuung

| Anbieter | Standort | Größenordnung |
|---|---|---|
| **Hetzner** | Nürnberg, Falkenstein | ab ca. 4 €/Monat |
| **netcup** | Nürnberg | ab ca. 3–6 €/Monat |

Beide sind technisch ausgezeichnet und preislich kaum zu schlagen. **Sie sind für dieses
Vorhaben nur dann die richtige Wahl, wenn mindestens zwei Personen dauerhaft bereit sind,
den Server zu pflegen** — nicht einmalig einzurichten, sondern über Jahre aktuell zu halten.

### 3.3 Server an der Schule — nicht empfohlen

Erreichbarkeit von außen, unterbrechungsfreie Stromversorgung, Sicherungen an einem
zweiten Ort, Erreichbarkeit in den Ferien: Das ist ohne IT-Betreuung an der Schule nicht
verlässlich zu leisten. Für ein Verfahren, das im laufenden Schuljahr funktionieren muss,
ist das zu wenig.

---

## 4. Was die Hosting-Wahl über die Technik mitentscheidet

Diese beiden Fragen hängen zusammen, deshalb hier der Hinweis:

Auf gemanagten Angeboten läuft **PHP** praktisch überall und ohne Einrichtung.
Python und Node.js laufen dort ebenfalls, aber nicht bei jedem Anbieter gleich
reibungslos.

Für dieses Vorhaben spricht einiges für PHP — nicht aus Begeisterung, sondern aus den
Gründen, die in Kriterium 1 stehen: Es läuft überall, es ist umfassend dokumentiert, und
die Wahrscheinlichkeit, dass später eine zweite Person damit zurechtkommt, ist höher als
bei jeder anderen Wahl. **Langweilig ist hier ein Qualitätsmerkmal.**

Das ist keine Festlegung — die Sprachwahl folgt in einem eigenen Schritt. Aber wer
Uberspace oder Mittwald wählt, hat mit PHP den geringsten Widerstand.

---

## 5. E-Mail-Versand: der übersehene Teil

Das System verschickt Bestätigungen, Anmeldelinks und Benachrichtigungen. **Mail, die im
Spam-Ordner landet, ist dasselbe wie keine Mail** — und bei einem Bestätigungslink,
ohne den kein Antrag zustande kommt, wäre das ein Totalausfall.

| Weg | Bewertung |
|---|---|
| Über den **Mailserver des Hosters** mit eigener Domain, korrekt eingerichteten SPF- und DKIM-Einträgen | **Empfohlen.** Bei allen genannten Anbietern enthalten oder günstig dazu |
| Direkter Versand vom Server ohne diese Einträge | Landet zuverlässig im Spam. Nicht brauchbar |
| Über einen Versanddienstleister | Zusätzlicher Auftragsverarbeitungsvertrag, für diese Mengen unnötig |

**Zu testen ist der Versand ausdrücklich an `@schule.hessen.de`** — ob Mails dort ankommen,
ist die entscheidende Frage und lässt sich vorab ausprobieren.

---

## 6. Prüfliste für jeden Anbieter

- [ ] Serverstandort **Deutschland** (nicht nur „EU", nicht nur Firmensitz)
- [ ] **Auftragsverarbeitungsvertrag** nach Art. 28 DSGVO verfügbar — vor Vertragsschluss anfordern
- [ ] Keine Unterauftragsverarbeiter außerhalb der EU
- [ ] **TLS-Zertifikat** enthalten (Let's Encrypt genügt)
- [ ] **Datenbank** enthalten (MariaDB/MySQL oder PostgreSQL)
- [ ] **Zeitgesteuerte Aufgaben** möglich — wird für den automatischen Löschlauf (E-7.1) gebraucht
- [ ] **Sicherungen** enthalten, und: lässt sich eine Wiederherstellung testen?
- [ ] Mailversand mit eigener Domain, SPF und DKIM
- [ ] Zugang für eine **zweite Person** einrichtbar

Der Punkt „zeitgesteuerte Aufgaben" wird leicht übersehen und ist hier wesentlich: Ohne ihn
läuft die Löschautomatik nicht — und die ist nach E-7.1 die tragende
Datenschutzmaßnahme des Systems.

---

## 7. Empfehlung

1. **Jetzt:** Schulträger und Medienzentrum anfragen (Abschnitt 2). Zwei E-Mails,
   zwei Wochen Wartezeit, parallel zur Beteiligung von Personalrat und Datenschutz.
2. **Wenn nichts zurückkommt:** Managed Hosting, voraussichtlich **Uberspace** —
   preislich unbedenklich, technisch ausreichend flexibel für Datenbank, Hintergrundaufgaben
   und Mailversand, und der Betrieb des Systems bleibt Aufgabe des Anbieters.
3. **Vor der Entscheidung:** Prüfliste aus Abschnitt 6 durchgehen und den
   Auftragsverarbeitungsvertrag **vorab** anfordern. Wer ihn erst nach Vertragsschluss
   sucht, verhandelt aus der schwächeren Position.
4. **Nicht:** Root-Server ohne zweite Person, und kein Server an der Schule.

### Kosten im Überblick

| Posten | Jährlich |
|---|---|
| Managed Hosting | ca. 60–360 € |
| Domain | ca. 10–20 € |
| **Summe** | **ca. 70–380 €** |

Ob die Schule das aus eigenen Mitteln trägt oder der Schulträger, ist mit der Schulleitung
zu klären — **nicht privat vorstrecken**. Ein Verfahren der Schule sollte auch auf einem
Vertrag der Schule laufen, nicht auf einem persönlichen. Das betrifft die Verantwortlichkeit
nach Art. 28 DSGVO ebenso wie die Frage, was geschieht, wenn Sie die Schule verlassen.

---

## 8. Der vorhandene IONOS-Vertrag — geprüft

Im IONOS-Konto der Schule bestehen (Stand der Vertragsübersicht):

| Leistung | Seit | Bemerkung |
|---|---|---|
| **IONOS MyWebsite Basic** | 2017 | enthält die Inklusiv-Domain **`senckenberg-schule.de`** |
| **IONOS MyWebsite Creator** | 2022 | |
| IONOS marketingRadar | | für dieses Vorhaben ohne Bedeutung |

### 8.1 MyWebsite ist kein Webhosting

**Ergebnis: Auf den vorhandenen Verträgen lässt sich die Anwendung nicht betreiben.**

MyWebsite ist ein **Homepage-Baukasten**: Seiten werden in einem Editor zusammengestellt
und von IONOS ausgeliefert. Es gibt

* **kein PHP** und keine andere Laufzeitumgebung für eigenen Programmcode,
* **keine Datenbank**,
* **keinen Dateizugriff** (kein SSH, kein FTP für eigene Anwendungen),
* **keine zeitgesteuerten Aufgaben** — und damit keinen Löschlauf.

Das ist kein kleinerer Tarif desselben Produkts, sondern ein anderes Produkt. Ein Upgrade
innerhalb von MyWebsite hilft nicht; es braucht in jedem Fall etwas Zusätzliches.

*Damit entfällt auch das Argument aus dem vorigen Abschnitt, ein bestehender Vertrag sei
mehr wert als ein neuer:* Es wird ohnehin ein neues Produkt gebraucht. Die Anbieterwahl ist
also wieder offen und nach Eignung zu entscheiden.

### 8.2 Was bleibt: die Domain

`senckenberg-schule.de` ist eine Inklusiv-Domain des MyWebsite-Basic-Vertrags. Sie ist
nutzbar, **unabhängig davon, wo die Anwendung läuft**:

```
www.senckenberg-schule.de        → bleibt bei MyWebsite (die Schulhomepage)
antrag.senckenberg-schule.de     → zeigt per DNS-Eintrag auf den Ort der Anwendung
```

Eine Unteradresse lässt sich einrichten und auf einen beliebigen Server verweisen. Die
Schulhomepage bleibt davon unberührt.

**Zu prüfen:** Ob die DNS-Verwaltung im MyWebsite-Basic-Vertrag zugänglich ist und eigene
Unteradressen mit freiem Ziel zulässt. Bei Baukasten-Produkten ist das gelegentlich
eingeschränkt. Im IONOS-Konto unter *Domains → DNS-Einstellungen* nachsehen; im Zweifel
beim Support fragen.

*Falls die DNS-Verwaltung eingeschränkt ist:* Die Domain lässt sich auch zu einem anderen
Anbieter umziehen oder dort nur die Verwaltung übernehmen. Das ist aber Aufwand — deshalb
erst prüfen, ob es nötig ist.

### 8.3 Zwei Wege

| | **A — IONOS Webhosting dazubuchen** | **B — Anderer Hoster, Domain bleibt bei IONOS** |
|---|---|---|
| Was | Zusätzliches Produkt neben MyWebsite | z. B. Uberspace; Unteradresse zeigt per DNS dorthin |
| Vorteil | **Ein Anbieter, eine Rechnung, eine Stelle im Störungsfall** | Mehr Flexibilität, oft bessere Unterstützung für eigene Anwendungen |
| Zu prüfen | Enthält der Tarif **Datenbank und zeitgesteuerte Aufgaben**? Serverstandort Deutschland? | DNS-Verwaltung bei IONOS möglich? Auftragsverarbeitungsvertrag beim zweiten Anbieter |
| Kosten | ca. 5–15 €/Monat zusätzlich | ca. 5–10 €/Monat zusätzlich |

**Empfehlung: Weg A prüfen, Weg B als Ausweichlösung.**

Der Vorteil eines Anbieters ist für ein nebenher betriebenes System real: eine
Zugangsverwaltung, eine Rechnung, eine Telefonnummer. **Er gilt aber nur, wenn der
IONOS-Webhosting-Tarif zeitgesteuerte Aufgaben enthält.** Ohne die läuft der automatische
Löschlauf nicht — und der ist nach E-7.1 die tragende Datenschutzmaßnahme. Dieser Punkt
entscheidet, nicht der Preis.

### 8.4 Ohnehin zu klären

* **Auftragsverarbeitungsvertrag** nach Art. 28 DSGVO — bei IONOS verfügbar, vor dem
  Echtbetrieb abschließen und ablegen.
* **Serverstandort Deutschland** ausdrücklich wählen und dokumentieren. „Deutscher
  Anbieter" genügt nicht; es zählt der Ort der Verarbeitung.
* **Vertragsinhaber:** Läuft das Konto auf die Schule? Bei einer Domain
  `senckenberg-schule.de` liegt das nahe, ist aber zu bestätigen. Ein Verfahren der Schule
  sollte nicht auf einem privaten Vertrag laufen.
* **Randbemerkung:** Zwei MyWebsite-Verträge (Basic und Creator) nebeneinander können ein
  Überrest aus einem Produktwechsel sein. Das betrifft dieses Vorhaben nicht, lohnt aber
  einen Blick — womöglich zahlt die Schule doppelt.

### 8.5 Absender der E-Mails

Unabhängig vom gewählten Weg sollten die Bestätigungs- und Anmeldemails von einer Adresse
der Schuldomäne kommen, etwa `antrag@senckenberg-schule.de`.

*Grund:* Eine Mail mit Anmeldelink von einer fremden Absenderadresse weckt zu Recht
Misstrauen — und die Zustellung an `@schule.hessen.de` ist von einer bekannten Domäne mit
korrekten SPF- und DKIM-Einträgen deutlich wahrscheinlicher. **Vorab testen.**

