# PROJECT-WORK-ON-D-LITE-ELECTRONICS-LTD
AINOW Bootcamp Capstone Project by Using Excel to clean, analyse and visualise for decision making.

### INTRODUCTION

After receiving the sales dataset of D-Lite Electronics Ltd, an initial review was conducted to understand its structure, content, and the level of inconsistencies present across the fields, from date entries to customer names. Due to noticeable data quality issues, a structured data cleaning and transformation process was required to ensure accuracy and reliability for analysis. To achieve this, a new worksheet was created where the raw data was systematically transformed into a clean, standardized format ready for analysis.

### Data Preparation and Transformation

A new worksheet was created and structured into thirteen (13) columns, namely: Raw Date, Day, Month, Year, Date, Region, 
Product, Category, Units Sold, Unit Price, Total Sales, Sales Rep, and Customer.

Under the Raw Date column, the following formula was applied to clean and standardize the date text by
removing unwanted characters and enforcing uniform text formatting:

=UPPER(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(CLEAN('RawData'!A1),"-","")," ",""),".",""))

For the Day column, two approaches were used. For dates with irregular month spellings, the formula
below was applied to correctly extract the day:

=TEXT(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE([@[RawDate]],"AMR","MAR"),"JNA","JAN"),"PAR","APR"),"D")
For the remaining records, a simpler extraction method was used:
=LEFT([@[Raw Date]],2)

The Month column followed a similar approach. For inconsistent month spellings, the formula below was used:
=TEXT(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE([@[RawDate]],"AMR","MAR"),"JNA","JAN"),"PAR","APR"),"MMM")

For other records, the month was extracted using:
=SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(MID([@[Raw Date]],3,3),"AMR","MAR"),"JNA","JAN"),"PAR","APR")

In the Year column, a validation rule was applied to ensure consistency by correcting any year that was not 2025:
=IF(YEAR(RIGHT([@[Raw Date]],4))<>2025,2025,0)

The Date column was then constructed by combining the Day, Month, and Year values:
=CONCAT(B2&"-"&C2&"-"&D2)

For the Region column, regional values were standardized using the following logic:

=IFS(LEFT(SUBSTITUTE('Raw Data'!B2," ",""),1)="s","South",

LEFT(SUBSTITUTE('Raw Data'!B2," ",""),1)="n","North",

LEFT(SUBSTITUTE('Raw Data'!B2," ",""),1)="e","East",

LEFT(SUBSTITUTE('Raw Data'!B2," ",""),1)="w","West")

The Product column was cleaned and formatted using:
=PROPER(CLEAN(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE('Raw Data'!C2," ",""),",",""),".","")))

For Category, products were grouped based on their prefixes using this formula:

=IFS(
LEFT(SUBSTITUTE('Raw Data'!D2," ",""),2)="pe","Peripherals",

LEFT(SUBSTITUTE('Raw Data'!D2," ",""),2)="au","Audio",

LEFT(SUBSTITUTE('Raw Data'!D2," ",""),2)="co","Computers",

LEFT(SUBSTITUTE('Raw Data'!D2," ",""),1)="e","Electronics",

LEFT(SUBSTITUTE('Raw Data'!D2," ",""),2)="mo","Mobile",

LEFT(SUBSTITUTE('Raw Data'!D2," ",""),2)="ph","Photography")

The Units Sold and Unit Price columns were directly referenced from the raw data.

Total Sales was calculated as:
=[@[Unit Price]] * [@[Units Sold]]

The Sales Representative names were standardized using:
=UPPER(TRIM(CLEAN(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE('Raw Data'!G2,",",""),".","")," ",""))))

For the Customer column, customer names were standardized using logical mapping based on text patterns 
to ensure uniform naming across the dataset.
=IFS(LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="M", "Musa Enterprrises",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="o", "Omega Wholesale",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),4)="Tola", "Tola Ventures", 

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="T", "Tope & Sons",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="z","Zainab Global",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),2)="Ma","Maryam Ltd",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="j","Jide Superstores",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="f","Femi Tech",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="k","Kelvin Tech",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="A","Adewale Stores",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),2)="Al","Alpha Retailers",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="b","Bright Solutions",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="c","Chika Mart",

LEFT(SUBSTITUTE('Raw Data'!H2," ",""),1)="e","Emeka Traders")

### Pivot Table Analysis
After cleaning and transforming the dataset, PivotTables were created by navigating to Insert → PivotTable, selecting New Worksheet, and confirming the selection.

The following analytical tables were created:
1.	Total Sales by Region
2.	Best-Selling Products
3.	Sales Performance by Sales Representative
4.	Total Sales by Category
5.	Units Sold by Sales Representative
6.	Region with the Highest-Selling Products
7.	Percentage Contribution of Products within Each Category
8.	Top Five Customers by Total Sales

### Dashboard Development
A separate worksheet was created for the Dashboard. 
Visual charts were developed from the PivotTables and enhanced with slicers, 
enabling dynamic filtering particularly by Product Category to support interactive 
analysis and management decision-making.

### CONCLUSION
Through a structured and methodical approach, 
the raw sales data was successfully cleaned, standardized, and transformed into an analysis-ready dataset.

The use of Excel formulas ensured data consistency, while PivotTables and dashboards enabled meaningful insights 
into sales performance across regions, products, categories, and sales representatives. 

This process not only improved data accuracy but also provided management with a clear, interactive view of sales trends, 
performance drivers, and customer contributions, thereby supporting informed business decision-making.


