# Supply Chain Bottleneck Analysis Project

**Category:** Business & Supply Chain Analytics  
**Tools Used:** Python, SQL, Qlik Cloud Analytics  
**Dataset Size:** 100 (original csv) and 10,100 (after python generation) rows respectively (Refer to project write up)

## 📌 Project Overview

## 📄 Full Project Write-UP/Report
<p>
  <strong>SUPPLY CHAIN PERFORMANCE &amp; BOTTLENECK ANALYSIS: A DATA-DRIVEN APPROACH</strong>
</p>
<p>
  PROJECT GOAL: To identify inefficiencies, assess quality, and optimize operational processes within a simulated product supply chain by transforming raw data into actionable insights and strategic recommendations.
</p>

<details>
  <summary><strong>Read more...</strong></summary>
  <p>
    This project focused on conducting a comprehensive Supply Chain Performance and Bottleneck Analysis to identify inefficiencies, assess quality, and optimize operational processes within a simulated product supply chain. The primary goal was to transform raw supply chain data into actionable insights, enabling data-driven decision-making for improved efficiency and reduced costs. This project demonstrates an end-to-end analytical workflow, from data preparation and engineering to advanced visualization and strategic recommendations.
  </p>
  <h4>Data Acquisition &amp; Augmentation</h4>
  <p>
    The project began with a small, initial dataset downloaded from Kaggle in a CSV format (supply_chain_data.csv), containing 100 rows of various supply chain metrics. To ensure the analysis was robust and representative of real-world scenarios in a large company, I decided that it was crucial to work with a larger volume of data. I used Gemini to help me create a python script to run in VS code to generate 10,000 more rows of similar data consistent with that of the original dataset.
  </p>
  <h4>Data Augmentation using Python</h4>
  <p>
    This script analyzed the patterns, ranges, and categorical distributions within the original 100 rows and then generated 10,000 additional, random rows that adhered to these learned characteristics. This process resulted in a significantly expanded dataset of 10,100 rows (LargerSuppyChainData.csv) therefore providing a more realistic foundation for analysis.
  </p>
  <h4>Data Preparation &amp; Feature Engineering in MySQL Workbench</h4>
  <p>
    The augmented dataset was then loaded into MySQL Workbench. I then started the data preparation and feature engineering process which was performed directly within the database environment using SQL queries.
  </p>
  <h4>Key SQL Transformations &amp; Engineered Features:</h4>
  <p>
    Total_Cost and Gross_Margin Calculation: New columns were added to the table. Total_Cost was calculated as the sum of Manufacturing costs and Shipping costs. Gross_Margin was calculated using the formula (Revenue generated - Total_Cost) / Revenue generated * 100, providing a key profitability metric.
  </p>
  <p>
    Total_Lead_Time: A new column was created by summing Lead time, Manufacturing lead time, and Shipping times to represent the overall duration of the supply process.
  </p>
  <p>
    Cost_Category Binning: A Cost_Category column was created to segment Total_Cost into categorical ranges like 'Low-Cost', 'Mid-Range', and 'High-Cost', enabling easier analysis and visualization.
  </p>
  <p>
    Rounding Numerical Values: Many of the Columns such as Gross_Margin and Shipping costs were rounded to two decimal places using the ROUND() function for improved readability and presentation in the dashboard.
  </p>
  <p>
    This rigorous SQL-based preparation ensured data quality and created a rich foundation for deeper analytical insights.
  </p>
  <h4>Data Loading &amp; Transformation in Qlik Sense</h4>
  <p>
    The cleaned and engineered dataset from MySQL was then loaded into Qlik Sense. A crucial transformation was performed directly within the Qlik Sense Data Load Editor to prepare the data for bottleneck analysis.
  </p>
  <h4>Unpivoting Time Metrics using CROSSTABLE</h4>
  <p>
    To effectively visualize the average time for each stage of the supply chain (Lead times, Manufacturing lead time, Shipping times) in a single bar chart, the data needed to be "unpivoted." The CROSSTABLE function was used for this in the Qlik Sense script. This transformed the columns Lead times, Manufacturing lead time, and Shipping times into two new columns:
  </p>
  <p>
    Metric_Name: Containing the names of the original time columns (e.g., 'Lead times', 'Manufacturing lead time').
  </p>
  <p>
    Metric_Value: Containing the corresponding time values.
  </p>
  <p>
    A new table named BottleneckData was created, which is perfectly structured for a bar chart comparing average times across different stages.
  </p>
  <h4>Overcoming Scripting Challenges:</h4>
  <p>
    This process involved iterative debugging and diagnosing with Gemini and ChatGPT to refine the Qlik Sense load script:
  </p>
  <p>
    Initial FROM (csv) errors: Resolved by using the explicit (txt, utf8, embedded labels, delimiter is ',') format.
  </p>
  <p>
    Unexpected token: 'Set' errors: Addressed by ensuring the script was placed in a new, clean section of the Data Load Editor, preventing interference from Qlik's auto-generated code.
  </p>
  <p>
    Table not found errors: Resolved by ensuring the CROSSTABLE function correctly referenced the loaded data, demonstrating robust data loading practices.
  </p>
  <h4>Qlik Sense Dashboard Development &amp; Visualizations</h4>
  <p>
    The core of the project's output is an interactive Qlik Sense dashboard titled "Supply Chain Performance &amp; Bottleneck Analysis." This dashboard is designed to provide quick, actionable insights into key operational areas, enabling stakeholders to understand performance, identify issues, and drive improvements.
  </p>
  <h4>Key Dashboard Components &amp; Insights:</h4>
  <p>
    Executive Summary KPIs:
  </p>
  <ul>
    <li><strong>"Estimated Cost of Defect":</strong> Provides a high-level financial impact of quality issues, making the business case for improvements clear.</li>
    <li><strong>"Avg Shipping Time (Days)":</strong> Shows the overall efficiency of product delivery.</li>
    <li><strong>"Avg Cycle Time Per Order":</strong> Quantifies the end-to-end duration of a typical order, providing a high-level view of process efficiency.</li>
    <li><strong>"Percent of Inspections Failed":</strong> A critical quality metric that highlights the proportion of products failing inspection.</li>
  </ul>
  <p>
    These KPIs offer an at-a-glance overview of critical supply chain health metrics for quick executive review.
  </p>
  <p>
    Summary of Key Findings (Text Box):
  </p>
  <p>
    This text box acts as a clear executive summary, directly stating the most important insights derived from the data.
  </p>
  <ul>
    <li><strong>"Average Lead Time by Supply Chain Stage" (Bar Chart):</strong> Visually compares the average duration of each key stage in the supply chain process (Manufacturing lead time and Shipping times). Directly identifies the primary bottleneck. In this analysis, "Manufacturing lead time" was clearly identified as the longest stage, indicating a critical area for process optimization.</li>
  </ul>
  <p>
    "Supplier Performance" (100% Stacked Bar Chart):
  </p>
  <p>
    Displays the percentage breakdown of inspection results (Fail, Pass, Pending) for each supplier. Crucially highlights suppliers with a higher proportion of failed or pending inspections, enabling targeted supplier management and quality improvement initiatives. This chart is crucial for assessing supplier reliability.
  </p>
  <ul>
    <li><strong>"Product Quality Performance" (Bar Chart):</strong> Compares the average defect rates across different Product type categories (e.g., Cosmetics, Haircare, Skincare). Identifies specific product categories with higher defect rates, prompting investigation into their manufacturing processes, materials, or design. For instance, "Haircare" products were identified as having a higher average defect rate.</li>
    <li><strong>"Carrier Performance: Shipping Time vs Cost" (Scatter Plot):</strong> Visualizes the trade-off between average shipping time and average shipping costs for different Shipping carriers. Aids in strategic decision-making for carrier selection, allowing businesses to choose carriers that align with their priorities (e.g., lowest cost, fastest delivery, or a balance).</li>
  </ul>
  <p>
    The entire dashboard is interactive, allowing users to click on any element (e.g., a specific supplier, a product type) to filter all other charts and explore related insights.
  </p>
  <h4>Key Insights &amp; Business Recommendations</h4>
  <p>
    The comprehensive analysis, as summarized on the dashboard, revealed several critical areas for supply chain optimization:
  </p>
  <p>
    Manufacturing Bottleneck: The consistently long "Manufacturing lead time" indicates a need for process re-engineering, automation, or resource optimization within the manufacturing stage.
  </p>
  <p>
    Recommendation: Investigate manufacturing processes for inefficiencies. This could involve process mapping, Lean Six Sigma methodologies, or technology upgrades to reduce production time.
  </p>
  <p>
    Target Haircare Quality: The higher defect rates in "Haircare" products, as shown in the "Product Quality Performance" chart, require a focused investigation into their specific production lines, material sourcing, or design.
  </p>
  <p>
    Recommendation: Conduct a root cause analysis for haircare product defects. This might involve reviewing raw material quality, manufacturing line issues, or packaging processes specific to haircare.
  </p>
  <p>
    Proactive Supplier Management: The "Supplier Performance" chart highlights which suppliers have the highest percentages of failed or pending inspections.
  </p>
  <p>
    Recommendation: Implement a supplier performance review program. Engage with high-failure-rate suppliers to address quality issues, consider alternative suppliers, or adjust order volumes based on performance. Address "Pending" inspections promptly to avoid potential hidden quality problems.
  </p>
  <p>
    Strategic Carrier Selection: The cost-time trade-offs among carriers, as visualized in the "Carrier Performance" scatter plot, enable informed decisions for optimizing delivery based on urgency and budget.
  </p>
  <p>
    Recommendation: Optimize carrier selection based on specific shipment needs. For urgent deliveries, a faster (potentially more expensive) carrier might be chosen, while for less time-sensitive shipments, a lower-cost carrier could be preferred.
  </p>
  <h4>Conclusion</h4>
  <p>
    This project leveraged data analytics to provide a holistic view of supply chain performance. By cleaning and engineering features in MySQL, augmenting the dataset with Python, and building an interactive dashboard in Qlik Sense, key bottlenecks and quality issues were identified. This was then translated from complex data into clear, actionable insights and strategic recommendations.
  </p>
</details>

## 📊 Deliverables

- ✅ Live Qlik Dashboard - https://gblqb7f3bd41gee.us.qlikcloud.com/sense/app/8c2a9ae7-b420-4f8b-8fcf-3611a5b03eae/sheet/hejCP/state/analysis
- ✅ Project WriteUp/Report -
- ✅ Dataset Cleaned and Engineered in MySQL Workbench -

## 📄 Additional Files

- SQL Script-
- Original Dataset-
- Python Script-
- Post Python Larger Dataset-
  
---

<p align="center">
  <small>© 2025 Rennie Crookston | Built with GitHub Pages & Jekyll</small>
</p>


