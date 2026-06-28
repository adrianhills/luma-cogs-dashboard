# Luma · Compute COGS Control Tower (mock)

A single-screen, zero-dependency mock dashboard for reasoning about **compute cost of goods sold (COGS)** at a generative-media lab. Built as a discussion prop for a TPM technical session on GPU / compute & COGS.

**Live demo:** _enable GitHub Pages (see below) → `https://<user>.github.io/luma-cogs-dashboard/`_

> ⚠️ **All numbers are illustrative / mock** — chosen to be order-of-magnitude plausible, none are real Luma figures. The *structure* is what's real: it mirrors how Luma actually prices and serves today.

## What it shows

| Panel | The question it answers |
|---|---|
| **KPI strip** | What's the blended cost/gen, gross margin, fleet utilization, idle reclaimed, external-model share — at a glance? |
| **Spend by surface** | Where does the GPU money go — consumer (Dream Machine), enterprise (Luma Agents + API), or research/training? |
| **Own vs. API** | Ray (in-house, carries training amortization) vs. Veo / Kling / Seedance (pass-through API spend — also COGS). |
| **Cost per generation** | The unit economic, by model × resolution. Credits charged → revenue; GPU-seconds → cost; margin per clip. |
| **Margin by plan tier** | Contribution margin per Luma Agents tier (Plus/Pro/Ultra) — surfaces the margin-negative power-user tail flat pricing hides. |
| **Utilization** | Claimed allocation vs. realized use — the #1 waste lever — and where to backfill the trough. |
| **Cost-per-gen trend** | Trended over time with model-release markers, so a "better but pricier" release is a deliberate call. |
| **Forecast simulator** | Move the demand/mix drivers (DAU, gens/user, API share, resolution, distillation adoption) → projected monthly COGS, revenue, and gross margin. The *baseline → simulate → re-baseline* loop. |

## The two-number mental model

A **marginal vs. fully-loaded** toggle (top right) recomputes every cost:

- **Marginal** — serving cost only (GPU-seconds + API pass-through). The right lens for pricing and rate-limit decisions.
- **Fully-loaded** — serving + amortized training compute + idle/reserved waste. The "is this product actually profitable" lens.

## Grounding (Luma's real pricing structure, mid-2026)

- Three **separate products with separate credit wallets**: **Dream Machine** (consumer web), **Luma Agents** (Plus $30 / 10k credits · Pro $90 / 40k · Ultra $300 / 150k), and the **Agents API** (pay-as-you-go / provisioned throughput).
- **Credits are the customer-facing unit** over GPU cost — video runs ≈ **4–280 credits/sec** depending on **model** (Ray = in-house; Veo / Kling / Seedance = third-party API), **resolution** (Draft → 4K), and audio.
- This is why the dashboard models *credits → revenue* and *GPU-seconds → cost* separately, and splits **own-model (training amortized)** from **API pass-through**.

## Run locally

It's a single static file — no build step.

```bash
# any static server works
python3 -m http.server 8093
# then open http://localhost:8093
```

## Deploy on GitHub Pages

1. Push this repo to GitHub.
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch → `main` / `(root)`.**
3. Wait ~1 minute; your site is at `https://<user>.github.io/luma-cogs-dashboard/`.

(`.nojekyll` is included so Pages serves the files as-is.)

## Tech

Plain HTML + CSS + vanilla JS. Inline SVG charts. No frameworks, no dependencies, no tracking — view source to read every assumption.
