# 🧮 Card & Sticker Printing Calculators

This project includes two simple, fully offline HTML tools:

* **Card Printing Calculator**
* **Sticker Price Calculator**

Both calculators take user inputs (dimensions and quantity), check for static price matches, and if none exist, perform a **dynamic calculation** based on area and per-meter pricing.

---

## 📘 Card Printing Calculator — Logic Flow

### 🧾 Input Fields

The user provides:

* **Card Length (cm)**
* **Card Width (cm)**
* **Quantity**

---

### 🧩 Step-by-Step Calculation Flow

#### 1️⃣ **Static Data Check**

The calculator first checks the predefined `staticData` array:

* If the **entered width**, **height**, and **quantity** exactly match a record,
  → it returns that record’s **Item Code**, **Price**, and marks result as **Static Data**.
* No further calculation occurs.

---

#### 2️⃣ **Lookup Table (Cards per Meter)**

If no static match is found, the app looks up how many cards fit per meter along each direction using this table:

| Size | Cards per Meter (Length) | Cards per Meter (Width) |
| ---- | ------------------------ | ----------------------- |
| 1    | 30                       | 44                      |
| 2    | 20                       | 28                      |
| 3    | 16                       | 20                      |
| 4    | 14                       | 20                      |
| 5    | 12                       | 16                      |
| ...  | ...                      | ...                     |
| 20   | 2                        | 4                       |

---

#### 3️⃣ **Calculate Cards per Square Meter**

```
totalCardsPerMeter = cardsPerMeterLength × cardsPerMeterWidth
```

---

#### 4️⃣ **Calculate Meters Needed**

```
metersNeeded = totalQuantity ÷ totalCardsPerMeter
```

---

#### 5️⃣ **Price per Meter**

The price depends on total meters required:

```
If metersNeeded ≤ 10 → pricePerMeter = 40
If metersNeeded > 10 → pricePerMeter = 30
```

---

#### 6️⃣ **Final Price**

```
finalPrice = pricePerMeter × metersNeeded
```

---

#### 7️⃣ **Minimum Meter Warning**

If `metersNeeded < 1`, the app shows a red warning box:

> ⚠️ Minimum printable length is 1 meter — adjusted to 1 meter for pricing.

---

### 🧮 Example

**Input:**

```
Length = 5
Width = 9
Quantity = 100
```

**Steps:**

1. No static record found.
2. Lookup: 5 → 12 per meter length, 9 → 8 per meter width
   → totalCardsPerMeter = 12 × 8 = 96
3. metersNeeded = 100 ÷ 96 = 1.04
4. pricePerMeter = 40
5. finalPrice = 40 × 1.04 = **41.6**

**Output:**

```
Number of meters: 1.0
Price per meter: 40
Final price: 41.6
Code: 1234
Result Type: Calculated by Meter
```

---

## 🎨 Sticker Price Calculator — Logic Flow

1️⃣ **Static Table Lookup**

* Uses the largest sticker dimension and quantity to match against predefined static data.
* If matched → returns static **Price** and **Code**.

2️⃣ **Meter-Based Calculation (if no static match)**

* Looks up “stickers per meter” for both width and height.
* Computes:

  ```
  totalStickersPerMeter = widthValue × heightValue
  metersNeeded = quantity ÷ totalStickersPerMeter
  ```
* Chooses **price per meter**:

  | Meters Range | Price | Code  |
  | ------------ | ----- | ----- |
  | 1–5          | 120   | 54314 |
  | 5–10         | 90    | 54315 |
  | >10          | 70    | 54316 |
* Computes final total:

  ```
  finalPrice = metersNeeded × pricePerMeter
  ```
* Displays all values and code.

3️⃣ **Red Warning (<1 meter)**

* If meters < 1 → shows red box:
  “⚠️ Minimum printable length is 1 meter — adjusted to 1 meter for pricing.”

---

## 🧱 Project Structure

```
📦 printing-calculators/
 ┣ 📄 card_printing_calculator.html
 ┣ 📄 sticker_price_calculator.html
 ┗ 📘 README.md   ← (this file)
```

---

## 🧰 Technical Notes

* No external dependencies — runs 100% offline in any browser.
* Written in plain **HTML**, **CSS**, and **JavaScript**.
* Logic and prices are easily editable within the `<script>` section.

---

## ✅ License

You are free to use, modify, or share this tool within your organization or for personal/commercial use.
