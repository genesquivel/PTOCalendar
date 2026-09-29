# PTO Calendar

A single-file, offline PTO/vacation simulator built around **VDC's Section 6.5**
accrual policy. Open `index.html` in any browser — no build, no server, no
dependencies. All data is saved in your browser's `localStorage`, so
simulations persist between opens.

## What it does

- **Tracks Paolo** from **6.90 hrs as of Aug 22, 2026** through **Dec 31, 2027**,
  accruing **3.0768 hrs per full 80-hr biweekly period** (40 hrs/week, 80 hrs/year).
  The starting balance — and every other parameter — is manually overridable in
  **Settings**.
- **Day-by-day picker** — click any date to add **4 hr**, **8 hr**, a **custom**
  amount, or mark it **Out — No Pay**. Click again to change or remove it.
- **Balance everywhere** — header shows current balance plus projected end-of-2026
  and end-of-2027. Each month card shows **start → accrued → used → end**, the end
  rolling into the next month, plus **YTD used** and per-day running-balance
  tooltips. PTO in Jan, Mar and Oct all stacks into the year-end figure.
- **Hours and days** — every figure (header, month start/accrued/used/end, YTD,
  tooltips, the day picker) shows both hours **and** day-equivalents; set
  hours-per-day so the conversion stays right.
- **Known-balance override** — in Settings, set a *known balance as-of date* to snap
  the running balance to your real number on that day; the calendar accrues and
  deducts forward from there.
- **Per-date projection** — click any day and the picker shows your projected
  balance **as of that date** (not just the month end); hover any day for the same.
- **Monthly cumulative** — month-end becomes next month's start, so multi-month
  PTO is fully accounted for.
- **7 paid VDC holidays** — New Year's, Memorial, Independence, Labor, Thanksgiving,
  Day after Thanksgiving, Christmas — 8 hrs paid, **not** drawn from PTO. Fixed-date
  holidays follow the OPM observance rule: a Saturday holiday is observed the
  preceding Friday, a Sunday holiday the following Monday (e.g. Independence Day
  2027 → Mon Jul 5; Christmas 2027 → Fri Dec 24), marked "(observed)".

## Accrual logic (Section 6.5)

- Rate: **0.03846 hrs of vacation per hour worked**
  - 40 hrs/week → 1.5384 hrs/week
  - 80 hrs/biweekly → **3.0768 hrs/period**
  - 2,080 hrs/year → **80 hrs/year** (2 weeks)
- Accrual posts at each biweekly **period end** (marked `$` on the calendar),
  anchored to Aug 22, 2026.
- **No accrual during unpaid leave** — Out-No-Pay hours are subtracted from the
  period's worked hours, reducing that period's accrual proportionally.

## Rules enforced / flagged

- **Earn first, then use** — no negative balance (overdrawn days are outlined red
  and flagged as blocking).
- **120 hr carryover cap** — anything above 120 on Dec 31 is forfeited, with a warning.
- **2-week / 1-month-gap rule** — when >80 hrs is banked, a single PTO stretch is
  capped at 2 weeks (80 hr) and consecutive blocks need a 1-month gap; violations
  are flagged.
- **Voluntary quit** — set a quit date to forfeit the remaining balance (Texas
  requires no payout).
- **Supervisor approval** — standing reminder that all PTO needs approval.
- **Out — No Pay = strike** — 12 strikes triggers a "no raises / promotion / bonus"
  warning.

## Baselines

The app is calibrated to a real payroll anchor: **as of the 09/25/2026 pay date
(period 09/06–09/19), available = 12.98 hrs.** Everything projects forward from that
known number. With no PTO entered:

| Milestone | Balance |
|---|---|
| Current (as of today, in range) | 12.98 hrs |
| End of 2026 | ~34.5 hrs |
| End of 2027 | ~114.5 hrs (right under the 120 cap) |

The pure Aug-22 model projected 13.05 at that point, so real accrual ran ~0.07 hr
light — the September card folds that correction into its accrued figure so it still
reconciles (start + accrued − used = end). "Today" tracks the viewer's real date.

> Note: end-of-2026 depends on whether the late-December biweekly period is counted
> in the year it *ends* (34.6) or the year it's *paid* (~31.5). The model counts it
> in the year it ends, which makes the end-of-2027 figure land exactly on 114.6.
> Use the **starting balance override** in Settings to pin any figure you prefer.

## Data

- **Export / Import** buttons save or load your entries and settings as JSON.
- **Reset all PTO** clears entries but keeps settings.
- Nothing leaves your browser.
