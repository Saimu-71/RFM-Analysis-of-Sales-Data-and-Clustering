# 📊 RFM Analysis of Sales Data and Clustering  

This project focuses on **RFM Analysis** (Recency, Frequency, Monetary) for clustering customers and analyzing sales data. It involves calculating RFM scores, creating customer categories (Silver, Gold, Diamond), and visualizing these insights through an interactive Power BI dashboard.  

---

## 🛠️ **Project Purpose**  
- Identify and segment customers based on their purchase behavior.  
- Understand sales trends and identify key customer groups.  
- Provide actionable insights to improve business strategies.  

---

## 📋 **Key Features**  

### 🔹 **Data Overview**  
**Key Columns**:  
- Invoice No, Description, InvoiceDate, CustomerID, Country  
- Total Amount, Recency, Frequency, Monetary  
- AverageRFMScore, AverageRFMScore(bins), CustomerCategory  

### 🔹 **Calculations and DAX Formulas**  

1. **Recency**: Number of days since the last purchase.  
    ```DAX  
    Recency =  
    VAR LastPurchaseDate =  
        CALCULATE(MAX('OnlineRetail'[InvoiceDate]), ALLEXCEPT('OnlineRetail', 'OnlineRetail'[CustomerID]))  
    RETURN  
        DATEDIFF(LastPurchaseDate, TODAY(), DAY)
    ```  

2. **Frequency**: Total number of purchases made by the customer.  
    ```DAX  
    Frequency =  
    CALCULATE(COUNT('OnlineRetail'[Invoice No]), ALLEXCEPT('OnlineRetail', 'OnlineRetail'[CustomerID]))
    ```  

3. **Monetary**: Total amount spent by the customer.  
    ```DAX  
    Monetary =  
    CALCULATE(SUM('OnlineRetail'[Amount]), ALLEXCEPT('OnlineRetail', 'OnlineRetail'[CustomerID]))
    ```  

4. **AverageRFMScore**: Weighted average of normalized Recency, Frequency, and Monetary values.  
    ```DAX  
    AverageRFMScore =  
    ( 'OnlineRetail'[NormalizedRecency] +  
      2 * 'OnlineRetail'[NormalizedFrequency] +  
      3 * 'OnlineRetail'[NormalizedMonetary] ) / 5
    ```  

5. **CustomerCategory**: Categorizes customers into Diamond, Gold, and Silver based on RFM scores.  
    ```DAX  
    CustomerCategory =  
    SWITCH(  
        TRUE(),  
        'OnlineRetail'[AverageRFMScore] >= 0.6, "Diamond",  
        'OnlineRetail'[AverageRFMScore] >= 0.3 && 'OnlineRetail'[AverageRFMScore] < 0.6, "Gold",  
        'OnlineRetail'[AverageRFMScore] < 0.3, "Silver"  
    )
    ```  

### 🔹 **Dashboard Features**  
1. **Customer Segmentation**: Visualize customer clusters (Silver, Gold, Diamond) using slicers.  
2. **Insights on Sales and Customers**:  
   - Total sales, recency, frequency, monetary values.  
   - Top 3 buyers by monetary value.  
   - Key customer characteristics (e.g., highest frequency, lowest recency).  
3. **Trends and Metrics**:  
   - Ribbon charts for normalized Recency, Frequency, and Monetary values against RFM scores.  
   - Column charts to display customer distribution across bins.  
4. **Time-based Analysis**: Sum of monetary values plotted by month.  

---

## 📊 **Visualizations Used**  
- Cards, Column Charts, Clustered Column Charts  
- Ribbon Charts, Slicers, Gauge Maps  
- Count and Average-based visualizations  

---

## 🚀 **Future Enhancements**  
- Automate updates for the latest customer data.  
- Implement machine learning for predictive analytics.  


# 📊 Sales Performance Analysis Dashboard  

This project features a **Power BI dashboard** that analyzes the sales performance of a retail company. It offers actionable insights through dynamic visualizations, helping businesses track growth in sales and profit across various dimensions, including product, category, subcategory, country, region, sales representative, and date intervals.  

---

## 🛠️ **Project Purpose**  
The purpose of this dashboard is to provide a one-page visual representation of sales insights to:  
- Monitor sales trends and performance metrics.  
- Identify profitable products, categories, and regions.  
- Enable data-driven decisions for improving sales strategies.  

---

## 📋 **Key Features**  

### 🔹 **Data Sources**  
- **Sales Data**: Folder containing yearly sales files (CSV format).  
- **Categories**: Excel file.  
- **Geography**: Excel file.  
- **Products**: Database/CSV.  
- **Sales Representatives**: Excel file.  
- **Subcategories**: Excel file.  

### 🔹 **Data Loading and Transformation**  
- A **resilient mechanism** to load all yearly sales files into a single fact table:  
  - Automatically incorporates new yearly files upon refresh.  
  - Handles missing files without errors.  
- Transformed the **Location** column by splitting **Country** and **City** to enable Geo maps.  
- Updated and formatted date fields to ensure proper usage in visuals.  
- Created a unique **GeoKey** by hashing and combining **Country** and **City** to connect Sales and Geography tables.  

### 🔹 **DAX Calculations**  

1. **Total Revenue**:  
    ```DAX  
    Total Revenue = Sales[Units] * Product[Retail Price]
    ```  

2. **Total Cost**:  
    ```DAX  
    Total Cost = Sales[Units] * Product[Standard Cost]
    ```  

3. **Gross Profit**:  
    ```DAX  
    Gross Profit = [Total Revenue] - [Total Cost]
    ```  

4. **GeoKey**:  
    ```DAX  
    GeoKey = CONCATENATE(Sales[Country], Sales[City])
    ```  

---

## 📊 **Dashboard Highlights**  
1. **Sales Performance Overview**:  
   - Key metrics like total revenue, gross profit, and total sales at a glance.  
2. **Monthly Trends**:  
   - Dynamic column charts showcasing monthly performance, sorted from January to December.  
3. **Regional Insights**:  
   - Geo maps and pie charts display performance by country and region.  
4. **Category and Product Analysis**:  
   - Detailed comparison of sales across categories, subcategories, and individual products.  
5. **Profitability Analysis**:  
   - Waterfall charts highlighting the breakdown of gross profit.  

---

## ⚡ **Technologies Used**  
- **Power BI**: Data modeling, DAX, and visualization.  
- **Power Query**: Data cleaning and transformation.  
- **DAX Functions**: For calculated columns and measures.  
- **Data Sources**: SQL databases, Excel sheets, CSV files.  

---

## 📚 **Key Learnings**  
- **Efficient Data Preprocessing**: Learned that **80% of analysis time** is spent on cleaning and preparing data.  
- **Advanced DAX Calculations**: Developed a deeper understanding of creating complex measures.  
- **Resilient Data Loading**: Implemented dynamic file handling for scalable data ingestion.  
- **Data Visualization**: Designed an intuitive dashboard that translates raw data into actionable insights.  

---

## 🚀 **Future Enhancements**  
- Incorporate machine learning models for **sales forecasting**.  
- Add KPIs to measure **customer acquisition and retention rates**.  
- Automate report distribution using Power BI Service.  

---

## 🌐 **Connect with Me**  
- **GitHub Repository**: [Sales Performance Analysis Dashboard](https://github.com/Saimu-71/RFM-Analysis-of-Sales-Data-and-Clustering/)  
- **LinkedIn**: [Tanshen Mahamud Saimu](https://www.linkedin.com/in/tanshen-mahamud-saimu-066a471a6/)  
