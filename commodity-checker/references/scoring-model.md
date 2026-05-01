# Scoring Model — 8 Dimensionen

> **Modell-Status:** Das folgende Scoring-Modell ist eine eigene Bewertungsmethodik für Content-Qualität und strategischen Aufwand. Die Gewichtung ist eine **eigene heuristische Annäherung** auf Basis öffentlich diskutierter Analysen rund um das Google Content Warehouse Leak (2024, u. a. Shaun Anderson / Hobo-Web) sowie SEO-Praxiserfahrung; sie ist **nicht offiziell von Google bestätigt** und stellt keine Aussage über tatsächliche Ranking-Faktoren dar. Das Modell dient der internen Priorisierung und Redaktionsstrategie, nicht als Abbild von Googles Ranking-Logik.

## Übersicht

| # | Dimension | Gewicht | Was bewertet wird |
|---|-----------|---------|------------------|
| D1 | Proprietary Data | 22% | Originäre Messdaten, interne Metriken, echte Projektzahlen |
| D2 | Personal Experience | 20% | Eigene Ausführung der Aufgabe, nicht nur theoretisches Wissen |
| D3 | Opinion/Stance | 15% | Klare Positionierung die der Autor verteidigt |
| D4 | Specificity | 15% | Konkrete Details statt vager Generalisierungen |
| D5 | Replication Resistance | 13% | Wie schwer ist es, diesen Content zu replizieren? (invertiert) |
| D6 | Information Gain | 10% | Echter Informationsgewinn für einen Branchenexperten |
| D7 | Entity Signals | 3% | Author-Attribution, Credentials, verlinkte Biografie |
| D8 | Structural Originality | 2% | Struktur reflektiert einzigartiges Wissen-Org-Schema |

---

## D1 — Proprietary Data (Gewicht: 22%)

**Kernfrage:** Gibt es mindestens einen Datenpunkt, den nur diese Person/dieses Unternehmen erheben konnte?

| Score | Kriterium | Beispiel |
|-------|-----------|---------|
| 0–2 | Keine eigenen Daten; nur allgemeine Behauptungen oder zitierte Drittquellen | "Studien zeigen, dass 70% der Nutzer..." |
| 3–4 | Bekannte Branchendaten korrekt zitiert, aber ohne Eigenerhebung | "Laut Statista hat Deutschland 84 Mio. Einwohner..." |
| 5–6 | Mindestens ein eigener Datenpunkt, aber unspezifisch ("In meinen Projekten sehe ich oft...") | "In meiner Praxis beobachte ich steigende CPC-Werte" |
| 7–8 | Konkreter proprietärer Datenpunkt mit Kontext | "In Projekt X (E-Commerce, Haushaltsgeräte) stieg die CTR von 1,2% auf 3,4% nach der Überarbeitung der Title-Tags" |
| 9–10 | Mehrere proprietäre Datenpunkte, eigene Messreihe oder Fallstudie mit vollständigem Kontext | "Unsere Analyse von 47 Magento-Shops zeigt: Shops mit >3.000 Filterkombinationen haben im Median 18% weniger indexierte URLs als technisch erwartbar" |

**Signalwörter für hohen Score:** konkrete Prozentzahlen + Kontext, "in unserem Projekt", "unsere Auswertung von X Datensätzen", Screenshots aus GA4/GSC, Zeiträume + Maßnahmen + Ergebnis

**Signalwörter für niedrigen Score:** "Experten empfehlen", "man sollte", "es ist wichtig", "viele Unternehmen", "Studien zeigen" (ohne eigene Ergänzung)

---

## D2 — Personal Experience (Gewicht: 20%)

**Kernfrage:** Hat der Autor das beschriebene Problem selbst gelöst — oder schreibt er über etwas das er nur kennt?

| Score | Kriterium | Beispiel |
|-------|-----------|---------|
| 0–2 | Rein theoretische Darstellung, kein persönlicher Bezug, unpersönliche Formulierung | "Bei der Einrichtung von robots.txt sollte man beachten..." |
| 3–4 | Gelegentliche Ich-Formulierungen ohne echten Handlungs-Kontext | "Ich empfehle immer, zuerst die Indexierung zu prüfen" |
| 5–6 | Klare eigene Beteiligung, aber ohne spezifischen Kontext | "Ich habe schon viele robots.txt-Fehler gesehen" |
| 7–8 | Konkrete Situation aus eigener Praxis geschildert | "Bei einem Kunden mit einem Magento-Shop (B2B, 4.800 Produkte) hatten wir genau dieses Problem: Googlebot crawlt die Seite, indexiert aber nur 12% der URLs" |
| 9–10 | Detaillierte Fallschilderung mit Entscheidungsweg, Hindernissen und Ergebnis | Vollständiger Case-Study-Absatz: Situation → Diagnose → mehrere Optionen → warum diese Entscheidung → was passiert ist → was er heute anders machen würde |

**Wichtig:** "Wir haben bei einem Kunden..." zählt als persönliche Erfahrung. "Experten raten..." zählt nicht.

**Negative Signale:** Passivkonstruktionen ("Es wird empfohlen"), Generalisierungen ("in der Regel"), "man"-Formulierungen.

---

## D3 — Opinion/Stance (Gewicht: 15%)

**Kernfrage:** Vertritt der Artikel eine klare, begründete Position — oder laviert er diplomatisch durch "Es kommt drauf an"?

| Score | Kriterium | Beispiel |
|-------|-----------|---------|
| 0–2 | Keine erkennbare Position; beide Seiten werden gleichwertig dargestellt ohne Schluss | "Manche empfehlen A, andere B. Je nach Situation kann beides richtig sein." |
| 3–4 | Leichte Tendenz, aber nie klar ausgesprochen | "Tendenziell würde ich A bevorzugen..." |
| 5–6 | Position erkennbar, aber ohne Begründung aus eigener Erfahrung | "Ich empfehle definitiv A." |
| 7–8 | Klare Position mit Begründung und Einschränkung | "Für Shops unter 10.000 SKUs empfehle ich A, weil ich in drei Projekten gesehen habe, dass B hier mehr Aufwand erzeugt als Nutzen." |
| 9–10 | Kontroverse Position die der Autor verteidigt und mit eigener Evidenz untermauert, inklusive Gegenargumenten | "Die Community empfiehlt B. Ich rate meinen Kunden trotzdem zu A — hier sind drei Gründe warum, und hier sind die Szenarien wo B doch sinnvoll ist." |

**Goldstandard:** Der Autor sagt etwas, das ihn potenziell angreifbar macht — und erklärt warum trotzdem.

---

## D4 — Specificity (Gewicht: 15%)

**Kernfrage:** Sind die Aussagen so konkret, dass ein Leser sie sofort anwenden kann?

| Score | Kriterium | Beispiel |
|-------|-----------|---------|
| 0–2 | Alle Aussagen vage; keine konkreten Zahlen, Namen, Situationen | "Title-Tags sollten nicht zu lang und nicht zu kurz sein" |
| 3–4 | Einige konkrete Details, aber nur aus allgemeiner Quelle | "Title-Tags sollten laut Google unter 60 Zeichen lang sein" |
| 5–6 | Mix aus Konkretem und Vagem | "Ich nutze für Title-Tags 55–58 Zeichen und beobachte weniger Truncation" |
| 7–8 | Konsequent spezifisch: Zahlen, Branchen, Zeiträume, Named Situations | "Für E-Commerce-Shops mit mehr als 500 Produktvarianten empfehle ich einen anderen Ansatz als für Dienstleister-Seiten: [konkrete Unterscheidung]" |
| 9–10 | Hyper-spezifisch: leser kann den Schritt sofort reproduzieren, mit allen Parametern | "Schritt 3: Öffne die GSC, filtere nach Crawl-Status 'Gecrawlt – derzeit nicht indexiert', exportiere alle URLs mit >100 Klicks/Monat im letzten Quartal, und prüfe zuerst diese Gruppe auf Thin-Content-Signale" |

---

## D5 — Replication Resistance (Gewicht: 13%)

**Kernfrage (invertiert):** Wie hoch ist der Aufwand für eine KI oder Agentur, diesen Content zu replizieren?

| Score | Kriterium | Test |
|-------|-----------|------|
| 0–2 | Vollständig replizierbar; ChatGPT-Prompt mit dem Keyword würde identischen Inhalt erzeugen | "10 Tipps für besseres E-Mail-Marketing" |
| 3–4 | Leicht replizierbar; Grundstruktur und Argumente sind Standard, nur Formulierung unterscheidet sich | |
| 5–6 | Mäßig replizierbar; einige eigene Formulierungen, aber kein unlösbar proprietäres Element | |
| 7–8 | Schwer replizierbar; enthält mindestens ein Element das echte Erstquellen-Recherche erfordert | Echter Case-Study-Datenpunkt |
| 9–10 | Praktisch nicht replizierbar; Kern-Content ist ohne direkten Zugang zu den Originaldaten oder -erlebnissen nicht reproduzierbar | Vollständige Fallstudie mit internen Metriken |

**Proxy-Test:** Prompt `"Schreibe einen Artikel über [Hauptkeyword]"` in ChatGPT und vergleiche die erste Seite Ergebnis mit dem Artikel. Deckungsgrad = invertierter Score.

---

## D6 — Information Gain (Gewicht: 10%)

**Kernfrage:** Was lernt ein Leser, der bereits 2+ Jahre Erfahrung im Fachgebiet hat?

| Score | Kriterium |
|-------|-----------|
| 0–2 | Nullinformation für Experten; alles bekannte Grundlagen |
| 3–4 | Eine neue Formulierung bekannter Fakten, oder eine interessante Perspektive ohne neue Information |
| 5–6 | Mindestens ein Detail das auch erfahrenen Lesern neu sein könnte |
| 7–8 | Mindestens ein echter Erkenntnisgewinn: Widerspruch zu bisheriger Community-Meinung, neues Framework, Gegenbeispiel |
| 9–10 | Mehrere genuine Erkenntnisse die auch erfahrene SEOs/Fachleute noch nicht wussten oder anders gesehen haben |

**Hinweis:** Ein Artikel kann für Einsteiger sehr nützlich sein und trotzdem Score 1 bei D6 bekommen. Das ist kein Fehler — nur eine strategische Einordnung.

---

## D7 — Entity Signals (Gewicht: 3%)

**Kernfrage:** Ist erkennbar, wer hinter diesem Content steht — für Leser und Suchmaschinen?

| Score | Kriterium |
|-------|-----------|
| 0–2 | Anonymer Artikel, kein Autorenname, kein Byline |
| 3–5 | Autorenname vorhanden, kein weiterer Kontext |
| 6–8 | Autorenname + kurze Bio + Link zu Profilseite oder LinkedIn |
| 9–10 | Autorenname + ausführliche Bio + Schema @type:Person + verlinktes LinkedIn/Xing + externe Erwähnungen erkennbar |

---

## D8 — Structural Originality (Gewicht: 2%)

**Kernfrage:** Ist die Struktur des Artikels selbst ein Ausdruck einzigartigen Wissens?

| Score | Kriterium |
|-------|-----------|
| 0–2 | Standard-Struktur: Intro → Was ist X → Warum wichtig → Tipps → Fazit |
| 3–5 | Leichte Abweichung, aber erkennbares Standard-Template |
| 6–8 | Eigenes Framework, eigene Kategorisierung, eigene Taxonomie |
| 9–10 | Struktur selbst ist eine intellektuelle Leistung die den Leser die Welt anders sehen lässt |

---

## Score-Interpretation

| contentEffort Score | Label | Strategische Empfehlung |
|--------------------|-------|------------------------|
| 0–39 | 🔴 Commodity | Grundlegende Überarbeitung nötig. Fokus auf D1+D2. Ohne eigene Daten/Erfahrung: Seite bewusst als Definitions-Page positionieren (keine Traffic-Erwartung). |
| 40–59 | 🟡 Grauzone | Ein gezielter Eingriff (ein proprietärer Datenpunkt + eine klare Positionierung) kann den Score in die Non-Commodity-Zone heben. |
| 60–74 | 🟢 Non-Commodity | Gute Basis. Schwächste Dimension gezielt stärken. Headline ggf. besser auf einzigartigen Kern ausrichten. |
| 75–100 | 🟢✓ Elite | Weiter so. Prüfen ob Headline den einzigartigen Wert klar kommuniziert. |

---

## Hinweis zur Gewichtung

Die Gewichtung ist eine **eigene heuristische Annäherung** auf Basis öffentlich diskutierter
Analysen rund um das `contentEffort`-Attribut aus dem Google Content Warehouse Leak
(2024, via Shaun Anderson / Hobo-Web-Analyse), kombiniert mit SEO-Praxiserfahrung.

Die Leak-Dokumente **werden so interpretiert**, dass Google Attribute wie `contentEffort`
verwendet — offizielle Gewichte oder Formeln legen sie jedoch nicht offen. Die
8-Dimensionen-Logik und ihre Gewichtung sind eine **eigene Interpretation** und kein
verifiziertes Abbild von Googles Ranking-Logik.

**Dieses Modell ist ein Redaktions- und Strategie-Score zur internen Priorisierung —
kein Ranking-Detektor und keine belegbare Aussage über Googles tatsächliche Gewichtung.**

---

*Dieses Modell ist für interne Content-Bewertung gedacht. Es ersetzt keine offizielle
Google-Dokumentation. Wo Quellenlage und Interpretation auseinandergehen, wird dies
explizit kenntlich gemacht.*
