# Market & Competitor Intelligence Agent for Women's Health Tech

This agent acts as an always‑on market researcher for women’s health tech founders. It tracks a curated set of competitors and market signals, then turns raw updates into actionable founder briefings.

This repo is focused on the **agentic workflow** and state management; data collection is mocked/simplified for portfolio purposes.

---

## What This Agent Does

- Ingests:
  - A list of competitors (names, URLs, brief descriptions).
  - A small feed of market/news items and product updates (from files or APIs).
- Classifies signals into categories:
  - Product launches and feature changes.
  - Partnerships and pilots.
  - Pricing and packaging changes.
  - Regulatory / clinical / reimbursement news.
- Maps signals to implications for the founder’s company:
  - “What this might mean for your positioning, roadmap, or GTM.”
- Produces a periodic **Founder Briefing**:
  - 1–2 pages of key changes, risks, and opportunities.

---

## Architecture

Core nodes:

1. **SignalIngestionAgent**
   - Reads new raw items from configured sources (in this repo: JSON/CSV files).
   - Normalizes them into a common signal schema.

2. **ClassificationAgent**
   - Tags each signal with type (product, partnership, pricing, regulatory, etc.) and segment (maternal, fertility, menopause, broad OB/GYN).

3. **ImpactAssessmentAgent**
   - Given the founder’s segment, stage, and strategy, assesses whether each signal is:
     - High / medium / low impact.
     - Threat, opportunity, or watch item.

4. **BriefingWriterAgent**
   - Groups signals into a human‑readable founder briefing (Markdown or HTML).

Example state:

```python
class IntelState(TypedDict):
    founder_profile: Dict[str, Any]
    raw_signals: List[Dict[str, Any]]
    classified_signals: List[Dict[str, Any]]
    assessed_signals: List[Dict[str, Any]]
    briefing: str
