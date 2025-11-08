#Technical Specification (Scenario 2)

**Created by:** [Aldren Yabut]  
**Updated by:** [Aldren Yabut]  
**Date Created:** [November 7,2025]  
**Date Updated:** [November 7, 2025]  
**Version:** [0.0]
**LLM Used:"" [LLM] (optional if LLm used)

**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO or Director of Treasury  

**Purpose:** To design a quantitative spreadsheet model that evaluates three FX hedging strategies forward contract, money market hedge, and currency options for a €4.5 million receivable due in one year. The goal is to identify the most effective method to protect against euro depreciation while maintaining potential upside if the euro strengthens.

## 1. Problem Statement

Our company expects to receive €4.5 million in 12 months from a European client, creating a foreign exchange exposure to movements in the EUR/USD rate. A weaker euro would reduce the USD value of this receivable, while a stronger euro would increase it.

The objective is to protect the USD value of this payment while allowing for some upside potential if the euro appreciates. This specification provides the framework for analyzing and comparing three hedging strategies forward contract, money market hedge, and currency options—within the context of the firm’s corporate treasury risk management plan.

---

## 2. Inputs (Known Variables)

| Variable | Description | Unit | Example | Source |
|-----------|-------------|------|----------|--------|
| `FC_AMT` | Foreign-currency receivable | EUR | 4,500,000 | Client Contract |
| `S₀` | Current EURUSD spot rate | USD/EUR | [1.1566] | Market data |
| `F₀` | 1-year EURUSD forward rate | USD/EUR | 1.0890 | Provided |
| `r_USD` | USD 1-year interest rate | % | [4.8] | Market data |
| `r_EUR` | EUR 1-year interest rate | % | [3.5] | Market data |
| `t` | Time to maturity | Years | 1 | Fixed |
| `K_put` | EUR Put strike | USD/EUR | [1.16] | Analyst choice |
| `K_call` | EUR Call strike | USD/EUR | [1.18] | Analyst choice |
| `Premium_put` | Put premium | USD per contract | 0.017 | Scenario |
| `Premium_call` | Call premium | USD per contract | 0.022 | Scenario |

---

## 3. Assumptions & Constraints

- Interest rates are annual and based on a 365-day year.
- Forward rate (F₀) represents a 1-year maturity.
- All rates are quoted as USD per EUR.
- Option premiums are paid upfront in USD.
- Transaction costs and taxes are ignored.
- No counterparty or credit risk assumed.
- Market rates stay constant over the year.
- Hedges mature at the same time as the receivable.
- Exchange rates rounded to four decimals; percentages to two.

---

## 4. Calculation Flow

1. Forward Hedge:
- Use the 1-year forward rate (F₀) to fix the USD amount today.
- Calculate: €4.5M × F₀.
- Compare this fixed value to unhedged outcomes.

2. Money Market Hedge
- Discount the euro receivable by the euro rate (r_EUR).
- Convert to USD at the spot rate (S₀).
- Borrow equivalent USD and repay in one year using r_USD.
- Compare the final USD value to the forward hedge.

3. Option Hedge
- Buy a EUR put (K_put), optionally sell a call (K_call).
- For each future rate (S_T), find the option payoff: max(K_put – S_T, 0).
- Add payoff to unhedged proceeds and subtract premiums.
- Compare across all FX scenarios.

4. Unhedged Case
- Calculate USD value: €4.5M × S_T.
- Use as a baseline for comparison.

5. Compare Results
- Summarize all hedge results in one table.
- Create payoff charts to show risk, cost, and upside.
  
---

## 5. Outputs

| Output | Description | Format | Purpose |
|---------|--------------|---------|----------|
| `USD_forward` | USD proceeds from forward hedge | Numeric | Fixed Rate benchmark |
| `USD_mm` | USD proceeds from money market hedge | Numeric | Verify Interest Rates |
| `USD_put` | USD proceeds from EUR put hedge | Table | Sensitivity & protection |
| `USD_call` | USD proceeds from EUR call hedge | Table | Test upside potential |
| `Chart_1` | Hedge outcomes vs. S_T | Line chart | Visual risk comparison |
| `Summary` | Written conclusion | 1–2 paragraphs | Support Decision |

---

## 6. Sensitivity Plan

- Vary the EUR/USD spot rate at maturity (Sₜ) from 1.03 to 1.14 (+/-5% around the current spot of 1.089).
- For each rate, calculate USD proceeds from all three hedging methods, Forward, Money Market, and Option Hedge.
- Show results in a comparison table and a line chart to visualize how each hedge performs as the euro strengthens or weakens.

---

## 7. Limitations & Next Steps

- This analysis excludes FX volatility, transaction costs, and counterparty risk. It assumes constant interest rates and perfect market conditions.
- The next step is to build the Excel model to calculate and compare USD proceeds for each hedge strategy under varying EUR/USD scenarios.
