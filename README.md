# The Cost of Failed Transactions: Power BI Analysis

**Zion Tech Hub Finance Data Challenge** | Analysis by **Lucky Justice Nelson**, Business Analyst

I analysed 28 months of East African transaction data (January 2022 to April 2024) to find out why most of the fee revenue never reaches the business, what happened in January 2024, and how much of it could realistically be recovered.

## The business question
Out of $3.15M in transaction fees, $2.85M (90%) was in payments that failed. The challenge asked me to:
1. Find where the failures concentrate and separate technical causes from behavioural ones.
2. Explain the January 2024 spike and say whether it is a one-off or the start of a trend.
3. Size a realistic recovery and recommend where to act first.

## Data
- 62,684 transaction rows, 5,657 customers, five markets: Kenya, Uganda, Ghana, Tanzania and Zambia.
- Customer sign-up records and daily exchange rates to convert fees to USD.
- The dataset belongs to Zion Tech Hub and is not included in this repository.

## What I found
- **Card is the main problem.** It is 23% of attempts but 77% of fee revenue, and 93.8% of that revenue failed. Mobile money fails 77.4%.
- **It is not one market.** Card fails 88% to 96% in every country.
- **Payment size matters.** Failure goes from 39% to 54% below $20 per payment, then 85% from $20 to $100 and 94% above $100.
- **Four accounts matter a lot.** Accounts 49957, 47087, 51026 and 49477 hold $1.05M (37%) of the failed revenue and fail almost every time.
- **January 2024 was an account event.** Failed fees hit $746K, about 9.6 times the earlier six-month average of $78K. Those four accounts caused 88% of it. Without them the failure rate stayed near 80%, the same as every month since October 2023. The same accounts also explain about 72% of December 2023 and April 2024.
- **Realistic recovery is about $110K, up to about $397K.** That is closing half of the gap between card and mobile money, without the four accounts. It is not the full $2.85M.

## What I recommend
1. **Fix card first.** Check gateway routing, issuer declines, 3-D Secure and the limits on payments above $20.
2. **Speak to the four accounts.** Find out whether the cause is limits, wrong details, KYC blocks or test traffic.
3. **Monitor and steer.** Record a failure reason for every failed payment, flag accounts that go above three times their own six-month average, and offer bank transfer or mobile money for large payments.

## Dashboards
**Page 1: where the failures are**

![Page 1](dashboards/page1_where_failures_concentrate.png)

**Page 2: the January 2024 spike**

![Page 2](dashboards/page2_january_2024_spike.png)

**Page 3: recovery and where to act first**

![Page 3](dashboards/page3_recovery_and_actions.png)

## How I built it
- **Power Query:** cleaned the data, merged the exchange rates on month and currency, and converted fees to USD at the rate on the first day of each month. 231 rows (under 0.5%) are in currencies with no rate in the file. They count in the failure counts but their fees could not be converted.
- **Data model:** a star schema with one fact table and customer, date and channel dimensions.
- **DAX:** around 40 measures for failure rates, the January bridge, concentration and the recovery scenarios. They are in [`dax/`](dax/DAX_Measures_and_Calculated_Columns.txt).
- **Limit:** the data has no failure-reason field, so I read technical versus behavioural causes from the patterns.

## Files
| Folder | What is in it |
|---|---|
| `report/` | The written report (PDF) with the three dashboards |
| `dashboards/` | Images of the three Power BI pages |
| `dax/` | All measures and calculated columns |
| `powerbi/` | The Power BI file |

## Contact
Lucky Justice Nelson | [LinkedIn](https://linkedin.com/in/justice-analyst) | [GitHub](https://github.com/JusticeAnalyst) | justicelucky436@gmail.com
