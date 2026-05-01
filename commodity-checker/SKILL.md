---
name: commodity-checker
description: >
  Analysiert URLs oder Content-Texte auf Commodity-Gehalt und bewertet sie mit einem
  simulierten contentEffort-Score (basierend auf dem Google API Leak 2024).
  Gibt einen strukturierten Report mit Ampel-Bewertung, 8-Dimensionen-Breakdown,
  Commodity-Fingerprint, 5-Fragen-Selbsttest, SERP-Delta-Analyse und konkrete
  Rescue-Aktionen mit 3 Headline-Rewrite-Vorschlägen aus.

  Verwende diesen Skill IMMER wenn der Nutzer Begriffe wie:
  "commodity check", "ist das commodity content", "content prüfen", "austauschbar?",
  "contentEffort", "commodity analyse", "non-commodity", "Selbsttest Content",
  "URL auf Qualität prüfen", "ist mein Artikel gut genug", "content bewerten",
  "überprüfe diesen Artikel", oder wenn eine URL + Frage nach Qualität/Differenzierung
  genannt werden — auch ohne explizites "Commodity".

  Also trigger on English phrases like:
  "commodity check", "is this commodity content", "check my content", "is this generic?",
  "contentEffort", "commodity analysis", "non-commodity", "content self-test",
  "check URL for quality", "is my article good enough", "review this article",
  "analyze this content", or when a URL + question about quality/differentiation
  is given — even without explicit use of "commodity".
---

# Commodity Checker Skill

Bewertet Content auf Austauschbarkeit (Commodity-Score) und liefert einen
vollständigen Optimierungsplan. Simuliert Googles `contentEffort`-Attribut
aus dem API-Leak 2024.

**Vor der ersten Ausführung**: Lies beide Reference-Dateien:
- `references/scoring-model.md` — 8-Dimensionen-Rubrik mit Beispielen
- `references/rescue-strategies.md` — Pattern-basierte Rescue-Strategien

---

## Inputs

- **URL** (bevorzugt) — Artikel, Blogpost, Landingpage
- **Raw Content** (alternativ) — eingefügter Text, Headline + Intro reicht für Quick-Mode
- **Beides** — URL + Briefing/Draft für Cross-Check

Wenn nur Headline + URL ohne Volltext verfügbar: Quick-Mode ausführen (nur Phasen 1+2, kein SERP-Delta).

---

## Workflow

### Phase 0 — Input-Erkennung & Ankündigung

**Sprache / Language:** Antworte immer in der Sprache des Nutzers. / Always respond in the user's language.

Domain aus URL extrahieren (z.B. `seo-kreativ.de` aus `https://seo-kreativ.de/artikel/`).
Bei Raw Content ohne URL: DOMAIN als leeren String verwenden.

Kurz ankündigen was analysiert wird. Wenn URL angegeben:

```
web_fetch(url, html_extraction_method="markdown", text_content_token_limit=6000)
```

**Fehlerbehandlung web_fetch:**
- HTTP 4xx/5xx oder leere Antwort → Quick-Mode mit URL + Titel als Input, im Report als "Volltext nicht ladbar" kennzeichnen
- JS-only / Paywall erkennbar → Hinweis im Report, nur Snippet + Meta aus SERP für Phase 1 nutzen
- Timeout → einmal retry, dann Quick-Mode

Extrahiere aus dem HTML/Markdown:
- `<title>` und H1
- Meta Description (falls im Markup sichtbar)
- Alle H2/H3-Überschriften
- Volltext der Artikel-Body (Navigation, Footer ignorieren)
- Author-Signale: Autorenname, Byline, About-Link, Schema `@type: Person`
- Schema Markup: vorhanden/welche Types?
- Datum: last-modified oder published date

---

### Phase 1 — Surface-Analyse

1. **Commodity Fingerprint bestimmen** (lies `references/rescue-strategies.md` → Abschnitt "Fingerprints")

   6 DACH-Patterns erkennen anhand von Titel + H2-Struktur:
   - Pattern A: Tipps-Liste ("X Tipps für Y", "Y Dinge die…")
   - Pattern B: Definition-Stub ("Was ist X?", "X einfach erklärt")
   - Pattern C: Blind-Vergleich ("X vs Y", "Vor- und Nachteile")
   - Pattern D: Ratgeber-Standard ("Der komplette Guide", "Alles über X")
   - Pattern E: Anleitung-Klon ("So geht X", "Schritt-für-Schritt")
   - Pattern F: Already Non-Commodity (kein Match) — weiter zu Phase 2

2. **Keyword-Extraktion** (für SERP-Delta in Phase 2):
   Primäres Keyword aus Title/H1 ableiten (2–4 Wörter).

---

### Phase 2 — SERP-Delta

SERP-Delta **vor** der Dimension-Bewertung ausführen — die Marktlage beeinflusst die Einordnung.

**Priorität: DataForSEO (wenn verfügbar)**
```
serp_results(keyword="[primäres Keyword]", location_code=2276, language_code="de")
```
Erste 3 organische Ergebnisse (keine Ads, nicht eigene URL) auswerten:
- URL, Titel, Snippet
- Commodity-Fingerprint der Konkurrenz bestimmen
- Wortanzahl schätzen (aus Snippet-Länge)

**Fallback: web_search**
```
web_search(query="[keyword] site:de OR site:at OR site:ch")
```
Gleiche Auswertung wie oben.

Wenn weder DataForSEO noch web_search verfügbar: Phase überspringen, im Report kennzeichnen.

**Differenzierungs-Score** (1–5):
- 1: Alle 3 Konkurrenten haben identischen Angle
- 3: 1–2 Konkurrenten unterscheiden sich leicht
- 5: Content ist deutlich einzigartiger als alle 3

> Tipp für tiefere SERP-Analyse: `/serp-intelligence [keyword]` liefert vollständige Entity-Gap-Analyse und Content-Tiefe der Top-10.

---

### Phase 3 — contentEffort-Simulation (8 Dimensionen)

Lies `references/scoring-model.md` und bewerte jede der 8 Dimensionen auf einer Skala 0–10.
Berücksichtige dabei SERP-Kontext aus Phase 2: Wenn alle Konkurrenten ebenfalls niedrig in D1 sind, ist das ein Chancen-Signal.

**WICHTIG — Transparenz-Pflicht**: Im Report immer klar kennzeichnen:
> *Diese Bewertung ist eine simulierte Annäherung an Googles `contentEffort`-Attribut,
> basierend auf dem Content-Warehouse-API-Leak 2024 (Inference, nicht offiziell bestätigt).*

Berechnung:
```
Rohwert =
  (D1_Score × 0.22) +
  (D2_Score × 0.20) +
  (D3_Score × 0.15) +
  (D4_Score × 0.15) +
  (D5_Score × 0.13) +
  (D6_Score × 0.10) +
  (D7_Score × 0.03) +
  (D8_Score × 0.02)
→ Rohwert liegt zwischen 0.0 und 10.0
→ contentEffort Score = Rohwert × 10  →  [0–100]
```

**Score-Schwellen:**
| Score | Ampel | Label |
|-------|-------|-------|
| 0–39  | 🔴    | Commodity |
| 40–59 | 🟡    | Grauzone |
| 60–74 | 🟢    | Non-Commodity |
| 75–100| 🟢✓   | Elite Non-Commodity |

**5-Fragen-Selbsttest** (automatisierte Auswertung parallel zu Phase 3):

| # | Frage | Gut-Signal | Bewertung |
|---|-------|-----------|-----------|
| F1 | KI-Test: Könnte ChatGPT das in 90 Sek. identisch schreiben? | **Nein** = gut | ✅/❌ |
| F2 | Eigene Daten: Min. 1 Datenpunkt den nur der Autor erheben konnte? | **Ja** = gut | ✅/❌ |
| F3 | Profi-Test: Erfährt ein Branchenexperte wirklich etwas Neues? | **Ja** = gut | ✅/❌ |
| F4 | Meinungstest: Klare Positionierung vorhanden die der Autor verteidigt? | **Ja** = gut | ✅/❌ |
| F5 | Vermisst-Test: Würde jemand diese Seite vermissen wenn offline? | **Ja** = gut | ✅/❌ |

Selbsttest-Score: Anzahl positiver Antworten / 5

---

### Phase 4 — Report-Ausgabe

Report-Struktur (in dieser Reihenfolge):

---

#### 📊 COMMODITY CHECK: [Titel des Artikels]

**Ampel:** [🔴/🟡/🟢/🟢✓] **contentEffort Score: [X]/100**
**Selbsttest:** [X]/5 positiv
**SERP-Differenzierung:** [1–5]/5 (oder "nicht analysiert")

> ⚠️ *Simulation: basierend auf Google API Leak 2024 · Inference · nicht offiziell bestätigt*

---

#### 🔍 Commodity-Fingerprint

**Pattern:** [A/B/C/D/E/F]
**Diagnose:** [1–2 Sätze warum dieser Pattern]
**Typisches Risiko dieses Patterns:** [aus rescue-strategies.md]

---

#### 🆚 SERP-Delta

| # | Konkurrenz-URL | Fingerprint | Differenzierung |
|---|---------------|-------------|-----------------|
| 1 | [domain] | Pattern [X] | [Einzeiler] |
| 2 | [domain] | Pattern [X] | [Einzeiler] |
| 3 | [domain] | Pattern [X] | [Einzeiler] |

**Dein Vorteil:** [Was du hast was die anderen nicht haben — oder "noch kein klarer Vorteil erkennbar"]
**Dein Risiko:** [Was die anderen besser machen]
**Marktchance:** [Ist der SERP-Markt für Non-Commodity Inhalte offen oder schon besetzt?]

---

#### 📐 contentEffort-Breakdown

| Dimension | Gewicht | Score (0–10) | Begründung |
|-----------|---------|--------------|------------|
| Proprietary Data | 22% | X | [konkrete Textstelle oder Beobachtung] |
| Personal Experience | 20% | X | [konkrete Textstelle oder Beobachtung] |
| Opinion/Stance | 15% | X | [konkrete Textstelle oder Beobachtung] |
| Specificity | 15% | X | [konkrete Textstelle oder Beobachtung] |
| Replication Resistance | 13% | X | [konkrete Textstelle oder Beobachtung] |
| Information Gain | 10% | X | [konkrete Textstelle oder Beobachtung] |
| Entity Signals | 3% | X | [konkrete Textstelle oder Beobachtung] |
| Structural Originality | 2% | X | [konkrete Textstelle oder Beobachtung] |
| **Rohwert** | 100% | **[X.X]** | × 10 = **[Score]/100** |

---

#### ✅ 5-Fragen-Selbsttest

| # | Frage | Gut-Signal | Ergebnis | Begründung |
|---|-------|-----------|----------|------------|
| F1 | KI-Test | Nein | ✅/❌ | [1 Satz] |
| F2 | Eigene Daten | Ja | ✅/❌ | [1 Satz] |
| F3 | Profi-Test | Ja | ✅/❌ | [1 Satz] |
| F4 | Meinungstest | Ja | ✅/❌ | [1 Satz] |
| F5 | Vermisst-Test | Ja | ✅/❌ | [1 Satz] |
| | **Gesamt** | | **[X]/5** | |

---

#### 💪 Stärken (was schon gut funktioniert)

[Bullet-Liste, max. 4 Punkte — ehrlich, nicht inflationär]

---

#### 🚨 Gaps & Rescue-Plan

**Priorität 1 — [Dimension mit größtem Hebel]**
- Problem: [konkrete Beobachtung mit Textstelle]
- Rescue: [spezifische Aktion, nicht generisch]
- Fragen die helfen: [2–3 Fragen die proprietäre Daten surfacen würden]

**Priorität 2 — [nächste Dimension]**
[gleiche Struktur]

**Priorität 3 — [nächste Dimension]**
[gleiche Struktur]

*(Pattern-spezifische Rescue-Strategien: `references/rescue-strategies.md`)*

---

#### ✍️ Headline-Rewrite (3 Alternativen)

*Nur wenn proprietäre Elemente vorhanden sind. Sonst: die Fragen aus dem Rescue-Plan stellen die das Material erst liefern würden.*

Original: `[aktuelle Überschrift]`

**Option 1 — Datenpunkt-Anker:**
`[Rewrite mit konkretem Zahlen-/Ergebnis-Anker]`
*Warum: [1 Satz]*

**Option 2 — Entscheidungs-Narrative:**
`[Rewrite als Entscheidungsgeschichte "Warum ich X gemacht / abgelehnt habe"]`
*Warum: [1 Satz]*

**Option 3 — Kontra-Intuition:**
`[Rewrite der eine Erwartung bricht oder eine unbequeme Wahrheit benennt]`
*Warum: [1 Satz]*

---

#### ☑️ Sofort-Maßnahmen (priorisiert)

- [ ] [Aktion 1 — höchster Hebel, sehr konkret]
- [ ] [Aktion 2]
- [ ] [Aktion 3]
- [ ] [Aktion 4 — optional, mittelfristig]

---

## Qualitätssicherung

- Begründungen in der Breakdown-Tabelle immer mit konkreter Textstelle — nie "keine eigenen Daten vorhanden" ohne Beleg
- Headline-Rewrites nur wenn proprietary elements vorhanden; sonst zuerst die Material-Fragen stellen
- SERP-Delta: wenn top-3 nicht ladbar, Fingerprint aus Snippet schätzen und kennzeichnen
- Bei sehr kurzem Content (< 400 Wörter): Quick-Mode kennzeichnen, D1–D5 bewerten, D6–D8 als "nicht beurteilbar"
- Disclaimer zur contentEffort-Simulation nie weglassen

---

---

## Referenzen

- `references/scoring-model.md` — detaillierte Kriterien und Beispiele für alle 8 Dimensionen
- `references/rescue-strategies.md` — Pattern-spezifische Rescue-Strategien + proprietäre Fragen-Kataloge
