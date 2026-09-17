# 03 — Datenschutz und Informationssicherheit

> **Hinweis:** Dieses Dokument ist eine fachliche Arbeitsgrundlage, keine Rechtsberatung.
> Die genannten Rechtsgrundlagen und Paragrafen sind **vor der Umsetzung mit der
> behördlichen Datenschutzbeauftragten bzw. dem Datenschutzbeauftragten und dem Personalrat
> abzugleichen**. Die Aussagen beziehen sich auf eine öffentliche Schule in Hessen;
> maßgeblich sind DSGVO, HDSIG, HSchG samt Schul-Datenschutzverordnung sowie die
> IT-Vorgaben des Landes. Ziffern einzelner Vorschriften sind zu verifizieren.

---

## 1. Warum das hier vorne steht

In diesem System werden **Beschäftigtendaten** verarbeitet — und zwar solche, aus denen sich
Rückschlüsse auf persönliche Lebensumstände ziehen lassen. Ein Papierantrag, der auf dem
Schreibtisch der Schulleitung liegt, ist ein Einzelfall. Eine Datenbank mit drei Jahren
Anträgen aller Kolleginnen und Kollegen ist etwas kategorial anderes: Sie ist durchsuchbar,
kopierbar und auswertbar. Diese Qualitätsänderung ist der eigentliche Grund, warum
Datenschutz hier kein Formalakt ist.

Zwei Konsequenzen ziehen sich durch das gesamte Konzept:

1. **Datenvermeidung vor Datenschutz.** Ein Datum, das nicht erhoben wird, muss nicht
   geschützt, nicht gelöscht und nicht ausgekunftet werden. Deshalb: Auswahllisten statt
   Freitext beim Anlass, kein Attestupload, keine Privatanschriften.
2. **Rollentrennung auf Feldebene.** Nicht „wer darf den Vorgang sehen", sondern „wer darf
   welches Feld sehen" (siehe [02-datenmodell.md](02-datenmodell.md), Abschnitt 3).

---

## 2. Schutzbedarfsfeststellung

| Datenkategorie | Beispiele | Schutzbedarf | Begründung |
|---|---|---|---|
| Vorgangsdaten | Vorgangsnummer, Status, Zeitraum | **normal** | Organisatorische Daten |
| Abwesenheitsdaten mit Personenbezug | Wer ist wann nicht da | **hoch** | Bewegungs- und Verhaltensprofil über die Zeit |
| **Anlass der Dienstbefreiung** | Arzttermin, familiärer Anlass | **hoch** | Rückschluss auf Gesundheit und persönliche Verhältnisse; bei Freitext droht Abgleiten in Art. 9 DSGVO |
| Entscheidungen und Kommentare | Ablehnungsbegründung | **hoch** | Bewertende Aussagen über Beschäftigte |
| Schülerbezogene Daten (Art C/D) | Klassenlisten, Teilnehmerzahlen | **hoch** | Daten Minderjähriger |
| Protokolldaten | Zugriffe, Statusänderungen | **hoch** | Missbrauchspotenzial zur Verhaltenskontrolle |

**Ergebnis: Gesamtschutzbedarf HOCH.** Besondere Kategorien nach Art. 9 DSGVO werden durch
das Formulardesign **bewusst vermieden** — das ist eine Anforderung an die Umsetzung, keine
Beschreibung des Ist-Zustands.

---

## 3. Rechtsrahmen (zu verifizieren)

| Punkt | Einschätzung |
|---|---|
| **Verantwortlicher** | Die Schule, vertreten durch die Schulleitung (ggf. gemeinsam mit dem Land als Dienstherr — klären). |
| **Rechtsgrundlage Beschäftigtendaten** | Art. 6 Abs. 1 lit. c/e DSGVO i. V. m. § 23 HDSIG (Verarbeitung zu Zwecken des Beschäftigungsverhältnisses) und dem Schulrecht. **Nicht** auf Einwilligung stützen — im Beschäftigungsverhältnis ist die Freiwilligkeit zweifelhaft, und eine widerrufene Einwilligung würde den Prozess zerstören. |
| **Rechtsgrundlage Schülerdaten** | Schulrechtliche Aufgabenerfüllung (HSchG i. V. m. Schul-Datenschutzverordnung). |
| **Verzeichnis von Verarbeitungstätigkeiten** | Art. 30 DSGVO — **verpflichtend**, vor Inbetriebnahme zu erstellen. |
| **Datenschutz-Folgenabschätzung** | Art. 35 DSGVO — Schwellwertprüfung durchführen und **dokumentieren**. Argument für eine DSFA: systematische Verarbeitung von Beschäftigtendaten mit Bewertungscharakter. Argument dagegen: geringer Umfang, keine automatisierte Entscheidung. Die Prüfung selbst ist in jedem Fall Pflicht. |
| **Auftragsverarbeitung** | Art. 28 DSGVO — AV-Vertrag mit jedem Hoster/Dienstleister, einschließlich Mailversand. |
| **Personalratsbeteiligung** | **Mitbestimmungspflichtig.** Das System ist eine technische Einrichtung, die objektiv geeignet ist, Verhalten und Leistung zu überwachen (§ 74 HPVG — Ziffer prüfen). Das gilt unabhängig von der Absicht. Empfehlung: **Dienstvereinbarung** mit Zweckbindung, Auswertungsverbot, Löschfristen und Protokollierungsregeln. |
| **Betroffenenrechte** | Auskunft, Berichtigung, Löschung, Einschränkung (Art. 15–18 DSGVO) — Prozess festlegen, wer sie bearbeitet. |
| **Informationspflicht** | Art. 13 DSGVO — Datenschutzhinweis im Formular, nicht nur in einer separaten Ordnung. |

**Die Personalratsbeteiligung ist der Punkt, der Projekte dieser Art am häufigsten
verzögert.** Sie sollte nicht am Ende stehen, sondern bereits jetzt in der Konzeptphase
beginnen — mit genau diesem Dokument als Gesprächsgrundlage. Der Personalrat bekommt damit
etwas zu prüfen, statt etwas Fertiges vorgesetzt.

---

## 4. Löschkonzept

Ohne Löschfristen wird jedes solche System zum Dauerarchiv. Vorschlag zur Abstimmung mit
DSB und Personalrat:

| Datenkategorie | Aufbewahrung | Danach |
|---|---|---|
| Genehmigte/abgelehnte Anträge Art. A (Dienstbefreiung) | Ende des Schuljahres + 1 Jahr | vollständige Löschung |
| Anträge Art. B (Dienstreise) mit Kostenbezug | nach haushaltsrechtlichen Fristen (klären, i. d. R. länger) | Löschung |
| Anträge Art. C/D (Veranstaltungen) | Ende des Schuljahres + 2 Jahre | Anonymisierung (Kennzahlen bleiben, Personenbezug entfällt) |
| Entwürfe ohne Einreichung | 90 Tage | automatische Löschung |
| Kommentarverlauf | wie zugehöriger Antrag | Löschung mit dem Vorgang |
| Protokolldaten | 6–12 Monate (mit Personalrat festlegen) | automatische Löschung |
| Benutzerkonten ausgeschiedener Personen | Deaktivierung sofort, Löschung nach Ablauf aller Antragsfristen | Löschung |

**Löschung muss automatisch laufen.** Eine Frist, die jemand manuell anstoßen muss, wird
nicht eingehalten. Der Löschlauf ist zu protokollieren (Tatsache der Löschung, nicht Inhalt).

**Wichtig:** Wird eine Dienstbefreiung in die Personalakte übernommen, geschieht das im
bestehenden Verfahren außerhalb dieses Systems. Das System ist und bleibt ein
Workflow-Werkzeug mit begrenzter Aufbewahrung, keine Aktenführung.

---

## 5. Technische und organisatorische Maßnahmen

### 5.1 Anmeldung und Identität

| Anforderung | Begründung |
|---|---|
| **Single Sign-on** gegen das bestehende dienstliche Konto (Schulportal / Verzeichnisdienst) | Kein weiteres Passwort, zentrale Sperrung beim Ausscheiden, keine eigene Passwortdatenbank als Angriffsziel |
| **Zwei-Faktor-Authentifizierung mindestens für SL, SL-V, ADM** | Diese Konten sehen alle Anträge; ein kompromittiertes SL-Konto ist der Worst Case |
| Automatische Abmeldung nach Inaktivität | Gemeinschaftsrechner im Lehrerzimmer |
| Kein Login per Magic-Link auf private Adressen | Zustellweg ist nicht kontrollierbar |

### 5.2 Autorisierung
Berechtigungsprüfung **serverseitig bei jedem Zugriff**, auf Feldebene gemäß Matrix in
Dokument 02. Ausblenden in der Oberfläche allein genügt nicht — die Daten dürfen den
Server gar nicht erst verlassen.

### 5.3 Transport und Speicherung
* Ausschließlich **TLS** (HTTPS), HSTS, keine unverschlüsselten Endpunkte.
* **Verschlüsselung der Datenträger** auf Server- und Backupseite.
* Backups verschlüsselt, getrennt vom Produktivsystem, **Wiederherstellung regelmäßig testen**
  (ein ungetestetes Backup ist kein Backup).
* Anlagen nicht im Webroot ablegen, Zugriff nur über berechtigungsgeprüfte Auslieferung.

### 5.4 E-Mail — die schwächste Stelle

E-Mail ist auf dem Transportweg nicht durchgehend gesichert und landet in Postfächern, die
außerhalb der Kontrolle des Systems liegen. Deshalb gilt ohne Ausnahme:

* **Benachrichtigungen enthalten keine personenbezogenen Inhalte.** Nur Vorgangsnummer,
  Antragsart, Ereignis und Link.
* **Kein Antragsgrund, kein Kommentartext, keine Klassenliste in der E-Mail** —
  auch nicht „zur Bequemlichkeit".
* Versand ausschließlich an **dienstliche** Adressen und Rollenpostfächer.
* Mailversand über einen Dienstleister mit AV-Vertrag und EU-Verarbeitung.
* Entscheidungen werden **nicht per Link-Klick in der Mail** getroffen (kein
  „Genehmigen"-Button in der E-Mail): Ein solcher Link ist ein Berechtigungsnachweis im
  Klartext in einem unsicheren Kanal.

### 5.5 Protokollierung

Protokolliert wird: Anmeldung, Statusänderung, Entscheidung, Zugriff auf einen Vorgang,
Export, Löschlauf, Rechteänderung.

Ebenso wichtig ist die **Zweckbindung**: Protokolldaten dienen der Sicherheit und
Nachvollziehbarkeit von Systemvorgängen, **nicht** der Bewertung von Beschäftigten. Sie sind
technisch getrennt zu halten, nur für ADM und DSB zugänglich, mit eigener kurzer
Löschfrist. Diese Regel gehört in die Dienstvereinbarung, nicht nur in die Dokumentation.

### 5.6 Betrieb und Hosting

| Anforderung | Begründung |
|---|---|
| Verarbeitung **ausschließlich in der EU**, vorzugsweise Deutschland | Beschäftigten- und Schülerdaten; Drittlandtransfers vermeiden statt rechtfertigen |
| Vorrang: Angebot des Schulträgers, des Landes oder ein bereits geprüfter Schuldienstleister | Nutzt vorhandene AV-Verträge und Freigaben; verkürzt die Prüfung erheblich |
| Regelmäßige Sicherheitsupdates, benannte Zuständigkeit | Ein System ohne Pflege wird zur Schwachstelle |
| Keine Analyse-, Tracking- oder CDN-Dienste Dritter | Jede eingebundene Fremdressource ist eine Datenabfluss-Möglichkeit |
| Dokumentierte Wiederanlauf- und Ausfallplanung | Was passiert bei Ausfall zur Antragsfrist? Papier-Rückfallweg definieren |

### 5.7 Mandantentrennung der Standorte
Die Standorttrennung ist eine **Berechtigungsfrage**, keine Frage getrennter Systeme:
Ein Sekretariat des Standorts A darf Vorgänge, die ausschließlich Standort B betreffen,
nicht sehen. Das ist in der Berechtigungsprüfung abzubilden und zu testen.

---

## 6. Risiken und Gegenmaßnahmen

| Risiko | Auswirkung | Gegenmaßnahme |
|---|---|---|
| Freitextfelder füllen sich mit Gesundheitsdaten | Art.-9-Daten ohne passende Rechtsgrundlage | Auswahllisten, Hinweistext im Formular, kurze Freitextfelder, Schulung |
| Kompromittiertes SL-Konto | Vollzugriff auf alle Anträge | 2FA, Sitzungsbegrenzung, Protokollierung, Alarm bei Massenzugriff |
| Weiterleitung von Antragsdetails per Mail durch Beteiligte | Umgehung des gesamten Schutzkonzepts | Keine Details in Mails, Schulung, Prozessregel in der Dienstvereinbarung |
| System wird schleichend zur Abwesenheitsstatistik | Mitbestimmungsverstoß, Vertrauensverlust | Auswertungen technisch nur aggregiert, Auswertungsverbot in der Dienstvereinbarung |
| Vertretungsplanung sieht Antragsgründe | Unnötige Kenntnis sensibler Daten | Reduzierte Sicht auf Feldebene, serverseitig erzwungen |
| Datenwachstum ohne Löschung | Unverhältnismäßige Vorratshaltung | Automatischer Löschlauf, protokolliert |
| Ausfall kurz vor einer Antragsfrist | Prozessstillstand | Definierter Papier-Rückfallweg, Ausfallplan |
| Abhängigkeit von einer einzelnen Person („der Kollege, der das gebaut hat") | Das System stirbt mit dem Wechsel dieser Person | Dokumentation, Standardtechnologie, mindestens zwei Zuständige — **Kriterium für die Technologiewahl** |

---

## 7. Checkliste bis zur Inbetriebnahme

- [ ] Datenschutzbeauftragte/n frühzeitig einbinden (jetzt, nicht vor dem Start)
- [ ] Personalrat beteiligen; Entwurf einer Dienstvereinbarung erstellen
- [ ] Verzeichnis von Verarbeitungstätigkeiten erstellen
- [ ] Schwellwertprüfung DSFA dokumentieren, ggf. DSFA durchführen
- [ ] Löschfristen abstimmen und technisch umsetzen
- [ ] AV-Verträge (Hosting, Mailversand) abschließen
- [ ] Berechtigungs- und Rollenkonzept schriftlich fixieren und **testen**
- [ ] Datenschutzhinweis nach Art. 13 DSGVO im Formular hinterlegen
- [ ] Verfahren für Betroffenenrechte festlegen
- [ ] Backup- und Wiederherstellungstest durchführen und protokollieren
- [ ] Papier-Rückfallweg für Ausfälle beschreiben
- [ ] Schulung für SL, STP, SEK und eine Kurzanleitung für das Kollegium
