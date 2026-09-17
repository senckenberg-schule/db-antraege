# 12 — Umsetzung in Microsoft 365

An der Schule besteht ein **Microsoft-365-Abonnement**. Damit entsteht eine Möglichkeit,
die alle bisherigen Techniküberlegungen überholt — nicht als Webhosting, sondern als
Umsetzung **ohne eigenen Programmcode**.

> **Wichtig vorweg:** Das gesamte Fachkonzept bleibt gültig. Rollen, Antragsarten,
> Standortlogik, Statusmodell, Benachrichtigungsmatrix, Sichtbarkeit und Löschfristen
> sind unabhängig von der Technik entschieden. Nur der Weg der Umsetzung ändert sich.

---

## 1. Der Aufbau

| Baustein | Aufgabe |
|---|---|
| **Power Apps** (oder Microsoft Forms) | Das Antragsformular |
| **SharePoint-Liste** | Die Datenhaltung — ein Eintrag je Antrag |
| **Power Automate** | Benachrichtigungen, Genehmigungsablauf, Löschlauf |
| **Microsoft-Konto** | Die Anmeldung — bereits vorhanden |

Der Genehmigungsablauf ist in Power Automate eine vorgefertigte Funktion („Genehmigungen"):
Sie verschickt eine Anfrage, stellt *Genehmigen* und *Ablehnen* zur Auswahl, nimmt einen
**Kommentar** auf und schreibt die Antwort zurück in die Liste. Genau unser Ablauf.

**Lizenzlage:** Genehmigungen laufen über einen **Standardconnector**, und Cloudflows mit
Standardconnectoren sind in den Microsoft-365-Lizenzen enthalten. Ein Zusatzabonnement ist
nach den öffentlichen Angaben nicht erforderlich — **im eigenen Mandanten zu bestätigen**
(siehe Abschnitt 5).

---

## 2. Was dadurch gelöst ist — und zwar richtig

**Die Anmeldung.** Das war das schwerste offene Problem, und es verschwindet vollständig.
Jede Lehrkraft ist im Mandanten angemeldet; das System kennt sie, ohne dass jemand einen
Namen eintippt.

Damit werden **sechs Entscheidungen gegenstandslos**, die alle nur Behelfe für die fehlende
Anmeldung waren:

| Entfällt | War nötig, weil |
|---|---|
| **E-8.1** Keine Anmeldung für das Kollegium | jetzt gibt es eine, und eine echte |
| **E-8.2** Bestätigungslink gegen Fälschungen | niemand kann mehr in fremdem Namen handeln |
| **E-8.3** Vier Passwortkonten | die Anmeldung besteht bereits |
| **E-8.4** Domänenprüfung, Adressregeln | nur Angehörige des Mandanten kommen hinein |
| Begrenzung der Absendeversuche | kein offen erreichbares Formular mehr |
| Zufällige Vorgangslinks als Nachweis | Berechtigung statt geheimer Adresse |

**Der Name ist kein Eingabefeld mehr.** Er kommt aus der Anmeldung — damit auch die
Angabe, **wer** entschieden hat, zuverlässig statt behauptet.

**Kein Server.** Keine Sicherheitsupdates, keine Sicherungen, keine TLS-Einrichtung, keine
Wiederherstellungstests. Das größte Risiko des Vorhabens — ein von einer Person nebenher
gepflegter Server (E-2.4) — entfällt.

**Keine zusätzlichen Kosten.** Innerhalb des bestehenden Abonnements.

**Nachfolgefähigkeit.** Ein Power-Automate-Flow ist anklickbar und von Microsoft
dokumentiert; jede Person mit Zugriff auf den Mandanten kann hineinsehen. Das ist
vermutlich übernehmbarer als eine selbst geschriebene PHP-Anwendung — vorausgesetzt, die
Flows bleiben überschaubar und werden beschriftet.

---

## 3. Was dabei verloren geht

Ehrlich benannt, damit die Entscheidung tragfähig ist.

| Verlust | Bedeutung |
|---|---|
| **Selbstlernende Vorschläge für Lerngruppen** (E-3.5) | Microsoft Forms kann das nicht. In Power Apps wäre eine Auswahl aus früheren Einträgen möglich, aber aufwändig. **Wahrscheinlich entfällt es** — das Feld bleibt Freitext, nur ohne Vorschläge |
| **Entweder-oder-Prüfung bei „Fortbildung"** (E-6.5) | In Forms nicht abbildbar; in Power Apps machbar. **Spricht für Power Apps statt Forms** |
| **Feinsteuerung der Sichtbarkeit** | SharePoint kennt Berechtigungen je **Eintrag**, nicht je **Feld**. Durch E-6.4 (Stundenplanung sieht alles) ist das kaum noch ein Problem — aber „erst ab Genehmigung" und „nur eigener Standort" brauchen eine bewusste Gestaltung, etwa über getrennte Listen oder gefilterte Ansichten mit Berechtigungen |
| **Gestalterische Freiheit** | Das Formular sieht aus wie Microsoft. Der vertraute Wortlaut Ihres Prototyps lässt sich übernehmen, das Erscheinungsbild nicht |
| **Unabhängigkeit** | Verlässt die Schule irgendwann Microsoft 365, ist das System weg. Bei einer eigenen Anwendung wäre nur der Hoster zu wechseln |

---

## 4. Der Punkt, an dem es sich entscheidet: Datenschutz

**Microsoft ist ein US-Unternehmen** — dieselbe Frage, die Supabase ausgeschlossen hat.

**Der Unterschied:** Die Schule **nutzt Microsoft 365 bereits**. Es besteht ein Vertrag,
ein Auftragsverarbeitungsvertrag und mit einiger Wahrscheinlichkeit eine
datenschutzrechtliche Bewertung. Der Begründungsaufwand ist also **bereits getragen** —
nicht neu zu erbringen.

**Was das nicht heißt:** Der Einsatz von Microsoft 365 an Schulen ist in Deutschland
umstritten, mehrere Länder haben ihn eingeschränkt oder mit Bedingungen versehen. Und eine
allgemeine Freigabe für Kommunikation und Dateien bedeutet nicht automatisch eine Freigabe
für **Personalvorgänge mit Abwesenheitsgründen**.

**Diese Frage gehört ausdrücklich gestellt**, nicht vorausgesetzt:

> „Wir nutzen Microsoft 365 bereits. Dürfen wir darin ein Antragsverfahren für
> Dienstbefreiungen abbilden — also Beschäftigtendaten einschließlich der Angabe des
> Anlasses (Arztbesuch, persönliche Gründe) in einer SharePoint-Liste speichern und über
> Power Automate verarbeiten? Die Daten werden nach 12 Monaten automatisch gelöscht;
> Zugriff haben Schulleitung, Stellvertretung und die beiden Stundenplanungen."

*Falls die Antwort nein lautet*, bleibt der Weg über eigenes Webhosting (Dokument 11)
bestehen — das Fachkonzept trägt beides. Deshalb ist die Frage **vor** dem Bauen zu
stellen, nicht danach.

**Zu klären ist außerdem der Speicherort:** Microsoft bietet für europäische Kunden eine
Verarbeitung innerhalb der EU an. Für welche Dienste und in welcher Ausprägung das im
Mandanten der Schule gilt, ist dort nachzusehen und zu dokumentieren.

---

## 5. Prüfliste

Mit der Person klären, die den Mandanten verwaltet:

- [ ] Welche Lizenzen haben die Lehrkräfte (A1, A3, A5)?
- [ ] Sind **Power Automate** und **Power Apps** im Mandanten freigeschaltet, oder sind sie
      administrativ gesperrt? *(Häufiger Stolperstein — oft aus Vorsicht deaktiviert)*
- [ ] Ist der **Genehmigungsconnector** nutzbar?
- [ ] Lassen sich **SharePoint-Listen** anlegen, und wer darf das?
- [ ] Ist ein **geplanter Flow** (für den Löschlauf) möglich?
- [ ] Wo liegen die Daten des Mandanten — EU?
- [ ] Liegt der Auftragsverarbeitungsvertrag vor, und deckt er diese Verwendung?
- [ ] Wer außer Ihnen hat Zugriff auf den Mandanten — für die Nachfolge (Q-03)?

---

## 6. Empfehlung

**Diesen Weg zuerst prüfen, vor jeder weiteren Zeile Code.**

Er löst das schwerste Problem des Vorhabens — die Anmeldung — richtig statt behelfsmäßig,
kostet nichts zusätzlich, nimmt den Serverbetrieb vollständig weg und ist
wahrscheinlich besser übernehmbar. Das wiegt die geringere Gestaltungsfreiheit auf.

**Reihenfolge:**

1. **Mandanten prüfen** (Abschnitt 5) — eine Frage an die M365-Betreuung.
2. **Datenschutzfrage stellen** (Abschnitt 4) — zusammen mit dem Anschreiben aus
   [09-vorlagen-beteiligung.md](09-vorlagen-beteiligung.md), und ausdrücklich für diesen
   Zweck.
3. **Bei grünem Licht:** mit Antragsart 1 anfangen — SharePoint-Liste, Power App,
   Genehmigungsflow. Ein überschaubarer erster Aufbau.
4. **Bei Ablehnung:** zurück zu Dokument 11, eigenes Webhosting, PHP.

**Was in keinem Fall verloren ist:** die acht Schritte der Fachplanung. Rollen, Ablauf,
Statusmodell, Benachrichtigungen, Formularfelder, Löschfristen und die Unterlagen für
Personalrat und Datenschutz gelten unverändert — gleich in welcher Technik.

*Quellen zur Lizenz- und Funktionslage:*
[Erste Schritte mit Power Automate-Genehmigungen](https://learn.microsoft.com/de-de/power-automate/get-started-approvals) ·
[Power Automate Lizenzierung FAQ](https://learn.microsoft.com/de-de/power-platform/admin/power-automate-licensing/faqs) ·
[Microsoft 365 Education Lizenzen](https://learn.microsoft.com/de-de/microsoft-365/education/guide/0-start/all-license)

---

## 7. Erfahrung aus einem früheren Flow: E-Mails kamen nicht an

Ein früher an der Schule gebauter Power-Automate-Flow verschickte E-Mails, die **bei
`@schule.hessen.de` nicht zuverlässig ankamen** und auch bei anderen Adressen blockiert
wurden. Das ist ein belastbarer Einwand — und er hat eine benennbare Ursache.

### 7.1 Power Automate hat mehrere Versandwege mit sehr unterschiedlichem Verhalten

| Aktion im Flow | Absender | Zustellung |
|---|---|---|
| **„E-Mail senden (V2)"** — Connector *Office 365 Outlook* | **das Postfach der Person, die den Flow verbunden hat** — eine echte Adresse der Schule | **gut.** Technisch eine gewöhnliche Exchange-Mail, nicht von einer normalen Mail zu unterscheiden |
| **„E-Mail-Benachrichtigung senden"** — Connector *Mail* | eine allgemeine Microsoft-Absenderadresse (`…@powerapps.com` o. ä.) | **schlecht.** Wird von strengen Filtern regelmäßig zurückgewiesen |
| **Benachrichtigungen des Genehmigungsdienstes** | Microsoft-Benachrichtigungsadresse | **schlecht**, aus demselben Grund |

**Wahrscheinliche Ursache des damaligen Problems:** Es wurde der *Mail*-Connector oder die
automatische Genehmigungs-Benachrichtigung verwendet — beide versenden von einer fremden
Microsoft-Adresse, die mit der Schuldomäne nichts zu tun hat. Ein streng eingestellter
Mailserver, und der Landesdienst dürfte streng eingestellt sein, wirft so etwas aus.

**Zu prüfen im alten Flow:** Welche Aktion wurde verwendet? Steht dort *Office 365 Outlook*
oder *Mail*? Das ist in wenigen Minuten nachzusehen und entscheidet, ob das Problem gelöst
oder grundsätzlich ist.

### 7.2 Die zweite mögliche Ursache: zwei getrennte Welten

Vermutlich sind das **zwei verschiedene Systeme**:

* das **Microsoft-365-Konto** der Schule (eigener Mandant, eigene Domäne),
* die **dienstliche Adresse** `@schule.hessen.de` beim Land.

Eine Mail aus dem Mandanten an `@schule.hessen.de` verlässt damit die eigene Organisation
und trifft auf die Filter des Landesdienstes. Selbst bei korrektem Absender ist das
störanfälliger als eine Mail innerhalb derselben Organisation.

### 7.3 Die eigentliche Lösung: den Ablauf ohne E-Mail führen

**Alle Beteiligten sind im Mandanten.** Damit braucht der interne Ablauf **gar keine
E-Mail**:

| Empfänger | Statt E-Mail |
|---|---|
| **Schulleitung, Stellvertretung** | **Teams-Nachricht mit Adaptive Card** — Antrag, *Genehmigen*, *Ablehnen*, *Rückfrage* und Kommentarfeld direkt in der Karte. Alternativ die **Genehmigungen-App in Teams**, in der alle offenen Anträge stehen |
| **Stundenplanung** | Teams-Nachricht plus die **SharePoint-Liste** als Arbeitsgrundlage — was ohnehin so entschieden war (E-5.1: „die Liste ist der Arbeitsplatz, die Mail nur ein Wecker") |
| **Antragstellende Person** | Teams-Nachricht über Eingang und Entscheidung |

**Nichts davon verlässt den Mandanten.** Kein Spamfilter, kein SPF, kein DKIM, keine
Zustellungsfrage — und datenschutzseitig sogar besser, weil keine Inhalte über
ungesicherte Transportwege laufen (Regel D-03 wird damit von selbst erfüllt).

**Das damalige Problem wäre damit nicht behoben, sondern beseitigt.**

### 7.4 Die Frage, an der es hängt

> **Nutzt das Kollegium Teams tatsächlich — oder liest es seine dienstliche Post
> ausschließlich unter `@schule.hessen.de`?**

Das ist jetzt die entscheidende Frage des ganzen Vorhabens.

| Antwort | Folge |
|---|---|
| **Teams wird genutzt** | Der Weg über Microsoft 365 ist klar die beste Lösung: echte Anmeldung, kein Server, keine Kosten, **und kein Zustellungsproblem** |
| **Teams wird nicht genutzt, Post nur beim Land** | Benachrichtigungen müssen per E-Mail an `@schule.hessen.de` — dann ist der Versandweg aus 7.1 zwingend richtig zu wählen und **vorab zu testen**. Gelingt das nicht, spricht es gegen Microsoft 365 und für eigenes Hosting |

**Der Test ist klein:** Einen Flow mit *einer* Aktion bauen — „E-Mail senden (V2)" über
*Office 365 Outlook* — und an die eigene `@schule.hessen.de`-Adresse schicken. Kommt sie
an, ist die Frage beantwortet. Das ist eine Viertelstunde Arbeit und entscheidet über die
gesamte technische Richtung.

### 7.5 Und dieselbe Frage gilt für den anderen Weg

Falls die Entscheidung auf eigenes Hosting fällt, besteht das Zustellungsproblem
**genauso** — dann sogar ohne den Ausweg über Teams. Ein eigener Webserver, der Mails an
`@schule.hessen.de` schickt, muss korrekte SPF- und DKIM-Einträge haben und wird bei
strengen Filtern ebenfalls auffällig.

**Die Zustellbarkeit an `@schule.hessen.de` ist damit kein Microsoft-Problem, sondern die
zentrale technische Voraussetzung des ganzen Vorhabens** — bei jedem Weg. Sie gehört
getestet, bevor irgendetwas gebaut wird.
