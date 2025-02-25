# **Flipkart Sales Analysis with Power BI**


## **Project Objective**
The objective of this project is to analyze Flipkart sales data and gain insights into various aspects such as sales performance, seller activity, and product popularity. The data visualization and analysis are performed using Power BI, leveraging measures and DAX formulas to create interactive and informative dashboards.


## **Dataset**
**The analysis is based on two datasets:** 

**Flipkart Sale Report.xlsx:** Contains fields like Order ID, Date, Status, Fulfilment, Sales Channel, Ship Service Level, Style, SKU, Category, Size, ASIN, Courier Status, Qty, Currency, Ship City, Ship State, Ship Postal Code, Ship Country, Fulfilled By.

**Flipkart-fashion.csv:** Includes fields like Amazon Prime (Y/N), ASIN, Best Seller Tag (Y/N), Brand, Colour, Delivery Type, Discount Percentage, Large, Left in Stock, No. of Reviews, Description, Product Details, Product Name, Product URL, Rating, Sales Price, Category, Seller Name, Seller ID.

## **Analysis and Findings**
**Key Measures and DAX Formulas**

For Sale Icon On:
```
SalesOn = 
  VAR selected = SELECTEDVALUE(Sale_Option[Type])
  VAR _url = "https://drive.google.com/uc?export=view&id=1mcmb1peVHoaU5XL2bYXinZtW9sv2bNG4"
  RETURN IF(selected="1", _url)
```

For Units Icon On:
```
SalesOn = 
  VAR selected = SELECTEDVALUE(Sale_Option[Type])
  VAR _url = "https://drive.google.com/uc?export=view&id=1mcmb1peVHoaU5XL2bYXinZtW9sv2bNG4"
  RETURN IF(selected="2", _url)
```

Seller Count:
```
Seller Count = 
  CALCULATE(
    [Sale_Units], 
    ALL('amazon-fashion'[Category])
  )
= VAR val = CALCULATE(
    COUNT('amazon-fashion'[seller_id]), 
    CONTAINSSTRING(Amazon[Status], "Delivered")
  )
  RETURN val
```

Filter Sale:
```
Filter Sale = 
  VAR selecting = SELECTEDVALUE(Sale_Option[Type])
  VAR _units = SUM(Amazon[Qty])
  VAR _sale = SUM(Amazon[Total_Ammount])
  RETURN IF(selecting="1", _sale, _units)
```

Return Units:
```
Return_Units = 
  VAR val = CALCULATE(
    [Sale_Units], 
    CONTAINSSTRING(Amazon[Status], "Return")
  )
  RETURN IF(val=BLANK(), 0, val)
```

Reviews:
```
Reviews = 
  VAR val = COUNT('amazon-fashion'[no_of_reviews])
  RETURN IF(ISBLANK(val), 0)
```

Sale Amount:
```
Sale_Ammount = 
  VAR val = SUM(Amazon[Total_Ammount])
  RETURN IF(ISBLANK(val), 0)
```

Sale Units:
```
Sale_Units = 
  VAR selecting = SELECTEDVALUE(Sale_Option[Type])
  VAR _units = SUM(Amazon[Qty])
  VAR _sale = SUM(Amazon[Total_Ammount])
  RETURN IF(selecting="1", _sale, _units)
```

Sale Option:
```
Sale_Option = 
  DATATABLE(
    "Name", STRING, 
    "Type", STRING, 
    {{"1", "Sales"}, {"2", "Units"}}
  )
```

All Sale:
```
All_Sale = CALCULATE([Sale_Units], ALL('amazon-fashion'[Category]))
```

Order Counts:
```
Order_Counts = 
  VAR val = CALCULATE(
    COUNT('amazon-fashion'[seller_id]), 
    CONTAINSSTRING(Amazon[Status], "Delivered")
  )
  RETURN IF(val=BLANK(), "0", val)
```

## Visuals and Insights
The Power BI report includes the following visuals:

**Sales Performance:** Displays total sales and units sold over time.

**Seller Analysis:** Shows the number of sellers, their performance, and top-performing sellers.

**Product Popularity:** Highlights best-selling products and those with the highest reviews.

## Screenshots
**Please find below the screenshots of the Power BI dashboard showcasing various aspects of the analysis:**
<img width="851" alt="img 1" src="https://github.com/user-attachments/assets/2b14c733-1ea5-4c56-8692-c9d1b8e28e1c" />
<img width="854" alt="img 2 1" src="https://github.com/user-attachments/assets/48636c45-0817-4697-af3b-9f4d04c4ee3e" />
<img width="853" alt="img 2 2" src="https://github.com/user-attachments/assets/076a8a3d-ebc8-4377-9bfc-ef589e049f03" />
<img width="854" alt="img 3" src="https://github.com/user-attachments/assets/56605a4c-e47d-472b-b7d4-23b1551cb41e" />


## Color Scheme
**Blue Color:** #118dff

**Background Color:** #F8F8F8

**White Color:** #FFFFFF

## Conclusion
The analysis provides valuable insights into Flipkart's sales performance, seller activity, and product popularity. By leveraging measures and DAX formulas, we created an interactive and informative Power BI dashboard that can help stakeholders make data-driven decisions.

## Disclaimer
Please note that this analysis uses Amazon sales data but is designed in the theme of Flipkart. You can rename the data fields as per your convenience. The data used in this analysis is obtained from online sources.
