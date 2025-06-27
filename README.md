📉 Layoffs Dashboard (2022–2025)

   🔍 Overview
   This interactive Layoffs Dashboard provides a detailed analysis of global tech and non-tech company layoffs from 2022 to 2025. It helps users understand trends, identify impacted industries, and explore layoffs by company, location, and time period.

The project was built using Power BI for data visualization and SQL for data processing and querying.

🛠️ Tools & Technologies
   Power BI – For designing interactive dashboards and visualizations
 
   Microsoft Excel / CSV – For raw data storage and manipulation

   SQL (MySQL / PostgreSQL) – For data cleaning and querying

📊 Key Features
Year-wise Layoff Trends (2022–2025)

Top Companies with Most Layoffs

Industry-wise Breakdown

Layoffs by Country & Continent

Company Status (Closed vs Active)

Employee Count Affected Over Time

Interactive Filters for year, industry, location, and company

useful DAX queries 

📌 1. Total Layoffs

 dax
 Copy
 Edit
     
            Total Layoffs = SUM('Layoffs'[Total Laid Off])

📌 2. Total Layoffs by Year

  dax
  Copy
  Edit
  
             Total Layoffs by Year = 
             CALCULATE(
             [Total Layoffs],
            ALLEXCEPT('Layoffs', 'Layoffs'[Year])
            )

📌 3. Percentage Laid Off (Company-wise)

 dax
 Copy
 Edit
     
     % Laid Off = 
     DIVIDE('Layoffs'[Total Laid Off], 'Layoffs'[Total Employees]) * 100
     Use this if your dataset includes a column like Total Employees.

📌 4. Year-over-Year Change in Layoffs

dax
Copy
Edit
     
      YoY Change = 
      VAR CurrentYear = SELECTEDVALUE('Layoffs'[Year])
      VAR PreviousYear = CurrentYear - 1
      VAR CurrentValue = [Total Layoffs]
      VAR PreviousValue = 
       CALCULATE(
         [Total Layoffs],
         'Layoffs'[Year] = PreviousYear
       )

RETURN
   
      DIVIDE(CurrentValue - PreviousValue, PreviousValue) * 100
    
📌 5. Top 5 Companies by Layoffs
     
You can use the filter in Power BI visuals:

Use a bar chart with Company as axis and Total Layoffs as value.

Add Top N filter → Top 5 by Total Layoffs.

Alternatively, a calculated table:

dax
Copy
Edit

    Top 5 Companies = 
    TOPN(
      5,
       SUMMARIZE('Layoffs', 'Layoffs'[Company], "Layoffs", [Total Layoffs]),
      [Layoffs],
      DESC
    )

📌 6. Layoffs Trend Over Time (Monthly)

 dax
 Copy
 Edit

          Monthly Layoffs = 
           CALCULATE(
          [Total Layoffs],
         ALLEXCEPT('Layoffs', 'Layoffs'[Month], 'Layoffs'[Year])
      )


Make sure you have a proper Date table with Year-Month columns to use in visuals.


📌 7. Total Layoffs by Country

dax
Copy
Edit

          Total by Country = 
          CALCULATE(
         [Total Layoffs],
         ALLEXCEPT('Layoffs', 'Layoffs'[Country])
      )

  
📌 8. Count of Companies Closed

 dax
 Copy
 Edit
 
         Closed Companies = 
         CALCULATE(
        DISTINCTCOUNT('Layoffs'[Company]),
        'Layoffs'[Status] = "Closed"
       )

📌 9. Average Layoffs per Company

  dax
 Copy
 Edit
 
           Avg Layoffs per Company = 
           DIVIDE(
          [Total Layoffs],
          DISTINCTCOUNT('Layoffs'[Company])
        )

📌 Insights & Observations

Peak layoffs occurred in early 2023, especially in tech startups.

USA, India, and Germany were among the top impacted countries.

SaaS and FinTech sectors faced the most cuts.

Majority of layoffs occurred during funding slowdowns and economic uncertainty post-COVID.

🧠 Learning Outcomes
    
  Gained experience in data preprocessing, visual analytics, and dashboard design.

  Improved skills in SQL query writing, data storytelling, and trend analysis.

  Practiced using DAX for advanced calculations in Power BI.

📌 How to Use

   Open the Power BI .pbix file in Power BI Desktop.

   Connect to the dataset or use the included one.

  Interact with the filters to explore different trends and visualizations.

🤝 Credits 
  
Data Source: Layoffs.fyi / Custom Compiled

Project by: Reshma Pun

Tools: Power BI, SQL
