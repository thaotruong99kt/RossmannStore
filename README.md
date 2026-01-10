# Rossmann Retail Performance: Trends, Seasonality, and Promotions

**1. Project Overview**
* This project analyzes the historical sales of 1,115 Rossmann stores. The primary objective is not only to clean the data but also to analyze store behavior, the effectiveness of promotions, the impact of competitors, and the influence of holidays.
* The project delivers actionable insights and strategies for marketing optimization.

**2. Business Questions**
* Macro Trend: How do sales revenues change over time, and what is the seasonal pattern?
* Store Performance: Which store model performs the best? Which stores are underperforming?
* Promotion Strategies: How do promotions affect different types of stores?
* External Impact: How do competitors and holidays affect customer behavior?

**3. Dataset Overview and Processing Pipeline**
* The analysis is based on two primary datasets:
  * train.csv: Historical sales data including Sales, Customers, Open status, Promotions, and Holidays.
  * store.csv: Metadata for every store, including Store Type, Assortment, and Competition Distance.

**Data Cleaning**
* Handle logic errors: Identify rows with Open=1 but Sales=0. Corrected these entries to Open=0.
* Handle missing values:
  * CompetitionDistance: Imputed missing values using the Median (due to the right-skewed distribution and significant outliers). <img width="1370" height="450" alt="image" src="https://github.com/user-attachments/assets/b8866dea-0a90-4e9e-b24f-3c608b8e3e85" />
  * CompetitionOpenSinceMonth/Year: Created a missing flag column to preserve information.
* Data Type Conversion: Converted specific columns (Date, StateHoliday) to the correct formats.

**4. Feature Engineering**
* Competition Timeline: Calculated MonthsSinceCompetitionOpen (Months elapsed since the nearest competitor opened).
* Promo2 Timeline: Calculated WeeksSincePromo2Start (Weeks elapsed since the store joined Promo2).
* Calendar Features: Extracted Year, Month, Week, and IsWeekend.
* Business Metrics:
  * AvgBasket: Calculated the average transaction value per customer.
  * OpenDayFlag: Created a flag for actual trading days (Filtered OpenDayFlag=1 for the entire analysis process).
  * DistanceBand: Grouped competitor distances into categorical bands (e.g., <500m, >5km).
    
**5. Executive Summary**
* Here is an overview of key factors driving sales and potential risks of the business:
* Financial Health: Overall sales are growing steadily each year. There is a strong seasonal trend, with sales peaking in December.
* Growth Drivers:
  * Promotions: This is the main tool to boost demand. On average, promotions increase sales by +38.8% compared to normal days.
  * Store Type: Although there are few StoreType 'b' locations, they are highly effective. Their average sales are 1.5 to 2 times higher than other store models.
* Risks & Challenges:
  * Competition: New competitors opening within 500 meters cause sales to drop by about 9%.
  * Performance: About 45% of stores show a negative growth trend. Although the decline is slow, this is an early warning sign that needs action.
  * Underperformance Group: A specific group of stores has low sales and unstable performance. These stores are reducing the overall efficiency of the chain.

**6. Key Analysis & Visualization**
**6.1 Macro Trends**
<img width="1362" height="444" alt="image" src="https://github.com/user-attachments/assets/af340637-2d26-4de9-853a-8a5fd5e0789c" />
* Line Chart with Range Slider: Used a Rolling Mean (30 days) to smooth the trend and exclude daily noise.
* The chart clearly shows annual seasonality with a peak in revenue occurring in December (Christmas Peak). 

**6.2 Micro Seasonality (Heatmap - Month x Weekdays)**
<img width="1366" height="446" alt="image" src="https://github.com/user-attachments/assets/82fcb17a-38f6-4a00-9f32-047186edfdfd" />

* Visualized customer behavior and sales trends. Weekends and year-end months are the Hotspots for sales revenue. 

**6.3 Store Performance**
<img width="1364" height="445" alt="image" src="https://github.com/user-attachments/assets/e6bc28c2-49d8-480e-905a-2270ec3190ca" />

* StoreType 'b' generates the highest revenue, approximately 1.5x higher than other types. Meanwhile, StoreType 'a' and 'd' show lower efficiency and perform similarly. 

<img width="897" height="696" alt="image" src="https://github.com/user-attachments/assets/2d0bc2e5-1ac5-41a3-b5af-b3d40aeb7d39" />

* There is a clear differentiation. "Stars" exhibit stable activities and high revenue. In contrast, "Underperformers" (accounting for ~15-20% of total stores) face low sales with high volatility. Operational audits are recommended for this group to identify root causes. 

<img width="944" height="225" alt="image" src="https://github.com/user-attachments/assets/636a1638-e554-47cb-8ba5-2d676a5bec7b" />

* The sales gap between the Top 50 and Bottom 50 stores stems mainly from Traffic (2.3x gap), while the Basket Size gap is minimal (1.1x). The issue for underperforming stores likely lies in Location or Marketing strategy, not upsell capability. 

<img width="994" height="785" alt="image" src="https://github.com/user-attachments/assets/c35e373b-d571-4d6d-9740-8374465b3e03" />

* Small stores (Types 'a', 'c') are dependent on promotions, with sales surging over 40% during discounts. In contrast, large stores (Type 'b') have strong organic sales and are less sensitive to promotions. For the action plan, cut the promotion budget for Type 'b' and reallocate resources to small stores to optimize ROI.
  
<img width="695" height="497" alt="image" src="https://github.com/user-attachments/assets/5b375589-12cd-43fb-8669-c8eb91a01f22" />

* Promo2 participants have lower baseline sales (smaller scale) but achieve higher uplift during promotions (+43% vs 39%). In conclusion, Promo2 should be maintained as a support tool, specifically for weaker stores to stabilize sales. Do not force stores to participate.  

**6.4 Context & Environment**

**Competition Impact by Distance (Bar chart)**
<img width="896" height="497" alt="image" src="https://github.com/user-attachments/assets/d225b783-88a5-4448-9432-aaf0eea4986c" />
* Competitors opening within a < 500m radius cause the most significant loss (~9% of total sales). At distances > 5km, there is almost no impact.
* Avoid opening stores in areas with high competitor density (<500m) unless the store possesses a unique competitive advantage.
  
**Holiday Stock-up Effect**
<img width="897" height="497" alt="image" src="https://github.com/user-attachments/assets/4e516bb9-a596-410b-9850-bba3331ef4fb" />

* Peak sales consistently occur 3-4 days before a holiday. When the school holiday starts, sales decrease immediately. Therefore, logistics should prioritize high stock levels for the T-4 period.
  
<img width="894" height="495" alt="image" src="https://github.com/user-attachments/assets/1e9cc789-1725-4e47-a59f-fbae5794abfc" />

**7. Tools & Libraries**
* Python: Core programming language.
* Pandas: Data manipulation, cleaning, and merging.
* Plotly: Interactive data visualization and dynamic plotting.
