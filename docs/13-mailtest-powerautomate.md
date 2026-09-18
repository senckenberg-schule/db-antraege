# 13 — Mailversand in Power Automate: vorhandenen Flow überarbeiten

Ziel: die Maileinstellungen im **bestehenden Flow** so ändern, dass die Nachrichten
ankommen — ohne einen separaten Testflow.

> **Erwartung vorweg:** Power Automate hat genau **drei** Stellschrauben, die auf die
> Zustellung wirken: **Aktion**, **Verbindung** und **Inhalt**. Sind die in Ordnung und es
> kommt weiterhin nichts an, liegt die Ursache außerhalb des Flows (SPF/DKIM, siehe
> unten). Dann hilft keine weitere Einstellung.

---

## Teil 1 — Am Flow ändern

### 1. Flow öffnen
[make.powerautomate.com](https://make.powerautomate.com) mit dem Schulkonto →
**Meine Flows** → den Flow auswählen → **Bearbeiten**.

### 2. Prüfen, welche Aktion tatsächlich versendet

Die Sendeaktion aufklappen und auf den **Connector-Namen** achten — nicht auf den Titel
der Aktion, den kann man umbenannt haben.

| Was dort steht | Bewertung |
|---|---|
| **Office 365 Outlook — E-Mail senden (V2)** | richtig |
| **Mail — E-Mail-Benachrichtigung senden (V3)** | **ersetzen**, versendet von einer Microsoft-Adresse |
| **Genehmigungen — Genehmigung starten** | Die Benachrichtigung kommt vom Genehmigungsdienst, nicht aus Ihrem Postfach. **Zusätzlich** eine eigene Mail per Outlook-Aktion senden |

**Falls zu ersetzen:** Aktion löschen, **+ Neuer Schritt**, `Office 365 Outlook` suchen,
**E-Mail senden (V2)** einfügen, Felder neu füllen. Die dynamischen Inhalte aus dem
Formular stehen unverändert zur Verfügung.

### 3. Verbindung prüfen — das ist der Absender

Im **Drei-Punkte-Menü** der Sendeaktion → **Meine Verbindungen**.

Dort steht das Konto, mit dem versendet wird. **Diese Adresse ist der Absender Ihrer
Mails.** Notieren Sie sie.

* Steht dort ein **privates oder fremdes Konto** → auf das Schulkonto umstellen
  (**Verbindung hinzufügen**).
* Steht dort das Schulkonto → in Ordnung, weiter.

### 4. „Von (Senden als)" kontrollieren

In der Aktion auf **Erweiterte Optionen anzeigen**.

Das Feld **Von (Senden als)** muss **leer** sein — es sei denn, das Konto hat für die
eingetragene Adresse ausdrücklich die Berechtigung „Senden als". Ein Eintrag ohne diese
Berechtigung lässt den Versand entweder scheitern oder die Mail unglaubwürdig erscheinen.

**Im Zweifel: Feld leeren.**

### 5. Empfänger auf ein kontrollierbares Ziel setzen

Solange geprüft wird, **nicht** an die Adresse aus dem Formular senden, sondern fest an
die eigene **`@schule.hessen.de`**-Adresse. So wissen Sie, wo die Mail landen sollte.

Die dynamische Empfängeradresse kommt zurück, sobald es funktioniert.

### 6. Inhalt entschärfen

Für den ersten Durchgang so schlicht wie möglich — Inhalt beeinflusst die Spam-Bewertung
spürbar:

| Feld | Für den Versuch |
|---|---|
| **Betreff** | kurz und sachlich, z. B. `Antrag eingegangen`. Keine Großbuchstaben, keine Ausrufezeichen, kein „Wichtig" |
| **Text** | zwei Sätze reiner Text. **Keine Links**, keine Bilder, keine Tabellen |
| **Wichtigkeit** | auf *Normal* (unter den erweiterten Optionen) |
| **Anlagen** | keine |

Links sind der häufigste Auslöser. Kommt die schlichte Mail an, fügen Sie den Link im
zweiten Durchgang wieder ein — dann wissen Sie, woran es lag.

### 7. Speichern und auslösen — ohne neues Formular

**Ausführungsverlauf** des Flows öffnen, einen früheren Lauf anklicken und oben
**Erneut übermitteln** wählen. Der Flow läuft mit denselben Formulardaten noch einmal.

Damit brauchen Sie weder ein neues Formular noch einen Testflow.

### 8. Ergebnis ansehen — an der richtigen Stelle

Der Ausführungsverlauf zeigt nur, dass **abgeschickt** wurde. Eine Abweisung kommt Sekunden
bis Minuten später **als Mail in das Postfach aus Schritt 3** zurück.

Dieses Postfach öffnen Sie über [outlook.office.com](https://outlook.office.com) mit dem
Schulkonto. **Dort liegen auch die Unzustellbarkeitsnachrichten der damaligen Versuche** —
sehr wahrscheinlich ungelesen.

---

## Teil 2 — Auswerten

| Beobachtung | Bedeutung | Nächster Schritt |
|---|---|---|
| Mail kommt an | Es lag an Aktion, Verbindung oder Inhalt | Link und dynamischen Empfänger schrittweise zurückbauen, nach jedem Schritt prüfen |
| Mail im **Spam-Ordner** | Zustellung funktioniert, Ruf des Absenders ist schwach | SPF und DKIM (Teil 3) |
| **Unzustellbarkeitsnachricht** | Der Text nennt den Grund | Tabelle unten |
| Nichts kommt an, keine Rückmeldung | Stille Aussortierung beim Empfänger | SPF und DKIM (Teil 3) |

### Was in der Unzustellbarkeitsnachricht stehen kann

| Text | Bedeutung |
|---|---|
| `SPF validation failed`, `550 5.7.23`, `does not designate … as permitted sender` | SPF fehlt für die Absenderdomäne |
| `DMARC`, `policy violation` | DMARC weist ab, weil SPF und DKIM fehlen |
| `550 5.7.1`, `blocked`, `spam` ohne Näheres | Ruf des Absenders — meist ebenfalls SPF/DKIM |
| `5.7.60`, `not allowed to send as` | Das Feld „Von (Senden als)" aus Schritt 4 ist gesetzt, ohne dass die Berechtigung besteht |

---

## Teil 3 — Wenn es am Flow nicht liegt

### Dann liegt es an der Absenderdomäne

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
