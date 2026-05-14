# EMItrack

A minimalist, single-file web application for calculating, visualising, and tracking loan EMIs — with optional GST on interest.

---

## Features

### Calculator
- Enter principal amount, tenure (months or years), annual interest rate, and loan start month
- Instant EMI calculation using the standard reducing-balance formula
- Named loans for easy identification and organisation

### GST Support
- Toggle GST on/off per loan
- Configurable GST rate (default: 18%), applied on the interest component of each EMI
- Separate GST column in the amortization table when enabled
- Effective annual rate recalculated to reflect GST burden

### Results Dashboard
| Metric | Description |
|---|---|
| Monthly EMI | Base EMI + GST (if enabled) |
| Total Interest | Cumulative interest paid over tenure |
| Total GST | Cumulative GST on interest (when enabled) |
| Total Outflow | Principal + Interest + GST |
| Effective Rate | Annualised cost of borrowing |

### Visualisation
- Stacked bar chart showing the principal vs. interest (vs. GST) split across the loan tenure
- Early months show higher interest weight; later months flip to principal-heavy — clearly visible in the chart

### Amortization Schedule
- Month-by-month table: EMI, principal paid, interest paid, GST (if enabled), and outstanding balance
- Scrollable with sticky headers for long tenures

### Loan Tracker
- Every calculated loan is saved automatically in browser `localStorage`
- Saved loans appear in the sidebar — click any to reload its full details and results
- Delete individual loans with the × button

---

## Usage

This is a self-contained HTML file — no build step, no dependencies to install.

1. Download `index.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)
3. Fill in the loan details and click **Calculate EMI**

That's it.

---

## How EMI is Calculated

The standard reducing-balance (flat reducing) formula:

```
EMI = P × r × (1 + r)^n / [(1 + r)^n − 1]
```

Where:
- `P` = Principal loan amount
- `r` = Monthly interest rate = Annual rate / 12 / 100
- `n` = Tenure in months

### GST on Interest

Each month, GST is applied only to the interest component — not the principal:

```
Monthly GST = Interest component × (GST rate / 100)
Effective monthly outflow = EMI + Monthly GST
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Structure | HTML5 |
| Styling | CSS3 (custom properties, grid, flexbox) |
| Logic | Vanilla JavaScript (ES6+) |
| Charts | [Chart.js 4.4.1](https://www.chartjs.org/) via CDN |
| Fonts | DM Serif Display, DM Mono, Outfit via Google Fonts |
| Persistence | Browser `localStorage` |

No frameworks. No bundler. No server required.

---

## Browser Support

Works in all modern browsers. Requires JavaScript to be enabled.

---

## Limitations

- Loan data is stored in the browser's `localStorage` — it is not synced across devices or browsers
- Clearing browser data will erase saved loans
- GST calculation assumes a flat rate on the interest portion; actual GST applicability may vary by lender and loan type — consult a financial advisor for specific cases
