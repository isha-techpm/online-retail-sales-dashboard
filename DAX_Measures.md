# 📊 DAX Measures – Online Retail Dashboard

This document explains the exact DAX measures used to generate the visuals displayed in the Online Retail Sales Dashboard. The dashboard contains four visuals:

- Revenue by Month  
- Quantity & Revenue by Country  
- Revenue by CustomerID  
- Quantity by Country (Map)

All measures are calculated from a single table: **'Online Retail'**, containing:
`InvoiceDate`, `Quantity`, `UnitPrice`, `CustomerID`, `Country`, `InvoiceNo`, `StockCode`, `Description`.

---

## 🧮 1. Total Revenue

Used in:
- Revenue by Month
- Quantity & Revenue by Country
- Revenue by CustomerID

```DAX
Total Revenue =
SUMX (
    'Online Retail',
    'Online Retail'[Quantity] * 'Online Retail'[UnitPrice]
)
```

---

## 📦 2. Total Quantity

Used in:
- Quantity & Revenue by Country
- Quantity by Country (Map)

```DAX
Total Quantity =
SUM ( 'Online Retail'[Quantity] )
```

---

## 📅 3. Revenue by Month (Line Chart)

No extra measure required.  
In the visual:
- Axis → `InvoiceDate` (set to Month or Year-Month)
- Values → `[Total Revenue]`

Power BI automatically groups months using the `InvoiceDate` hierarchy.

---

## 🌍 4. Quantity & Revenue by Country (Clustered Column Chart)

Uses two existing measures:

- `[Total Quantity]`
- `[Total Revenue]`

Visual setup:
- Axis → `Country`
- Values → `[Total Quantity]`, `[Total Revenue]`

---

## 👤 5. Revenue by CustomerID (Bar Chart)

Uses:

- `[Total Revenue]`

Visual setup:
- Axis → `CustomerID`
- Values → `[Total Revenue]`

(Optional) To sort customers by revenue:

```DAX
Customer Rank =
RANKX (
    ALL ( 'Online Retail'[CustomerID] ),
    [Total Revenue],
    ,
    DESC
)
```

Sort the visual by `[Customer Rank]`.

---

## 🗺️ 6. Quantity by Country (Map Visual)

Uses:

- `[Total Quantity]`

Visual setup:
- Location → `Country`
- Bubble size → `[Total Quantity]`

---

## ✅ Summary of Measures Used

| Purpose                        | Measure         |
|-------------------------------|-----------------|
| Total Revenue                 | ✔ `Total Revenue` |
| Total Quantity                | ✔ `Total Quantity` |
| Revenue by Month              | ✔ uses `Total Revenue` |
| Quantity & Revenue by Country | ✔ both measures |
| Revenue by CustomerID         | ✔ `Total Revenue` |
| Map (Quantity by Country)     | ✔ `Total Quantity` |


