# AI use 

We used AI to help us to code and draft the group work. The group decide the key terms, gave the instructions and made the final decisions. 

## What we gave to AI

1. **Overall approach.** We chose the approach "test Eta with a constrained Markowitz portfolio": fund the 2024 and 2027 payments first by exact cash-flow matching with Beta and Delta bonds, then build the growth portfolio with a constrained Markowitz optimisation that compares the sample covariance matrix with the single-index model, and reject the unconstrained historical max-Sharpe portfolio (Eta). The AI listed several possible approaches; we compared their strengths and weaknesses and picked this one.
2. **Securities.** We selected the 10 stocks (MSA, KAI, GEF, IOSP, FLO, CALM, IDA, NWN, CHE, NSIT) across 6 sectors, the two ETFs (XMLV, RWL) and the benchmark (SPY) from the candidates we discussed with the AI. 

## What the AI did

* Suggested alternative approaches, candidate securities, data sources and starting values for the assumptions (inflation from the Treasury breakeven, ERP 5% with a Damodaran cross-check, risk aversion A = 4, reading of the trustees' 15% loss concern, weight limits, trading costs). We reviewed these and accepted them as our assumptions.
* Wrote and debugged the Python code: data download and source record, bond pricing and cash-flow matching, the optimiser, risk calculations, tables and figures.

## Responsibility

We checked the bond results (YTM, discount factors, number of Beta and Delta bonds) by hand. We are responsible for all decisions, assumptions and interpretations in this submission.

Võ Hoàng Ngọc Phú · Trần Bình Minh · Hoàng Trọng Đăng