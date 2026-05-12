---
name: first-client-playbook
description: Orchestriert den 30-Tage-Plan zum ersten zahlanden Kunden. Führt die 7 Skills in der richtigen Reihenfolge aus, trackt Fortschritt und passt alles für den deutschen Markt an (DSGVO, Plattformen, €, Sprache). Trigger: "erstkunden-playbook", "playbook starten", "30-tage-plan", "erster kunde", "first client deutsch", "kundengewinnung starten".
---

# First Client Playbook (DACH-Edition)

30-Tage-Plan vom Nullpunkt zum ersten zahlanden Kunden — adaptiert für Deutschland, Österreich, Schweiz.

## Was dieses Skill macht

Führt den kompletten Ablauf aus:
1. **Woche 1**: Branche auswählen → Industry Download → Ride-Along → Money Map
2. **Woche 2**: Client Locator (Plattformen finden + Outreach starten)
3. **Woche 3**: Discovery Script (Discovery Calls führen)
4. **Woche 4**: Blueprint Builder + Closer Deck (Build-Plan + Sales-Deck)

Mit Fortschritts-Tracking, DACH-Markt-Anpassungen und Compliance-Checks.

## Bevor du startest

Stell sicher, dass diese Skills verfügbar sind:
- `industry-download`
- `ride-along`
- `money-map`
- `client-locator`
- `discovery-script`
- `blueprint-builder`
- `closer-deck`

## Session-State

Lies zu Beginn `memory/first-client-state.json` um den aktuellen Fortschritt zu kennen.
Erstelle die Datei wenn sie nicht existiert:

```json
{
  "started": null,
  "phase": "init",
  "industry": null,
  "week": 0,
  "steps_completed": [],
  "outputs": {}
}
```

Speichere nach jedem abgeschlossenen Schritt den aktualisierten State.

## DACH-Markt-Anpassungen (IMMER beachten)

Diese Anpassungen gelten für jeden Schritt. Sie überschreiben die US-zentrierten Defaults der Einzelskills.

### Plattformen (DACH statt US)

| US-Default | DACH-Alternative |
|---|---|
| Facebook Groups | Facebook-Gruppen (kleiner, aber existent) + Xing-Gruppen |
| Reddit (US-Subreddits) | r/de_EDV, r/selbststaendig, r/Finanzen, r/Handwerker |
| LinkedIn Groups | LinkedIn + Xing-Gruppen |
| Slack Communities | Deutsche Slack/Discord-Communitys (z.B. German Tech, digitale Vorreiter) |
| Cold Email | **In DE nicht ohne Opt-in!** → Stattdessen: LinkedIn/Xing DM, Telefon, Empfehlungen |
| US Conferences | Deutsche Messen + Branchenevents + IHK-Veranstaltungen |

### Rechtliche Compliance (IMMER prüfen)

1. **Keine Cold-Email-Kaltakquise** in DE (§7 UWG). Nur mit vorherigem Opt-in oder bestehender Geschäftsbeziehung.
2. **LinkedIn/Xing-DMs** sind Grauzone — persönlich halten, kein Massenversand, immer Opt-out anbieten.
3. **DSGVO**: Bei Datenerhebung (CRM, Kontaktdaten) auf Rechtsgrundlage achten.
4. **Impressumspflicht**: Bei Web-Präsenz oder Landingpage nötig.
5. **Kleinunternehmerregelung** (§19 UStG): Bei Start unter 22.000€/Jahr Umsatz — Rechnung ohne MwSt.

### Sprache & Ton

- Outreach IMMER auf Deutsch
- Formeller als US-Pendants, aber nicht steif
- "Sie" außer in informellen Communities
- Deutsche Branchenbegriffe (keine 1:1-Übersetzungen aus dem Englischen)

### Preise & Markt

- € statt $, 2.500€/Monat als Basis
- Setup Fee: 1.500-5.000€
- Deutsche Branchen recherchieren über Destatis, nicht US Census
- Lokale Wettbewerber und Software-Landschaft berücksichtigen

### Deutsche Zielbranchen (besonders geeignet)

- Handwerk (Sanitär, Elektro, Dachdecker, Maler) — größter Sektor, stark digitalisierungsbedürftig
- Steuerberater & Buchhalter — extrem administrative Last
- Kleine Industriebetriebe (CNC, Zulieferer)
- Arztpraxen / Zahnärzte (Privatpraxen mit Terminmanagement-Problemen)
- Architektur- & Ingenieurbüros
- Speditionen & Logistik (3-20 LKW)
- Facility Management / Gebäudereinigung

## Phase 1: Init — Branche auswählen

Wenn `phase == "init"`:

1. Frag den Nutzer nach einer Branche. Gib ihm die Liste der deutschen Zielbranchen als Inspiration.
2. Lass ihn eine auswählen oder selbst eine nennen.
3. **Wichtig**: Die Branche muss spezifisch genug sein. "Handwerk" ist zu breit. "Sanitärbetriebe mit 3-15 Mitarbeitern" ist gut.
4. Speichere die Branche im State (`phase: "week1"`, `week: 1`).
5. Gehe direkt zu Phase 2.

## Phase 2: Woche 1 — Branche verstehen + Problem finden

Wenn `phase == "week1"`:

Führe nacheinander aus (jeweils mit DACH-Anpassungen):

### Step 1: Industry Download
Rufe den `industry-download` Skill für die gewählte Branche auf.
- ZUSATZ DACH: Recherchiere auch auf deutschen Quellen (deutsche Foren, Xing-Gruppen, IHK-Seiten, Handwerkskammer, Branchenverbände).
- ZUSATZ DACH: Nutze Destatis für Branchenzahlen statt US Census.
- ZUSATZ DACH: Liste deutsche Software/Tools die die Branche nutzt (Lexware, DATEV, SevDesk, etc. statt QuickBooks).
- Speichere Output in `outputs.industry_download`.

### Step 2: Ride-Along
Rufe den `ride-along` Skill für die gewählte Branche auf.
- ZUSATZ DACH: Recherchiere deutsche Tagesabläufe, nicht US-zentrierte.
- ZUSATZ DACH: Nutze deutsche Zeiten, Währungen, Begriffe, gesetzliche Rahmenbedingungen (Arbeitszeit, Pausenregelung, Feiertage).
- Speichere Output in `outputs.ride_along`.

### Step 3: Money Map
Rufe den `money-map` Skill für die gewählte Branche auf, mit den Outputs aus Step 1+2.
- ZUSATZ DACH: Prüfe ob die gefundenen Probleme im deutschen Markt relevant sind.
- ZUSATZ DACH: Kalkuliere €-Beträge (nicht $).
- Speichere Output in `outputs.money_map`.

Nach Abschluss:
- Zeige Zusammenfassung: Branche, Top-Problem, geschätztes monatliches €-Potenzial.
- Update State: `steps_completed: [industry_download, ride_along, money_map]`, `phase: "week2"`, `week: 2`.
- Sag: "Woche 1 abgeschlossen. In Woche 2 finden wir raus, wo deine Kunden sind. Soll ich weitermachen oder willst du das Gelernte erst sacken lassen?"

## Phase 3: Woche 2 — Kunden finden

Wenn `phase == "week2"`:

### Step 4: Client Locator
Rufe den `client-locator` Skill für die gewählte Branche auf.
- ZUSATZ DACH: Ersetze die US-Plattform-Defaults durch DACH-Alternativen (siehe Plattform-Tabelle oben).
- ZUSATZ DACH: Füge hinzu: Xing-Gruppen, deutsche Branchenverbände, IHK-/HWK-Events, regionale Messen.
- ZUSATZ DACH: Outreach-Skripte auf DEUTSCH.
- ZUSATZ DACH: Warne vor Cold-Email-Rechtsprechung in DE. Empfiehl LinkedIn/Xing-DMs, Telefon oder Veranstaltungen.
- Speichere Output in `outputs.client_locator`.

Nach Abschluss:
- Zeige die Top-5-Plattformen für die Branche in DACH.
- Update State: `steps_completed` += `client_locator`, `phase: "week3"`, `week: 3`.
- Sag: "Deine Outreach-Kanäle stehen. Jetzt bereiten wir den Discovery Call vor. In Woche 3 führst du 3-5 Gespräche."

## Phase 4: Woche 3 — Discovery Calls

Wenn `phase == "week3"`:

### Step 5: Discovery Script
Rufe den `discovery-script` Skill für die gewählte Branche auf.
- ZUSATZ DACH: Script auf DEUTSCH. Deutscher Gesprächsstil.
- ZUSATZ DACH: Formeller Einstieg ("Guten Tag, schön dass es klappt").
- ZUSATZ DACH: Deutsche Einwände antizipieren ("Das macht unser Steuerberater schon", "Dafür haben wir eine Excel-Liste").
- Speichere Output in `outputs.discovery_script`.

Update State: `steps_completed` += `discovery_script`, `phase: "week3_waiting"`.

Dann:
- Sag dem Nutzer: "Das Discovery Script steht. Jetzt dein Job: Führe 3-5 Discovery Calls mit den Kontakten aus Woche 2. Komm zurück, wenn du ein Transkript oder detaillierte Notizen von einem vielversprechenden Call hast."
- Update State: `phase: "week3_waiting"`.

Wenn der Nutzer mit einem Transkript zurückkommt:
- Update State: `phase: "week4"`, `week: 4`.
- Gehe zu Phase 5.

## Phase 5: Woche 4 — Bauen & Closen

Wenn `phase == "week4"`:

### Step 6: Blueprint Builder
Rufe den `blueprint-builder` Skill mit dem Discovery-Call-Transkript auf.
- Speichere Output in `outputs.blueprint_builder`.

### Step 7: Closer Deck
Rufe den `closer-deck` Skill mit demselben Transkript auf.
- Stelle sicher dass das HTML-Template aus `closer-deck/assets/template.html` verwendet wird.
- ZUSATZ DACH: €-Beträge, deutsche Sprache im Deck.
- Speichere die HTML-Datei im Workspace ab.
- Speichere Output-Referenz in `outputs.closer_deck`.

Nach Abschluss:
- Update State: `steps_completed` += `blueprint_builder, closer_deck`, `phase: "complete"`.
- Zeige Zusammenfassung des gesamten Playbooks.
- Gratuliere! Der Build-Plan und das Sales-Deck sind fertig.

## Zusammenfassung bei Abschluss

Wenn `phase == "complete"`, zeige:
- Gewählte Branche
- Identifiziertes Problem
- Monatliches €-Potenzial
- Erstellte Artefakte (Build-Plan, Closer Deck HTML)
- Nächste Schritte: Bauen (mit Coding-Agent) + Closer Deck präsentieren + ersten Kunden closen

## Fortschritt manuell steuern

Der Nutzer kann jederzeit:
- "playbook status" → zeige aktuellen Stand
- "playbook reset" → starte von vorne (bestätigen lassen!)
- "playbook jump woche X" → springe zu einer Phase (warnen wenn vorgelagerte Steps fehlen)
- "playbook weiter" → mache mit der aktuellen Phase weiter
