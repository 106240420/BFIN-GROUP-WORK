# Decision log — Kappa Foundation (initial decision record) | We used AI to generate this depend on our contents

Each entry: what we decided, the alternatives, why, and where the evidence is. File references are to `notebooks/02_kappa_analysis.ipynb` (§) and `outputs/original_22Oct/` (T/F).

| # | Decision | Alternatives considered | Reason | Evidence |
|--:|:--|:--|:--|:--|
| 1 | Data sources: Yahoo (yfinance), French library, U.S. Treasury, SEC EDGAR, Damodaran | FRED for breakeven/yields | FRED CSV download returned a maintenance page on our retrieval day; Treasury publishes the same curves officially | `data/raw/source_record.csv`, notebook 01 Step 4 |
| 2 | Replace CSGS (CSG Systems) with NSIT (Insight Enterprises) as IT stock | keep CSGS from another source | Yahoo returns no data for CSGS (no longer listed). Logged as FAILED, not filled. Shows survivorship bias in our universe | notebook 01 Step 2, §2.3 |
| 3 | Universe: 10 stocks in 6 sectors + XMLV, RWL; benchmark SPY | other low-vol/size ETFs; equal-weight S&P 500 as benchmark | Stable mid-caps fit fixed payments; RWL adds a smart-beta tilt; SPY is simple, investable, total-return comparable | §2, T02 |
| 4 | Estimation window Jan 2016–Dec 2022 (84 months) | 60 months (2018–2022); Feb 2015–Dec 2022 (95 months) | Whole calendar years, includes 2020 and 2022 stress, closer to 2022 business mix; robustness checked | §1.4, §5.5, T11 |
| 5 | Discount curve by bootstrapping with flat forwards | linear spot interpolation | Prices all bonds exactly, no extra parameters; PV of payments differs by only ≈ USD 50 | §3.2, T04, F01 |
| 6 | Fund the 2024/2027 payments by exact cash-flow matching: 2,157 Beta + 3,479 Delta | immunization with Gamma + Epsilon; independent matching (Beta for 2024, Delta for 2027 without using coupons) | No rate risk to the payments, no forced sales; same economic cost as PV of payments; using Delta coupons saves ≈ USD 0.22M vs independent matching | §3.4–§3.5, T06, T07 |
| 7 | Keep the 2023 Delta coupon in cash at 0% until 2024 | reinvest in Alpha-type bills | Conservative; costs only ≈ USD 4k in PV | §3.4 |
| 8 | Inflation 2.3% (stress 3.5%) | Fed goal 2%; survey forecasts | Market breakeven on 30 Dec 2022 (5y 2.33%, 10y 2.30%) | §4.1, notebook B §2 |
| 9 | Expected returns = CAPM (β × ERP), ERP = 5% | historical mean returns | Historical means are too noisy and favour past winners (look-ahead in our name choice) | §5.2, notebook B §4 |
| 10 | Recommended growth portfolio: constrained max-Sharpe with SIM covariance | same with sample covariance; Eta = unconstrained historical max-Sharpe | Eta: 6 names, 85% in 3 past winners → rejected. SIM vs sample: similar realised risk out of sample, SIM weights less driven by noisy correlations | §5.3–§5.5, T10 |
| 11 | Reading of the trustees' "~15% loss": stress loss ≤ 15% and 1-yr 95% VaR ≤ 10%, both net of the fixed payments | gross market value loss; VaR only | Dedicated bonds and payments move together; stress needed because normal VaR understates tail risk (L04) | §5.6, T12 |
| 12 | 49% of the remainder in the growth portfolio (≈ 26% of the fund), rest in Epsilon (matures 2030) | all-safe (Epsilon only); higher equity share | All-safe misses the real goal (≈ USD 7.66M real); A = 4 optimum is just inside the stress limit; goal probability ≈ 67% | §4.1, §5.6–§5.8, T08, T14 |
| 13 | Evaluation rule frozen: December rebalancing with 3 pp drift band, SPY buy-and-hold, metrics incl. FF3/Carhart alpha | monthly rebalancing; no band | Low turnover and costs; rule fixed before seeing 2023–2025 | §7, `frozen_policy.json` |
| 14 | Review triggers: inflation outlook > 3.4%, ERP view < 2.5%, stress loss > 15% | none | Levels at which the goal probability falls below 50% with our allocation | §5.8 |

## Open points for the final submission

* Run §7 with `RUN_EVALUATION = True` and save the results under a new output tag.
* Collect any feedback on this record and log changes here as new entries (old entries are not edited).
