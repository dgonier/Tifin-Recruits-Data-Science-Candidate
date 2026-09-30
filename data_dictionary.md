# Data dictionary

Raw exports from Northwind's three custodians (Schwab, Fidelity, Pershing) and their
CRM. The data covers January 2023 through December 31, 2025. All data is synthetic;
any resemblance to real people is coincidental.

Descriptions below are as documented by Northwind Operations.

## `advisors.csv`: one row per advisor, current and former

| column | description |
|---|---|
| advisor_id | Advisor identifier, e.g. `A001` |
| first_name, last_name | Advisor name |
| office | Boston, Chicago, Denver, Austin, Scottsdale |
| title | Senior Wealth Manager, Lead Advisor, Associate Advisor |
| hire_date | Date joined Northwind |
| termination_date | Date left Northwind (blank if active) |
| termination_reason | HR reason code (blank if active) |

## `households.csv`: CRM household record (snapshot as of 2025-12-31)

A *household* is the client relationship: one family, possibly many accounts.

| column | description |
|---|---|
| household_id | Household identifier |
| household_name | Display name |
| primary_birth_year | Birth year of the primary client |
| marital_status | Married, Widowed, Single, Divorced |
| state | State of residence |
| acquisition_channel | How the relationship came to Northwind. "Lakeside Acquisition (2022)" = clients who came over when Northwind acquired Lakeside Advisors in April 2022. "Inheritance" = heir of a former client. |
| client_since | Relationship start date |
| service_tier | Service tier assigned at onboarding (Core / Premier / Private Client) |
| risk_profile | Conservative, Moderate, Growth, Aggressive |
| fee_schedule | `Standard` (see `fee_schedules.csv`) or `Negotiated` |
| negotiated_fee_bps | Annual fee in basis points if Negotiated |
| household_status | CRM status: Active / Closed |
| primary_advisor_id | Advisor currently responsible for the household |

## `advisor_assignments.csv`: history of which advisor served each household

| column | description |
|---|---|
| household_id | |
| advisor_id | |
| start_date, end_date | Assignment period (end_date blank = current) |
| assignment_reason | Why the assignment started |

## `accounts.csv`: one row per custodial account

| column | description |
|---|---|
| account_id | Account identifier |
| household_id | Owning household |
| account_type | e.g. Joint Taxable, Traditional IRA, Roth IRA, Trust, Inherited IRA, 529 Plan |
| custodian | Custodian name as recorded at account opening |
| open_date | Date opened |
| close_date | Date closed (blank if open) |

## `monthly_balances.csv`: month-end market value per account

| column | description |
|---|---|
| account_id | |
| month_end | Month-end date. 2022-12-31 is included as an opening snapshot. |
| market_value | Market value in USD at month end, as reported by the custodian |

## `transactions.csv`: cash and asset movements (not trades within a portfolio)

| column | description |
|---|---|
| txn_id | Transaction identifier |
| account_id | |
| trade_date | |
| txn_type | `CONTRIBUTION`, `WITHDRAWAL`, `RMD` (required minimum distribution), `ACAT_IN` / `ACAT_OUT` (asset transfer from/to another firm), `JOURNAL_IN` / `JOURNAL_OUT` (transfer between accounts at Northwind), `FEE` (advisory fee debit) |
| amount | Amount in USD, as delivered by each custodian's feed |
| custodian | Custodian feed the record came from |
| contra_firm | For ACATs: the other firm, as reported |
| contra_account_id | For journals: the other Northwind account |

Dividends, interest and trades inside accounts are not included. They show up in
market value.

## `interactions.csv`: CRM activity log

| column | description |
|---|---|
| interaction_id | |
| household_id | |
| advisor_id | Who logged it |
| interaction_date | |
| interaction_type | Meeting - In Person, Meeting - Video, Phone Call, Email |
| topic | CRM dropdown category |
| notes | Free-text note written by the advisor. **Contains client PII; see the privacy constraint in the brief.** |

## `fee_schedules.csv`: Northwind's standard advisory fee schedules

| column | description |
|---|---|
| schedule_name | |
| effective_from, effective_to | Period the schedule applied |
| household_aum_min, household_aum_max | Household AUM band (USD) |
| annual_fee_bps | Annual fee for households in the band, in basis points of AUM, billed quarterly |
