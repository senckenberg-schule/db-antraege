# 04 — Anforderungskatalog (aktueller Stand)

Prüfliste für die Umsetzung. **MUSS** — ohne das ist das System unbrauchbar oder
unzulässig. **SOLL** — deutlicher Mehrwert, in Stufe 1 verzichtbar. **KANN** — später.

Gestrichene Anforderungen sind mit Begründung aufgeführt, damit nicht später jemand
meint, sie seien vergessen worden.

---

## F — Fachlich

| ID | Anforderung | Prio |
|---|---|---|
| F-01 | Formular je Antragsart, gemeinsames Gerüst, zwei Konfigurationen | MUSS |
| F-02 | Antragstellung **ohne Anmeldung**, nur mit Adresse `@schule.hessen.de` | MUSS |
| F-03 | **Bestätigungslink** — Antrag wird erst nach dem Klick gültig, vorher für niemanden sichtbar | MUSS |
| F-04 | Unbestätigte Anträge nach 24 Stunden automatisch löschen | MUSS |
| F-05 | Standortauswahl Runkel · Villmar · Beide, Pflicht, in beiden Zeitraum-Zweigen | MUSS |
| F-06 | Entscheidung: genehmigen · ablehnen · Rückfrage; Kommentar Pflicht bei Ablehnung und Rückfrage | MUSS |
| F-07 | Rückfrage als Dialog am Vorgang; Antrag dabei bearbeitbar, Änderungen im Verlauf sichtbar | MUSS |
| F-08 | Kommentare nach dem Absenden nicht editierbar | MUSS |
| F-09 | Arbeitsvorrat der Schulleitung, sortiert nach **Beginn des Zeitraums** | MUSS |
| F-10 | Benachrichtigungen gemäß Matrix; Stundenplanung standortabhängig | MUSS |
| F-11 | Reduzierte Sicht: Stundenplanung ohne Rückfrage-Dialog, erst ab Genehmigung, nur eigener Standort | MUSS |
| F-12 | **Stornieren** durch Antragsteller oder Schulleitung, mit Benachrichtigung aller zuvor Informierten | MUSS |
| F-13 | Zurückziehen vor der Entscheidung | MUSS |
| F-14 | Am eigenen Antrag keine Entscheidungsschaltflächen | MUSS |
| F-15 | Anlagen; bei „Fortbildung" Anhang **oder** „Ort und Thema" | MUSS |
| F-16 | Lerngruppen als Freitext mit selbstlernenden Vorschlägen | SOLL |
| F-17 | Erinnerung an die Schulleitung bei bald beginnenden offenen Anträgen | SOLL |
| F-18 | „Antrag ändern" = stornieren und neu stellen, mit vorbelegten Werten | SOLL |
| F-19 | Filter *abgeschlossene anzeigen* in den Listen | SOLL |
| F-20 | Aggregierte Kennzahlen ohne Personenbezug | KANN |
| F-21 | Export der genehmigten Abwesenheiten als Datei | KANN |
| F-22 | Automatische Übergabe an Untis | KANN (Stufe 3) |
| F-23 | Anmeldung über Schulportal oder IServ | KANN |

### Gestrichen

| Anforderung | Warum |
|---|---|
| Fristenprüfung mit Begründungspflicht | Es gibt keine verbindlichen Antragsfristen. Das System bewertet den Zeitpunkt nicht |
| Eigener Status für Änderungsanträge | Ersetzt durch stornieren und neu stellen — ein Status und ein Sonderfall weniger |
| Menüpunkt „Archiv" | Suggeriert Dauerhaftigkeit und widerspricht der Löschfrist; ein Filter genügt |
| Rolle Sekretariat, Ansicht „Heute abwesend" | Die Abwesenheiten stehen ohnehin im Stundenplan |
| Rollenpostfächer | Ein von mehreren gelesenes Postfach taugt nicht als Anmeldung |
| Zustimmung der Begleitpersonen | Nennung genügt; sie werden mitgemeldet |
| Automatischer Konflikthinweis je Lerngruppe | Nicht möglich, da Lerngruppen Freitext sind |
| Serientermine | Nicht angefordert |

---

## D — Datenschutz und Sicherheit

| ID | Anforderung | Prio |
|---|---|---|
| D-01 | Verarbeitung in **Deutschland**, Auftragsverarbeitungsvertrag vor Vertragsschluss | MUSS |
| D-02 | Berechtigungsprüfung **serverseitig** bei jedem Zugriff | MUSS |
| D-03 | Keine inhaltlichen Angaben in E-Mails außer in der Meldung an die Stundenplanung | MUSS |
| D-04 | **Automatischer Löschlauf**: Anträge nach 12 Monaten, Entwürfe nach 90 Tagen, Protokolle nach 6 Monaten | MUSS |
| D-05 | Ausschließlich HTTPS; verschlüsselte Sicherungen | MUSS |
| D-06 | Passwörter als **Argon2id- oder bcrypt**-Hash; niemals im Repository | MUSS |
| D-07 | **Vier getrennte Konten**, keine gemeinsamen Zugänge | MUSS |
| D-08 | Passwortvergabe durch die Person selbst; Administration kennt kein fremdes Passwort | MUSS |
| D-09 | Begrenzung der Fehlversuche bei der Anmeldung und der Absendeversuche am Formular | MUSS |
| D-10 | Domänenprüfung auf **Gleichheit** des Teils nach dem letzten `@` | MUSS |
| D-11 | Vorgangslinks als lange Zufallszeichenfolge; öffnen nur den einen Vorgang | MUSS |
| D-12 | Anlagen: kein SVG/HTML, Auslieferung als Download, Ablage außerhalb des Web-Verzeichnisses, berechtigungsgeprüft | MUSS |
| D-13 | Keine Erhebung von Gesundheitsdaten; Hinweise im Formular gegen Atteste und Diagnosen | MUSS |
| D-14 | Datenschutzhinweis nach Art. 13 DSGVO im Formular | MUSS |
| D-15 | Keine personenbezogenen Auswertungen — technisch ausgeschlossen | MUSS |
| D-16 | Protokolldaten getrennt, zweckgebunden, kein Zugriff der Schulleitung | MUSS |
| D-17 | Keine Fremdressourcen (Tracking, Analyse, fremde Schriftarten oder Skripte) | MUSS |
| D-18 | Getestete Wiederherstellung aus der Sicherung | MUSS |
| D-19 | Zwei-Faktor-Authentifizierung für die vier Konten | SOLL (zurückgestellt) |

---

## Q — Qualität und Betrieb

| ID | Anforderung | Prio |
|---|---|---|
| Q-01 | Bedienbar auf dem Smartphone | MUSS |
| Q-02 | Antrag in unter 3 Minuten, Entscheidung in unter 30 Sekunden | MUSS |
| Q-03 | **Betrieb durch eine zweite Person übernehmbar** — Standardtechnik, dokumentiert | MUSS |
| Q-04 | Zeitgesteuerte Aufgaben möglich (Voraussetzung für D-04) | MUSS |
| Q-05 | Mailversand mit eigener Domain, SPF und DKIM; Zustellung an `@schule.hessen.de` geprüft | MUSS |
| Q-06 | Betriebsdokumentation: Einrichtung, Sicherung, Wiederherstellung, Konfiguration | MUSS |
| Q-07 | Barrierearme Bedienung | SOLL |
| Q-08 | Datenexport in offenem Format | SOLL |
| Q-09 | Papier-Rückfallweg bei Ausfall | SOLL |
| Q-10 | Automatisierte Tests für Berechtigungen, Statusübergänge und Domänenprüfung | SOLL |

---

## Die fünf Punkte, an denen es scheitern kann

1. **Q-03 — Wartbarkeit.** Das System hängt an einer Person. Langweilige, dokumentierte
   Technik schlägt jede elegante Lösung.
2. **D-04 mit Q-04 — Löschautomatik.** Ohne zeitgesteuerte Aufgaben läuft sie nicht, und
   sie ist die tragende Datenschutzmaßnahme. Beim Hoster vorab prüfen.
3. **Q-05 — Mailzustellung.** Kommt der Bestätigungslink nicht an, entsteht kein Antrag.
   Vorab testen, nicht hoffen.
4. **D-06 — keine Zugangsdaten im Repository.** Das Projekt liegt auf GitHub; was einmal
   eingecheckt wurde, bleibt in der Versionsgeschichte.
5. **Q-02 — Akzeptanz.** Ein System, das umständlicher ist als eine Mail an die
   Schulleitung, wird umgangen. Dann hat die Schule beide Verfahren parallel — das
   schlechteste aller Ergebnisse.
