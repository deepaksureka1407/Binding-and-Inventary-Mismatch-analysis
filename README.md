# 📊 Binding vs Inventory Analysis - Power BI Dashboard

This Power BI dashboard helps track and analyze the flow of books from the **Binding Room** to the **Inventory Room**. It identifies mismatches, delays, and potential losses between production and stock entry stages.

---

## 📌 Purpose

The dashboard ensures:
- **Accurate tracking** of book movement post-printing
- **Mismatch detection** between binding and inventory
- **Delay analysis** to reduce processing lag
- **Operational transparency** across departments

---

## 📂 Data Sources

The model uses two tables:

1. **`binding_logs`**
   - `Book Barcode`
   - `Book Code`, `Book Title`
   - `Quantity` (bound)
   - `Log Time` (binding timestamp)
   - `User`

2. **`books_inventory_logs`**
   - `Barcode`, `Book`, `Book Code`
   - `Quantity` (entered into inventory)
   - `Date` (inventory timestamp)
   - `User`, `Type`, `Volume`, etc.

These are linked using a **bridge table** based on `Book Barcode`.

---

## 📈 Key Features

### ✅ KPI Cards
- Total Binding Quantity
- Total Inventory Quantity
- Mismatch Quantity (Difference)
- Delay (in Hours)

### 📄 Table Visual
- Detailed comparison per `Book Barcode`
- Shows binding quantity, inventory quantity, mismatch quantity, delay, and mismatch flag

### 📊 Charts
- **Mismatch Quantity by Book Barcode** (Bar Chart)
- **Inventory Trend by Date** (Line Chart)

### 🧰 Filters / Slicers
- Book Code
- Date Range
- Mismatch Flag (`Mismatch`, `No Mismatch`)

---

## ⚙️ DAX Measures Used

```dax
Mismatch Quantity = [Total Binding Quantity] - [Total Inventory Quantity]

Mismatch Flag = 
IF([Mismatch Quantity] <> 0, "Mismatch", "No Mismatch")

Delay (Hours) = 
DATEDIFF([First Binding Time], [First Inventory Time], HOUR)
