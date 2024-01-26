# pizza_sale_report
## Table of contents 
- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Data Cleaning](#data-cleaning)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
### Project Overview
This project seeks to provide meaningful insights from the sales performance from a pizza business for the year. During the analysis process trends were identified and data driven recommendations were provided so as to promote the future performance of the business and area of interest.

![ATMDashboard1](https://github.com/Abiatm/pizza_sale_project/assets/153201833/1f6cb211-b4db-489b-a42f-d37a10e18236)
![saleper](https://github.com/Abiatm/pizza_sale_project/assets/153201833/b75ef32b-e722-46c7-a54a-27c73ba30163)
![sizeper](https://github.com/Abiatm/pizza_sale_project/assets/153201833/542d373a-8d0e-47de-a83e-6e674d6835a9)

### Problem Statement
#### The problems that need to be addressed are:
- Total revenue, order and amount sold.
- Order trend by day and month.
- Revenue by pizza category, size and times of day.

### Data Source
The dataset used for this analysis is the pizza_sales_data file ,which shows the full details of the information about the pizza sales activities.
### Tools Used
- SQL - Data cleaning,Data munging
- PowerBi- Data validation,Data visualization
- Excel- Data cleaning,Data validation
- Dashboard Design- Data ink ratio
- Data Analysis- Extraction,wrangling and Exploration
 ### Data Cleaning
 #### List of things checked and evaluated where necessary before performing data exploration
 - Trimming of data
 - Removal of duplicates
 - Converting text to columns
 - Filtering of blank cells
 - cleaning operation
 - Use of left, right and medium functions where necessary
 - Use of upper, lower and proper where necessary
 ### Data Analysis
```SQL
1	SELECT sum(total_price)  as Total_Revenue FROM spizza.`pizza_sales_excel_file - copy`;
2	select sum(quantity) FROM spizza.`pizza_sales_excel_file - copy`;
3	select dayname(order_date) as name_of_day, count(distinct order_date) as occurance_rate from spizza.`pizza_sales_excel_file - copy`
group by name_of_day
order by field(name_of_day,'sunday','monday','tuesday','wednesday','thursday','friday','saturday');
4	select dayname(order_date) as name_of_day, count(distinct order_id) as occurance_rate from spizza.`pizza_sales_excel_file - copy`
group by name_of_day
order by field( name_of_day,'sunday','monday','tuesday','wednesday','thursday','friday','saturday');
5 select  monthname(order_date) as month_name, count(distinct order_id) as occurance_rate from spizza.`pizza_sales_excel_file - copy`
group by month_name
order by field(month_name ,'january','february','march','april','may','june','july','august','september','october','november','december');
6 select pizza_category,round(sum(total_price),2) as total_sale_amount,round(100*sum(total_price)/(select sum(total_price)from spizza.`pizza_sales_excel_file - copy`  ),2) as percentage_of_total_sale from spizza.`pizza_sales_excel_file - copy`
group by pizza_category;
7 SELECT * FROM spizza.`pizza_sales_excel_file - copy`;
update spizza.`pizza_sales_excel_file - copy`
set pizza_size = 'Medium' where pizza_size='M';
update spizza.`pizza_sales_excel_file - copy`
set  pizza_size='Small' where pizza_size = 'S';
update spizza.`pizza_sales_excel_file - copy`
set  pizza_size='More_extra_large' where pizza_size = 'XXL';
update spizza.`pizza_sales_excel_file - copy` 
set  pizza_size='Extra_large' where pizza_size = 'XL';
update spizza.`pizza_sales_excel_file - copy`
set  pizza_size='large' where pizza_size = 'L';
;
select pizza_size,round(sum(total_price),2) as total_sale_amount,round(100*sum(total_price)/(select sum(total_price)from spizza.`pizza_sales_excel_file - copy`  ),2) as percentage_of_total_sale from spizza.`pizza_sales_excel_file - copy`
group by pizza_size;
```
```
POwerBi
1 Sum_of_Revenue = sum('pizza_sales_excel_file - Copy'[total_price])
2 Sum_of_Revenue = sum('pizza_sales_excel_file - Copy'[total_price])
3 Total_order = DISTINCTCOUNT('pizza_sales_excel_file - Copy'[order_id])
4 Day_Abbrev = UPPER(LEFT('pizza_sales_excel_file - Copy'[Day Name],3))
5 maxss_value = 
VAR max_data_point= if(MAXX(ALL('Field Switch'[Field Switch]),Charts[Total_order])=3538,MAXX(ALL('Field Switch'[Field Switch]),Charts[Total_order]),BLANK())
VAR COLOR=
        IF (MAXX(ALL('Field Switch'[Field Switch]),Charts[Total_order])=3538,
             "Green",
              "DArk Yellow"
            )
RETURN
3538
6 Month_Abbrev = UPPER(LEFT('pizza_sales_excel_file - Copy'[Month Name],3))
7 MaxMonth = if(MAXX(ALL('pizza_sales_excel_file - Copy'[Month_Abbrev]),Charts[Total_order])=1935,MAXX(ALL('pizza_sales_excel_file - Copy'[Month_Abbrev]),Charts[Total_order]),BLANK())
8 MinDataPoint = if(MINX(ALL('Field Switch'[Field Switch]),Charts[Total_order])=2624,MINX(ALL('Field Switch'[Field Switch]),Charts[Total_order]),BLANK())
9 MinMonth = if(MINX(ALL('pizza_sales_excel_file - Copy'[Month_Abbrev]),Charts[Total_order])=1646,MINX(ALL('pizza_sales_excel_file - Copy'[Month_Abbrev]),Charts[Total_order]),BLANK())
```
### Results
The analysis results are summarized as follows:
1.	The sales order trend has shown an appreciable increase from the first day of week with a decrease on last day of the week and highest order on friday, lowest on Sunday.
2.	Classic pizza has the highest revenue generation with the size “large” at high demand during afternoon hours.
3.	The order trend by month has unstable increase as it fluctuates but with highest order on July and lowest order on october.

### Recommendations
Based on the obtained results from the analysis, the following recommendations are made:
1.	To obtain maximum revenue for the business, more investment and focus should be on the product, marketing, and promotion department with their operational demand to be high especially on Friday’s which has highest pizza demand rate.
2.	Production and processing department should focus on reducing production of pizza sizes such as extra large and more extra large as it has the least demand rate.
3.	Due to hot summer weather condition which makes pizza a convenient and refreshing option attracted more sales in July. More marketing and promotion should be adopted during this month yearly to improve revenue generation.


