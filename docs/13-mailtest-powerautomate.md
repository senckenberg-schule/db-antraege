# 13 — Mailversand in Power Automate: Test und Einstellungen

Ziel: herausfinden, **warum** die Mails nicht ankamen, und es abstellen. Der Test ist
bewusst der kleinstmögliche — ein Flow mit einer einzigen Aktion. Alles andere kommt erst,
wenn die Zustellung steht.

---

## Vorbemerkung: Power Automate hat kaum Einstellungen zur Zustellbarkeit

Das ist wichtig für die Erwartung. An der Zustellung ändert im Flow selbst fast nichts —
entscheidend sind drei Dinge:

1. **Welche Aktion** verwendet wird (`E-Mail senden (V2)` vom Connector *Office 365 Outlook*),
2. **welches Konto** die Verbindung herstellt — das bestimmt den **Absender**,
3. ob die **Absenderdomäne** zum Versand über Microsoft berechtigt ist (SPF, DKIM).

Punkt 3 liegt außerhalb von Power Automate. Der Test klärt, ob es daran liegt.

---

## Schritt 1 — Testflow anlegen

1. [make.powerautomate.com](https://make.powerautomate.com) öffnen, mit dem **Schulkonto**
   anmelden.
2. Oben rechts prüfen, in welcher **Umgebung** Sie sind — es sollte die der Schule sein,
   nicht eine private.
3. Links **Erstellen** → **Sofortiger Cloud Flow**.
4. Name: `Mailtest`. Auslöser: **Flow manuell auslösen**. → **Erstellen**.

## Schritt 2 — Die richtige Aktion wählen

5. **+ Neuer Schritt**.
6. Ins Suchfeld `Office 365 Outlook` eingeben.
7. Aus der Liste **„E-Mail senden (V2)"** wählen.

> **Wichtig:** Es darf **nicht** die Aktion *„E-Mail-Benachrichtigung senden"* sein
> (Connector *Mail*) und auch nicht *„Genehmigung starten"*. Beide versenden von einer
> Microsoft-Adresse und werden von strengen Filtern verworfen. Sie erkennen die richtige
> Aktion am Symbol und am Connector-Namen **Office 365 Outlook**.

## Schritt 3 — Verbindung prüfen: wer ist der Absender?

8. Beim ersten Mal fragt Power Automate nach einer Verbindung. Im Drei-Punkte-Menü der
   Aktion → **Meine Verbindungen** steht, **mit welchem Konto** verbunden ist.
9. **Dieses Konto ist der Absender.** Notieren Sie die Adresse — sie ist der Schlüssel zur
   Diagnose.

Ist dort ein privates oder fremdes Konto hinterlegt, auf das Schulkonto wechseln.

## Schritt 4 — Erste Testmail: an sich selbst im Mandanten

10. **An:** die eigene Adresse **im Mandanten** (dieselbe wie in Schritt 9).
11. **Betreff:** `Test 1 intern`
12. **Text:** ein Satz, **ohne Link und ohne Anhang**.
13. Speichern, dann **Testen** → **Manuell** → **Testen** → **Flow ausführen**.

**Diese Mail muss ankommen.** Sie verlässt den Mandanten nicht und unterliegt keiner
externen Prüfung.

> Das Postfach erreichen Sie über [outlook.office.com](https://outlook.office.com) mit dem
> Schulkonto — auch wenn Sie es sonst nie benutzen. **Genau dort liegen auch die
> Unzustellbarkeitsnachrichten der damaligen Versuche.** Wahrscheinlich haben Sie sie nie
> gesehen.

| Ergebnis | Bedeutung |
|---|---|
| Kommt an | Der Versandweg funktioniert. Weiter mit Schritt 5 |
| Kommt **nicht** an | Kein Zustellungsproblem, sondern ein Rechte- oder Postfachproblem. Hat das Konto überhaupt ein Exchange-Postfach? |

## Schritt 5 — Zweite Testmail: an die Dienstadresse

14. Im selben Flow die Empfängeradresse ändern auf Ihre **`@schule.hessen.de`**-Adresse.
15. Betreff: `Test 2 dienstlich`. Erneut ausführen.
16. **Zehn Minuten warten**, dann **auch den Spam-Ordner prüfen**.

## Schritt 6 — Dritte Testmail: an eine externe Adresse

17. Empfänger auf eine Gmail-Adresse ändern, Betreff `Test 3 extern`, ausführen.

*(Nur zur Diagnose. Für den Betrieb sind private Adressen ausgeschlossen — siehe E-8.6.)*

## Schritt 7 — Auswerten

| Test 1 (intern) | Test 2 (Land) | Test 3 (Gmail) | Diagnose |
|---|---|---|---|
| ✅ | ✅ | ✅ | **Gelöst.** Damals wurde vermutlich doch eine andere Aktion verwendet |
| ✅ | ❌ | ❌ | **Absenderdomäne nicht berechtigt** — SPF/DKIM fehlen. Weiter unten |
| ✅ | ❌ | ✅ | Der Landesdienst filtert gezielt. Eine Freigabe dort erfragen, oder auf Teams ausweichen |
| ✅ | ✅ | ❌ | Für uns unerheblich — private Adressen sind ohnehin ausgeschlossen |
| ❌ | ❌ | ❌ | Postfach- oder Rechteproblem, kein Zustellungsproblem |

**Der wahrscheinlichste Fall ist Zeile 2** — er erklärt genau Ihre damalige Beobachtung.

## Schritt 8 — Die Unzustellbarkeitsnachricht lesen

Bei jedem ❌: im Postfach aus Schritt 9 nachsehen. Der Ausführungsverlauf in Power Automate
zeigt nur, dass **abgeschickt** wurde — die Abweisung kommt Sekunden bis Minuten später per
Mail zurück.

| Text in der Nachricht | Bedeutung |
|---|---|
| `SPF validation failed`, `550 5.7.23`, `does not designate ... as permitted sender` | SPF fehlt für die Absenderdomäne |
| `DMARC`, `policy violation` | DMARC weist ab, weil SPF und DKIM fehlen |
| `550 5.7.1`, `blocked`, `spam` ohne weitere Angabe | Ruf des Absenders; meist ebenfalls SPF/DKIM |
| Keine Nachricht, Mail liegt im Spam-Ordner | Nicht abgewiesen, nur einsortiert — SPF/DKIM beheben das ebenfalls |

---

## Was bei Zeile 2 zu tun ist

### A. Absenderadresse ansehen (aus Schritt 9)

* Endet sie auf **`…onmicrosoft.com`** → **das ist die Ursache.** Solche Absender werden
  von strengen Filtern grundsätzlich abgewiesen. Behebung: im Mandanten eine eigene
  Domäne einrichten und als Standardadresse setzen. Das macht die Mandantenverwaltung.
* Lautet sie auf eine **eigene Domäne** → weiter mit B.

### B. SPF prüfen und ergänzen

Der TXT-Eintrag der Absenderdomäne muss Microsoft erlauben:

```
v=spf1 include:spf.protection.outlook.com -all
```

Ist bereits ein SPF-Eintrag vorhanden (etwa für einen anderen Mailanbieter), wird der
`include` **ergänzt**, nicht ersetzt:

```
v=spf1 include:<bisheriger> include:spf.protection.outlook.com -all
```

> **Es darf nur einen SPF-Eintrag je Domäne geben.** Zwei getrennte TXT-Einträge machen
> beide ungültig — das ist der häufigste Fehler dabei.

Prüfen lässt sich der vorhandene Eintrag mit jedem öffentlichen SPF-Prüfwerkzeug oder
über die DNS-Verwaltung der Domäne.

### C. DKIM einschalten

**Für eigene Domänen ist DKIM in Exchange Online nicht automatisch aktiv.**

1. [security.microsoft.com](https://security.microsoft.com) → *E-Mail und Zusammenarbeit*
   → *Richtlinien und Regeln* → *Bedrohungsrichtlinien* → **DKIM**.
2. Domäne auswählen → **Aktivieren**.
3. Microsoft zeigt **zwei CNAME-Einträge** an (`selector1._domainkey` und
   `selector2._domainkey`). Diese in der DNS-Verwaltung der Domäne anlegen.
4. Zurück ins Portal, erneut **Aktivieren**. Nach der DNS-Verteilung — Minuten bis
   Stunden — greift es.

### D. DMARC setzen

TXT-Eintrag auf `_dmarc.<domäne>`, zunächst zurückhaltend:

```
v=DMARC1; p=none; rua=mailto:<eine Adresse für Berichte>
```

Erst wenn SPF und DKIM nachweislich greifen, auf `p=quarantine` und später `p=reject`
schärfen. **Nicht sofort scharf stellen** — sonst blockieren Sie den eigenen Versand.

### E. Erneut testen

Schritte 4 bis 7 wiederholen. DNS-Änderungen brauchen Zeit; wenn es nicht sofort wirkt,
nach ein paar Stunden noch einmal.

---

## Wer das tun kann

| Aufgabe | Wer |
|---|---|
| Testflow bauen, Tests 1–3 | Sie |
| Unzustellbarkeitsnachricht lesen | Sie |
| Absenderdomäne im Mandanten ändern | Mandantenverwaltung |
| DKIM im Sicherheitsportal aktivieren | Mandantenverwaltung |
| SPF-, DKIM- und DMARC-Einträge im DNS anlegen | wer die DNS-Verwaltung der Domäne hat |

**Die ersten beiden Zeilen reichen für die Diagnose.** Erst wenn feststeht, woran es liegt,
brauchen Sie jemanden mit weitergehenden Rechten — und dann mit einer konkreten Bitte statt
mit einer vagen Frage. Das erhöht die Aussicht auf Erfolg erheblich.

---

## Und wenn es nicht gelingt

Dann bleibt der Ablauf **innerhalb des Mandanten**: Genehmigungen und Hinweise über Teams,
Arbeitsvorrat als Liste. Test 1 zeigt ja, dass intern alles funktioniert.

Der Mailversand nach außen ist Komfort — **kein Bestandteil des Verfahrens** (E-8.5).
