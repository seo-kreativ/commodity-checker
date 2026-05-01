# Commodity Checker — Claude Code Skill

> **[Deutsch](#deutsch) | [English](#english)**

---

## Deutsch

Analysiert Web-Content auf Austauschbarkeit und bewertet ihn mit einem simulierten `contentEffort`-Score (basierend auf dem Google Content Warehouse API Leak 2024).

### Was der Skill macht

- **contentEffort-Score (0–100)** mit Ampel-Bewertung (Commodity / Grauzone / Non-Commodity / Elite)
- **8-Dimensionen-Breakdown**: Proprietary Data, Personal Experience, Opinion/Stance, Specificity, Replication Resistance, Information Gain, Entity Signals, Structural Originality
- **Commodity-Fingerprint**: erkennt 6 DACH-typische Patterns (Tipps-Liste, Definition-Stub, Blind-Vergleich, Ratgeber-Standard, Anleitung-Klon, Non-Commodity)
- **SERP-Delta**: vergleicht gegen Top-3-Konkurrenz (via DataForSEO oder web_search)
- **5-Fragen-Selbsttest** (KI-Test, Eigene Daten, Profi-Test, Meinungstest, Vermisst-Test)
- **Rescue-Plan** mit 3 priorisierten Maßnahmen und pattern-spezifischen Strategien
- **3 Headline-Rewrite-Vorschläge** (Datenpunkt-Anker, Entscheidungs-Narrative, Kontra-Intuition)

### Installation

**Option 1 — Skill-Paket (empfohlen)**

```bash
claude skills install commodity-checker.skill
```

**Option 2 — Aus dem Repository**

```bash
git clone https://github.com/seo-kreativ/commodity-checker
claude skills install ./commodity-checker/commodity-checker
```

### Verwendung

Der Skill wird automatisch ausgelöst bei Begriffen wie:

- `commodity check`, `ist das commodity content`, `content prüfen`
- `contentEffort`, `commodity analyse`, `non-commodity`
- `URL auf Qualität prüfen`, `ist mein Artikel gut genug`
- oder einfach: URL + Frage nach Qualität/Differenzierung

**Beispiel:**

```
/commodity-checker https://example.com/mein-artikel
```

```
Ist dieser Artikel commodity content?
https://example.com/mein-artikel
```

### Hintergrund

Der Score simuliert Googles `contentEffort`-Attribut aus dem Content Warehouse API Leak (2024, via Shaun Anderson / Hobo-Web-Analyse). Die Gewichtung der 8 Dimensionen ist eine Annäherung — **nicht offiziell bestätigt**.

### Disclaimer

> Dieser Skill ist **nicht mit Google verbunden** und stellt keine offizielle Aussage von Google dar. Alle Bewertungen sind simulierte Einschätzungen auf Basis öffentlich verfügbarer Analysen des Google Content Warehouse Leaks. Es wird keine Haftung für Richtigkeit, Vollständigkeit oder Einfluss auf das Ranking übernommen.
>
> Der Skill analysiert ausschließlich öffentlich zugängliche URLs. Nutzer sind selbst dafür verantwortlich, dass sie nur Inhalte analysieren, für die sie die entsprechenden Rechte besitzen oder die öffentlich zugänglich sind.

### Datenschutz

> Der Skill verarbeitet ausschließlich öffentlich zugängliche Inhalte. Personenbezogene oder personenbeziehbare Daten werden nicht aktiv gesammelt, gespeichert oder weitergegeben. Nutzer sollten sicherstellen, dass die analysierten URLs keine sensiblen oder geschützten Daten enthalten.

---

## English

Analyzes web content for commodity-ness and scores it using a simulated `contentEffort` score (based on the Google Content Warehouse API Leak 2024).

### What the skill does

- **contentEffort Score (0–100)** with traffic-light rating (Commodity / Gray Zone / Non-Commodity / Elite)
- **8-dimension breakdown**: Proprietary Data, Personal Experience, Opinion/Stance, Specificity, Replication Resistance, Information Gain, Entity Signals, Structural Originality
- **Commodity Fingerprint**: detects 6 common DACH patterns (Tips List, Definition Stub, Blind Comparison, Standard Guide, Tutorial Clone, Non-Commodity)
- **SERP Delta**: compares against top 3 competitors (via DataForSEO or web_search)
- **5-question self-test** (AI Test, Own Data, Expert Test, Opinion Test, Missed Test)
- **Rescue plan** with 3 prioritized actions and pattern-specific strategies
- **3 headline rewrite suggestions** (Data Anchor, Decision Narrative, Counter-Intuition)

### Installation

**Option 1 — Skill package (recommended)**

```bash
claude skills install commodity-checker.skill
```

**Option 2 — From the repository**

```bash
git clone https://github.com/seo-kreativ/commodity-checker
claude skills install ./commodity-checker/commodity-checker
```

### Usage

The skill is triggered automatically by phrases like:

- `commodity check`, `is this commodity content`, `check my content`
- `contentEffort`, `commodity analysis`, `non-commodity`
- `check URL for quality`, `is my article good enough`
- or simply: a URL + a question about quality/differentiation

**Example:**

```
/commodity-checker https://example.com/my-article
```

```
Is this article commodity content?
https://example.com/my-article
```

### Background

The score simulates Google's `contentEffort` attribute from the Content Warehouse API Leak (2024, via Shaun Anderson / Hobo-Web analysis). The weighting of the 8 dimensions is an approximation — **not officially confirmed**.

### Disclaimer

> This skill is **not affiliated with Google** and does not represent any official statement by Google. All scores are simulated estimates based on publicly available analyses of the Google Content Warehouse Leak. No liability is accepted for correctness, completeness or impact on search rankings.
>
> This skill only analyzes publicly accessible URLs. Users are solely responsible for ensuring they only analyze content they own or that is publicly available and that no sensitive or protected data is exposed.

### Privacy

> This skill only processes publicly accessible content. No personal or personally identifiable data is actively collected, stored or shared. Users should ensure that the analyzed URLs do not contain sensitive or protected data.

---

## File structure

```
commodity-checker/
├── SKILL.md                         # Skill logic and workflow
└── references/
    ├── scoring-model.md             # 8-dimension rubric with examples
    └── rescue-strategies.md         # Pattern-based rescue strategies
```

## Author

Created by [seo-kreativ.de](https://seo-kreativ.de)

## License

MIT
