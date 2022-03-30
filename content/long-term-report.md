


**Review key metrics with scorecard reports-long term report**

Microsoft Dynamics 365 Fraud Protection provides long term report for purchase protection. You can use them to review your key metrics and understand the performance of your fraud protection efforts for historical transactions over 6 months old.

Your top key performance indicators (KPIs) are summarized across the top of the scorecard page to provide a snapshot of your fraud protection performance. You can use the charts on the page to drill down and fully investigate the metrics.  

The purchase protection long-term report is updated with the latest transactional data every 24 hours. The time stamp on the report shows the update time in Coordinated Universal Time.

Users can switch views between count view and amount view. Count view shows volume and percentage by transaction count and amount shows volume and percentage in US dollars.

The machine learning model in Fraud Protection evaluates every transaction by using advanced adaptive AI and then assigns a risk score. The higher the risk score, the higher the perceived risk. The machine learning model uses a range of risk scores from 0 (zero) through 999.

**User filters in long term report**

You can use the drop-down menus and sliders on the report to filter your view of the interactive charts. The following filter options are available:

- **PI type** This filter includes payment instrument types such as card type.

- **Product type** – You can filter at product type. IP country/region – Country/region based on IP address.

- **Date range** – Use this filter to show transaction data by date. You can select dates in the calendar, enter dates manually, or select date ranges.

- **Score range:** use the input or scroll bar to select desired score range from 0 to 999, incremental of 10.

- **Non-fraud type** – You can filter by non-fraud label. The non-fraud label might include bank approved, merchant approved, and other labels previously provided by you. Changing this will impact denominator for the calculation of fraud rate.

- **Fraud type** – You can filter by fraud label. The fraud label include chargebacks, refunds, merchant rejected, and other labels previously provided by you. Changing this will impact fraud volume and numerator for the calculation of fraud rate.

To clear specific filter selections, hover over the category name, and then select the **Clear selections** button (eraser symbol). To reset all filters to the default options, select **Reset**.

**Key performance indicators**

The scorecard provides the following key performance metrics:

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Manual review rate** – Out of the total volume of purchases, this chart shows the percentage that was sent by rules for manual review.

- **Rule rejected rate** – Out of the total volume of purchases, this chart shows the percentage that was rejected by rules.

- **Bank acceptance rate –** percentage of transactions approved by bank among transactions sent to bank.

- **Chargeback received** –total volume of chargebacks received within the given date range.

- **Fraud volume** –total volume of transaction labeled as fraud in fraud type filter.

- **Fraud rate** – percentage of transactions labeled as fraud in fraud type filter, among total transactions labeled as fraud or non-fraud.

- **Average score** – Average score of total transactions.

**KPI charts**

The KPI charts provide details about the following key performance metrics. Users can switch date granularity between daily, weekly, or monthly views of your data.

- **Transaction volume** – This chart shows the total count or number of transactions that were sent for assessment.

- **Rule rejected rate** – Out of the total volume of purchases, this chart shows the percentage that was rejected by rules.

- **Bank acceptance rate –** percentage of transactions approved by bank among transactions sent to bank.

- **Fraud rate** – percentage of transactions labeled as fraud in fraud type filter, among total transactions labeled as fraud or non-fraud.

- **Score distribution** –transaction volume distribution by risk score, incremental by 10. Users can switch between chart layout or table layout.

