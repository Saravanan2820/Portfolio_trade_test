# Portfolio_trade_test

# Portfolio Trade Order Compliance & Execution Checker

## Project Overview

The Portfolio Trade Order Compliance & Execution Checker is a Python-based application developed using Google Colab and Pandas.

The application evaluates proposed portfolio trades against predefined compliance and execution-readiness rules before execution.

Each trade is assigned one of three decisions:

- **Approved** – Trade passes all compliance checks.
- **Rejected** – Trade violates one or more mandatory compliance rules.
- **Needs Manual Sign-off** – Trade exceeds the maximum permitted position concentration and requires approval.

## Objectives

- Validate proposed trade information.
- Check restricted securities.
- Verify sufficient holdings before selling.
- Verify sufficient cash before buying.
- Calculate post-trade position concentration.
- Generate automated compliance decisions.
- Export the final compliance report as a CSV file.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Google Colab | Development environment |
| Pandas | Data processing and analysis |
| CSV | Trade input and report output |

## Project Workflow

The application follows six sequential compliance checks.

### Step 1: Trade Data Validation

Checks whether:
- Quantity is greater than zero.
- Price is greater than zero.
- Action is either Buy or Sell.

If validation fails:

**Decision:** Rejected

**Reason:** Invalid trade data.

### Step 2: Restricted Security Check

Checks whether the security exists in the portfolio's restricted securities list.

If the security is restricted:

**Decision:** Rejected

**Reason:** Security is restricted for this portfolio.

### Step 3: Sell Holdings Check

Checks whether the portfolio currently holds sufficient quantity of the security.

If available holdings are less than the requested sell quantity:

**Decision:** Rejected

**Reason:** Insufficient holdings to sell.

### Step 4: Buy Affordability Check

Calculates:

Purchase Cost = Quantity × Price

If purchase cost exceeds the available cash balance:

**Decision:** Rejected

**Reason:** Insufficient cash for this buy order.

### Step 5: Position Concentration Check

This check applies only to Buy orders.

Calculations include:

1. Post-trade cash balance.
2. Post-trade security quantity.
3. Post-trade value of the purchased security.
4. Value of all other holdings using their individual market prices.
5. Total portfolio value after the trade.
6. Position concentration percentage.

Formula:

Position Percentage = (Post-trade Security Value / Total Portfolio Value After Trade) × 100

If the position percentage exceeds the maximum permitted concentration:

**Decision:** Needs Manual Sign-off

**Reason:** Exceeds maximum position concentration — requires approval.

### Step 6: Final Decision

If the trade passes all applicable compliance checks:

**Decision:** Approved

## Input Data

The application accepts proposed trades through a CSV file named `trades_test.csv`.

Expected columns:

| Column | Description |
|---|---|
| portfolio_id | Portfolio identifier |
| security_id | Security identifier |
| action | Buy or Sell |
| quantity | Proposed trade quantity |
| price | Proposed trade price |
| security_type | Equity, Bond or ETF |

## Portfolio Reference Data

Each portfolio contains:

- Cash balance
- Restricted securities
- Maximum position percentage
- Current holdings
- Individual market prices for each holding

## Output

The application generates a compliance report named:

`compliance_report.csv`

The report includes:

- Original trade details
- Compliance decision
- Reason for the decision

## How to Run the Project

1. Open [Google Colab](https://colab.research.google.com/).
2. Upload the project notebook.
3. Upload `trades_test.csv`.
4. Run the notebook cells sequentially.
5. Initialize portfolio reference data.
6. Execute the compliance checking function.
7. Process all proposed trades.
8. Generate and download `compliance_report.csv`.

## Sample Compliance Results

The completed sample run processed 20 proposed trades.

| Decision | Number of Trades |
|---|---:|
| Approved | 13 |
| Rejected | 4 |
| Needs Manual Sign-off | 3 |
| **Total** | **20** |

## Key Features

- Sequential rule-based validation.
- Automated trade decision-making.
- Portfolio-level compliance checking.
- Position concentration calculation.
- Manual approval identification.
- Automated CSV report generation.

## Future Enhancements

- Integration with live portfolio data.
- Database connectivity.
- Interactive Streamlit dashboard.
- Detailed audit logs.
- User authentication and authorization.
- Automated compliance notifications.

## Disclaimer

This project is developed for educational and demonstration purposes. Portfolio reference data used in the sample implementation is illustrative. The application is not connected to a live trading system and does not execute actual trades.

---

**Project:** Portfolio Trade Order Compliance & Execution Checker

**Language:** Python

**Environment:** Google Colab

**Libraries:** Pandas
