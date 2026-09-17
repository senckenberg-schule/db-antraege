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

### 7.6 Nachtrag: es war bereits „V2" — Neubewertung

Der frühere Flow verwendete bereits **„E-Mail senden (V2)"** über den Connector
*Office 365 Outlook*, und die Zustellung scheiterte dennoch. Die Erklärung aus 7.1
greift damit nicht.

#### Wahrscheinlichere Ursache: der Absenderdomäne fehlt die Berechtigung

Beim Versand aus Exchange Online lautet der Absender auf die Domäne des Mandanten —
etwa `@senckenberg-schule.de`. Damit eine fremde Stelle diese Mail annimmt, muss die
**DNS-Konfiguration dieser Domäne** den Versand über Microsoft ausdrücklich erlauben.

Und genau da liegt bei dieser Schule ein Bruch: **Die DNS-Einträge von
`senckenberg-schule.de` liegen bei IONOS** und sind für MyWebsite und den IONOS-Mailversand
eingerichtet — nicht für Microsoft 365.

| Prüfpunkt | Was fehlen könnte | Folge |
|---|---|---|
| **SPF** (TXT-Eintrag der Domäne) | `include:spf.protection.outlook.com` fehlt, weil der Eintrag auf IONOS zeigt | Jede aus Microsoft versendete Mail **fällt bei der SPF-Prüfung durch**. Strenge Empfänger weisen sie ab |
| **DKIM** | Für **eigene Domänen ist DKIM in Exchange Online nicht automatisch aktiv** — es muss im Microsoft-Verwaltungsportal eingeschaltet und mit zwei DNS-Einträgen hinterlegt werden | Fehlende Signatur; in Verbindung mit SPF-Fehler nahezu sichere Abweisung |
| **DMARC** | Eintrag fehlt oder steht auf `reject` | Bei fehlendem SPF und DKIM wird konsequent abgewiesen |
| **Absenderdomäne** | Versand erfolgte womöglich als `…@<mandant>.onmicrosoft.com` | Solche Absender werden von strengen Filtern häufig grundsätzlich blockiert |

**Das erklärt beide Beobachtungen**: dass es bei `@schule.hessen.de` scheiterte *und* dass
auch andere Adressen die Mails blockierten. Ein SPF-Fehlschlag ist kein Problem des
Empfängers — er wirkt überall dort, wo geprüft wird.

#### Was zu beschaffen ist, bevor weiter geraten wird

**Die Unzustellbarkeitsnachricht.** Sie nennt den Grund im Klartext — etwa
`550 5.7.23 SPF validation failed`, `DMARC policy`, oder eine Einordnung als unerwünschte
Werbung. Ohne diesen Text bleibt alles Vermutung.

Zu finden im **Postfach, aus dem der Flow versendet hat** (die Verlaufsanzeige in Power
Automate zeigt nur, dass die Aktion erfolgreich *abgeschickt* wurde — die Abweisung kommt
danach und landet im Postfach).

Falls die Mails nicht abgewiesen, sondern nur **in den Spam-Ordner einsortiert** wurden,
ist die Ursache dieselbe, die Behandlung aber einfacher.

#### Diese Prüfung lohnt unabhängig vom Umsetzungsweg

Die genannten DNS-Einträge betreffen die Domäne, nicht Microsoft. **Sind sie nicht in
Ordnung, hat auch ein eigener Webserver dasselbe Problem** — er versendet dann ebenfalls
als `@senckenberg-schule.de`.

Wer sie in Ordnung bringt, verbessert damit beide Wege gleichzeitig. Es ist Arbeit an der
Domäne, nicht an der Anwendung.

---

## 8. Die Konsequenz für den Entwurf: E-Mail darf nicht tragend sein

Unabhängig davon, ob sich die Zustellung reparieren lässt, folgt aus dieser Erfahrung eine
Festlegung:

> **Das System muss auch dann vollständig benutzbar sein, wenn keine einzige E-Mail
> ankommt.**

Für die Stundenplanung war das schon entschieden (E-5.1: „die Liste ist der Arbeitsplatz,
die Mail nur ein Wecker"). Dieser Grundsatz wird nun auf **alle** Beteiligten ausgedehnt:

| Rolle | Arbeitet aus | E-Mail |
|---|---|---|
| Schulleitung, Stellvertretung | einer Übersicht offener Anträge, die sie selbst öffnen | Hinweis, kein Erfordernis |
| Stundenplanung | der Liste genehmigter Vorgänge | Hinweis, kein Erfordernis |
| Antragstellende Person | Bestätigung **auf dem Bildschirm**, mit Vorgangsnummer | Hinweis, kein Erfordernis |

### 8.1 Und damit fällt der Bestätigungslink — er muss fallen

Entscheidung **E-8.2** (Antrag wird erst durch Klick auf einen Link in der Mail gültig)
setzte **zuverlässige Zustellung voraus**. Kommt die Mail nicht an, entsteht **kein
Antrag** — der Fehler ist dann nicht ein verpasster Hinweis, sondern der Totalausfall des
Verfahrens.

**Daraus folgt eine Kette, die die technische Richtung bestimmt:**

```
E-Mail unzuverlässig
   → Bestätigungslink untauglich
   → der anmeldungsfreie Entwurf trägt nicht
   → es braucht eine echte Anmeldung
   → Microsoft 365, Schulportal oder IServ
   → mit Microsoft 365: Benachrichtigung über Teams statt E-Mail
```

**Die unzuverlässige Zustellung spricht damit nicht gegen Microsoft 365 — sie spricht
dafür.** Denn der anmeldungsfreie Entwurf war es, der E-Mail unverzichtbar machte. Eine
echte Anmeldung macht sie zum Beiwerk.

### 8.2 Die Frage wird dadurch schärfer

Nicht mehr „nutzt das Kollegium Teams?", sondern:

> **Gibt es innerhalb von Microsoft 365 einen Kanal, den die Beteiligten tatsächlich
> ansehen?** Teams, oder ein Postfach im Mandanten, das gelesen wird.

Für den Kernablauf genügen dabei **vier Personen**, nicht das ganze Kollegium: Schulleitung,
Stellvertretung und die beiden Stundenplanungen. Sie erhalten die Hinweise. Die
antragstellende Person braucht keinen Hinweis — sie füllt das Formular aus und bekommt die
Bestätigung sofort angezeigt.

**Diese vier zu fragen, ob sie Teams benutzen, ist überschaubar.** Und wenn sie es nicht
tun: Vier Personen für ein Werkzeug zu gewinnen, das die Schule schon bezahlt, ist
leichter, als die Zustellbarkeit eines Landesmailservers zu beeinflussen.

### 8.3 Weiterer Befund: auch Gmail blockte — das bestätigt die Absenderdiagnose

Die Mails des früheren Flows wurden **sowohl bei `@schule.hessen.de` als auch bei privaten
Adressen (Gmail)** blockiert.

**Das ist ein aussagekräftiger Befund.** Zwei voneinander unabhängige, unterschiedlich
betriebene Mailsysteme weisen dieselben Mails ab — dann liegt die Ursache nicht bei den
Empfängern, sondern beim **Absender**. Gmail prüft SPF, DKIM und DMARC besonders streng;
ein Absender ohne gültige Authentifizierung wird dort verlässlich einsortiert oder
abgewiesen.

Damit verdichtet sich der Verdacht aus 7.6: **Die Absenderdomäne des Mandanten ist für den
Versand über Microsoft nicht berechtigt.**

### 8.4 Das ist behebbar — und lohnt unabhängig von diesem Vorhaben

Vier Schritte, keine Programmierung:

| # | Schritt | Wo |
|---|---|---|
| 1 | **Absenderdomäne feststellen.** Lautet der Absender auf `@senckenberg-schule.de` oder auf `@<mandant>.onmicrosoft.com`? Letzteres wird von strengen Filtern grundsätzlich blockiert und muss auf die eigene Domäne umgestellt werden | Microsoft-365-Verwaltung, oder Kopfzeilen einer erhaltenen Mail |
| 2 | **SPF ergänzen:** `include:spf.protection.outlook.com` in den TXT-Eintrag der Domäne. Der IONOS-Versand kann dabei bleiben — ein SPF-Eintrag kann mehrere Absender erlauben | IONOS, DNS-Einstellungen |
| 3 | **DKIM einschalten.** In Exchange Online für eigene Domänen **nicht automatisch aktiv**: im Microsoft-Verwaltungsportal aktivieren, dann die beiden vorgegebenen CNAME-Einträge bei IONOS anlegen | Microsoft + IONOS |
| 4 | **DMARC setzen**, zunächst zurückhaltend (`p=none` mit Berichtsadresse), nach erfolgreicher Prüfung schärfen | IONOS, DNS |

**Der Aufwand liegt bei etwa einer halben Stunde**, wenn man die Anleitung neben sich hat.
Danach akzeptieren Gmail und der Landesdienst die Mails — und zwar auch alle anderen Mails
der Schuldomäne, nicht nur die des Antragssystems.

**Diese Arbeit verbessert jeden Umsetzungsweg gleichzeitig.** Ein eigener Webserver würde
ebenfalls als `@senckenberg-schule.de` versenden und stünde vor genau denselben
Anforderungen.

### 8.5 Private Adressen sind ohnehin ausgeschlossen

Unabhängig von der Zustellbarkeit: **Benachrichtigungen gehen niemals an private
Adressen.** Auch nicht an eine, die zuverlässig funktioniert.

Schon die Nachricht „Antrag DB-2026-0147 wurde genehmigt" an eine private Gmail-Adresse
wäre eine Verarbeitung von Beschäftigtendaten in einem Postfach außerhalb der Kontrolle
der Schule — und über die Zeit entstünde dort ein Abwesenheitsarchiv des Kollegiums.
Regel D-03 und das Konzept in Dokument 08 schließen das aus.

Zulässige Empfänger sind ausschließlich:
* die dienstliche Adresse `@schule.hessen.de`,
* ein Postfach im Mandanten der Schule,
* ein Kanal innerhalb des Mandanten (Teams).

**Damit ist Gmail kein Ausweichweg, sondern für dieses Vorhaben gesperrt.**

### 8.6 Die Fragen, die jetzt die Richtung entscheiden

In dieser Reihenfolge:

| # | Frage | Wenn ja | Wenn nein |
|---|---|---|---|
| 1 | **Haben alle Lehrkräfte ein Microsoft-365-Konto, das sie nutzen und dessen Anmeldung sie kennen?** | Die Anmeldung ist gelöst — der tragende Vorteil von Microsoft 365 | Dann trägt der Weg nicht. Zurück zu Schulportal, IServ oder eigenem Hosting |
| 2 | **Nutzen zumindest die vier Personen mit besonderen Rechten Teams?** | Benachrichtigungen laufen intern, kein Zustellungsproblem | Arbeitsvorrat als angepinnte Liste, ohne Hinweise |
| 3 | **Lassen sich SPF und DKIM in Ordnung bringen (8.4)?** | E-Mail wird zusätzlich nutzbar, auch an `@schule.hessen.de` | Der Ablauf bleibt vollständig innerhalb des Mandanten |

**Frage 1 ist die entscheidende.** Wird Microsoft 365 an der Schule nur von einzelnen
genutzt, während das Kollegium mit der Landesadresse arbeitet, dann ist die Anmeldung
**nicht** gelöst — und der Hauptgrund für diesen Weg fällt weg.

### 8.7 Nachtrag: das damalige Formular war anonym

Das Forms-Formular des früheren Flows war auf **„Jeder mit dem Link kann antworten"**
eingestellt.

**Zwei Folgerungen:**

1. **Die Kernfrage aus 8.6 ist damit nicht beantwortet.** Anonyme Formulare verlangen keine
   Anmeldung — der Versuch sagt also nichts darüber, ob die Lehrkräfte nutzbare
   Microsoft-365-Konten haben.
2. **Der damalige Aufbau hatte dieselbe Schwäche wie der PHP-Entwurf:** Ohne Anmeldung
   musste der Name in ein Feld getippt werden, und jeder mit dem Link konnte einen Antrag
   unter jedem Namen stellen. Das war kein Fehler — nur die Folge der anonymen Einstellung.

Die Maildiagnose bleibt davon unberührt: „E-Mail senden (V2)" versendet aus dem Postfach
der Person, die den Flow verbunden hat — also aus der Mandantendomäne. Fehlen dort SPF und
DKIM, wird die Mail bei Gmail und beim Landesdienst gleichermaßen abgewiesen.

### 8.8 Der Zehn-Minuten-Test, der die Kernfrage beantwortet

Statt die Mandantenverwaltung zu fragen, lässt sich das selbst prüfen — und zwar besser,
weil der Test nicht nur klärt, ob Konten **existieren**, sondern ob die Leute sich
tatsächlich **anmelden können**.

**Ablauf:**

1. Ein neues Formular in Microsoft Forms anlegen, eine einzige Frage genügt.
2. In den Einstellungen umstellen auf **„Nur Personen in meiner Organisation können
   antworten"** — und dort **„Namen erfassen"** aktivieren.
3. Den Link an **zwei oder drei Personen** schicken, darunter möglichst die Schulleitung
   und eine der beiden Stundenplanungen. Also an die Menschen, auf die es ankommt.
4. Fragen: *„Kannst du das aufmachen und abschicken?"*

**Auswertung:**

| Ergebnis | Bedeutung |
|---|---|
| Alle können ausfüllen, und die Antworten tragen ihre Namen | **Die Anmeldung ist gelöst.** Microsoft 365 ist der Weg: Identität aus der Anmeldung, kein Namensfeld, kein Bestätigungslink, keine Domänenprüfung, keine Hostingkosten |
| Einzelne kommen nicht hinein oder kennen ihre Anmeldung nicht | Konten sind vorhanden, aber nicht in Gebrauch. **Lösbar** — aber es ist Einführungsarbeit im Kollegium, keine technische Frage. Bei vier entscheidenden Personen überschaubar |
| Niemand kann sich anmelden | Der Weg trägt nicht. Zurück zu Schulportal, IServ oder eigenem Hosting mit dem anmeldungsfreien Entwurf |

**Dass die Antworten die Namen tragen, ist der eigentliche Prüfpunkt.** Erscheint dort
„Müller, Anna" statt „Anonym", liefert Forms genau die Identität, die dieses System
braucht — und der schwierigste Teil des ganzen Vorhabens ist damit erledigt.

Dieser Test kostet nichts, verändert nichts und ist in einer Freistunde erledigt.
**Er sollte vor jeder weiteren Technikentscheidung stehen.**


### 8.9 Richtigstellung: IONOS ist nicht beteiligt

Der IONOS-Vertrag der Schule hält **nur die Schulhomepage**. Die Annahme aus 7.6, die
Mandantendomäne von Microsoft 365 werde über IONOS verwaltet und deren SPF-Eintrag zeige
deshalb nicht auf Microsoft, ist damit **nicht belegt**.

**Der Kern der Diagnose bleibt gültig:** Zwei unabhängige Mailsysteme — Landesdienst und
Gmail — haben dieselben Mails abgewiesen. Das weist auf den Absender, nicht auf die
Empfänger. Offen ist nur, **welche Absenderdomäne** betroffen war und wo ihre
DNS-Einträge liegen.

**Das ist mit einer einzigen Angabe zu klären:** Wie lautete die Absenderadresse der
damaligen Mails? Sie steht in der Unzustellbarkeitsnachricht oder, falls eine Mail im
Spam-Ordner angekommen ist, in ihren Kopfzeilen.

* Endet sie auf **`…onmicrosoft.com`** → das ist die Ursache. Solche Absender werden von
  strengen Filtern grundsätzlich abgewiesen. Behebung: eine eigene Domäne im Mandanten
  einrichten und für sie SPF und DKIM setzen.
* Lautet sie auf eine **eigene Domäne** → für diese Domäne sind SPF und DKIM zu prüfen,
  wo auch immer ihre DNS-Einträge liegen.

---

## 9. Stand der Entscheidung

Nach allem Bisherigen bleiben **drei mögliche Endzustände**. Alle drei hängen an derselben
Frage.

| | Voraussetzung | Benachrichtigung | Kosten |
|---|---|---|---|
| **A — Microsoft 365** | Lehrkräfte haben nutzbare Konten | **Teams**, kein E-Mail-Versand nötig | keine |
| **B — Eigene Anwendung** | Zustellbarkeit an `@schule.hessen.de` in Ordnung gebracht | E-Mail | Hosting, ca. 70–380 €/Jahr |
| **C — Eigene Anwendung, ohne Benachrichtigung** | keine | keine — alle öffnen selbst eine Liste | Hosting |

**Die entscheidende Frage ist unverändert die aus 8.8:** Haben die Lehrkräfte — und vor
allem die vier Personen mit besonderen Rechten — nutzbare Microsoft-365-Konten?

* **Ja** → Weg A. Er ist kostenlos, braucht keinen Server, keine Zustellbarkeit und löst
  die Identitätsfrage richtig statt behelfsmäßig.
* **Nein** → Weg B oder C. Dann ist zu klären, ob die Zustellbarkeit herzustellen ist;
  gelingt das nicht, bleibt C.

**Weg C ist tragfähig, aber schwächer:** Das Verfahren funktioniert, nur erfährt niemand
von einem neuen Antrag, ohne nachzusehen. Bei einzelnen Anträgen pro Tag ist das
zumutbar — es entspricht dem Papierstapel auf dem Schreibtisch, nur ohne Verrutschen.
Es setzt aber die Gewohnheit voraus, täglich hineinzusehen.
