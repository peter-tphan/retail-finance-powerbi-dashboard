# 📊 Finance Performance Dashboard

A Power BI finance reporting project developed from real operational invoice, payment and credit data.

The project focuses on building a reusable reporting model for receivables performance, credit exposure and customer payment behaviour, using Power Query, DAX and interactive analysis rather than relying on static finance reports.

> This repository contains an anonymised portfolio view. Customer-identifying information has been removed from the dashboard preview.

---

## 🔎 How to Review This Project

The dashboard preview below shows the reporting design, KPI framework and customer-level analysis.

The repository is intended to demonstrate the Power BI development and analytical logic behind the report rather than expose operational company data.

---

## 📊 Dashboard Preview

![Finance Performance Dashboard](assets/finance-performance-dashboard-demo.png)

---

## 🎯 Reporting Context

Finance reporting required information from invoice, payment, credit and overdue data to answer different questions within the same reporting model.

The key challenge was not simply displaying totals. The report needed to distinguish between:

- invoiced revenue and cash collected
- current outstanding and overdue exposure
- historical invoice performance and current AR position
- credit limits and actual utilisation
- customer payment speed and late-payment behaviour
- portfolio movements and the customers driving them

The dashboard was therefore designed as an interactive reporting layer rather than a collection of independent charts.

---

## 🧱 Data Preparation & Semantic Model

Power Query was used to prepare invoice and supporting finance data before analysis.

Key work included:

| Area | Implementation |
|---|---|
| Data cleansing | Removed invalid or non-reportable records and standardised field formats |
| Data validation | Checked invoice status, balances, dates and payment fields before KPI calculation |
| Payment logic | Derived payment-delay fields from due dates, settlement dates and invoice status |
| Date modelling | Added a dedicated date dimension to support daily, weekly, monthly and yearly analysis |
| Credit data | Connected customer credit information with invoice activity for exposure and utilisation analysis |
| AR snapshot | Retained a separate overdue snapshot where current portfolio exposure required different reporting logic from invoice history |

This separation was important because historical invoice analysis and the latest AR position do not always operate at the same grain or reporting context.

---

## 🧮 DAX & Measure Design

The report uses a reusable DAX measure layer rather than embedding calculations directly into individual visuals.

Measures cover:

- invoiced revenue and settled value
- outstanding and overdue exposure
- collection performance
- credit utilisation
- paid invoice counts and values
- average and median paid days
- late-payment rates and values
- period-over-period movements
- customer contribution and portfolio shares

### Filter-context handling

A key modelling challenge involved the current overdue snapshot.

The AR snapshot is intentionally disconnected from the main invoice fact table because it represents a current-state view rather than transaction history.

`TREATAS` is used to pass the active customer context into the snapshot when current overdue exposure is required.

This allows the report to preserve a separate snapshot while still responding to customer-level analysis.

### Context-sensitive measures

DAX measures were also designed to respond correctly to report interactions.

For example, late-payment measures use preserved filter context so selecting a specific payment-timing category returns the customers and value associated with that category rather than recalculating across every late-payment bucket.

This distinction became important when moving from portfolio KPIs into invoice and customer-level investigation.

---

## ⚙️ Power BI Development

The report uses Power BI features to support analysis across multiple levels rather than static presentation.

| Feature | Purpose |
|---|---|
| Field parameters | Switch reporting grain between daily, weekly, monthly and yearly views |
| Synced slicers | Maintain consistent date, customer and reporting-grain selections |
| Cross-visual filtering | Move from KPI or payment category into the customers driving the result |
| Dynamic KPI context | Recalculate values and comparisons based on current report selections |
| Tabular Editor | Organise the measure layer and display folders for easier model maintenance |
| Tooltips | Add supporting invoice counts and contextual measures without overcrowding visuals |

---

## 💡 Analytical Design

The dashboard was structured so each view answers the next finance question rather than presenting isolated metrics.

### Receivables Performance

Starts with revenue, collections, outstanding balance and overdue exposure, then moves into trend and customer-level drivers.

### Credit Portfolio

Connects customer credit limits with outstanding and overdue exposure to identify utilisation and concentration risk.

### Payment Behaviour

Moves from overall payment value and lateness into payment-speed segments, timing distribution and customer-level payment risk.

This creates a reporting flow from:

**Performance → Exposure → Behaviour → Customer Driver**

rather than requiring users to interpret unrelated visuals independently.

---

## 🧠 Selected Modelling Decisions

Several measures required a distinction between metrics that appear similar but answer different questions.

**Current overdue vs invoice-period overdue**

Current AR exposure represents the latest portfolio position, while invoice-period analysis describes invoices issued within the selected reporting period. These were kept logically separate to avoid treating a current balance as a historical time-series measure.

**Average vs median paid days**

Average paid days provides an overall payment-speed indicator, while the median helps identify whether a small number of heavily delayed invoices are distorting the average.

**Late paid value vs paid value**

Late paid value measures the financial impact associated specifically with late settlement, whereas total paid value represents commercial activity. Keeping both concepts separate prevents high-value customers from automatically being interpreted as payment-risk customers.

---

## 🤖 AI-Assisted Development

AI tools were used selectively during development to support DAX debugging, challenge measure logic and review edge cases.

AI-generated suggestions were treated as development support rather than a source of truth. Measure behaviour was checked against the underlying finance data and expected filter context before being retained in the model.

No AI model is embedded in the production reporting pipeline.

---

## 🛠️ Tools & Skills Demonstrated

| Tool / Skill | Application |
|---|---|
| Power BI | Data modelling, report development and interactive analysis |
| Power Query / M | Data cleansing, transformation and derived reporting fields |
| DAX | Reusable measures, time intelligence and filter-context logic |
| Tabular Editor | Measure organisation and semantic-model maintenance |
| Data modelling | Combined transactional, dimensional, credit and snapshot reporting structures |
| Finance analytics | Receivables, collections, overdue exposure, credit utilisation and payment behaviour |
| Data validation | Reconciled KPI logic and investigated unexpected report behaviour |
| Stakeholder reporting | Converted finance data into management-level and customer-level views |
| AI-assisted analysis | Supported debugging and logic review with manual validation |

---

## ✅ What This Project Demonstrates

This project demonstrates my ability to:

1. Translate finance reporting requirements into a structured Power BI model
2. Clean and validate operational data before reporting
3. Build reusable DAX measures rather than visual-specific calculations
4. Handle different data grains and filter contexts within one semantic model
5. Distinguish current-state finance metrics from historical performance analysis
6. Debug measure behaviour through customer and visual-level interactions
7. Design dashboards around connected analytical questions
8. Translate portfolio-level movements into customer-level drivers
9. Maintain a structured measure layer for continued report development
10. Communicate finance performance to both analytical and non-technical users

---

## 🔐 Data Privacy

This dashboard was developed from real operational finance data.

The public portfolio version contains only an anonymised dashboard preview. Customer-identifying information has been removed, and no underlying operational dataset or customer-level source data is included in this repository.
