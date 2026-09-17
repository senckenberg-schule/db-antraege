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
