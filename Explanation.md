
---

# 🔍 **Explanation of Formulas Used**

Below is a simple explanation of what each formula does and why it is used.

---

## ### **1️⃣ ISA Percentage (Column D)**

### **Formula:**

```excel
=IF(AND(B2<>"",C2<>""),(B2/C2)*100,"")
```

### **Explanation:**

* This formula checks whether **ISA Marks (B2)** and **ISA Max Marks (C2)** are entered.
* If both are filled:

  * It calculates the percentage using:
    **(Marks Obtained ÷ Maximum Marks) × 100**
* If any value is missing, it returns **blank** instead of an error.

---

## ### **2️⃣ Predicted SEA Marks (Weighted ISA Marks) – Column E**

### **Formula:**

```excel
=IF(B2="","",ROUND((B2/C2)*F2,0))
```

### **Explanation:**

* This predicts SEA score based on ISA performance.
* It calculates the ISA percentage and multiplies it by **SEA_Max (F2)** to get a proportional score.
* `ROUND(...,0)` rounds it to the nearest whole number.

This is used when you want to estimate how well a student is likely to perform externally.

---

## ### **3️⃣ SEA Percentage (Column G)**

### **Formula:**

```excel
=IF(AND(E2<>"",F2<>""),(E2/F2)*100,"")
```

### **Explanation:**

* Calculates percentage in the same way as ISA:

  * **(SEA Marks ÷ SEA Max Marks) × 100**
* Only calculates when both values exist.

---

## ### **4️⃣ Final Percentage (Column H)**

### **Formula:**

```excel
=IF(AND(D2<>"",G2<>""),(D2+G2)/2,IF(D2<>"",D2,IF(G2<>"",G2,"")))
```

### **Explanation:**

This formula finds the *final performance* using both ISA and SEA percentages.

It does the following:

1. **If both ISA% and SEA% are available →**

   * Final = Average of ISA% and SEA%
2. **If only ISA% is available →**

   * Final = ISA%
3. **If only SEA% is available →**

   * Final = SEA%
4. **If neither is available →**

   * Leave blank.

This ensures **no error appears** even when marks are missing.

---

## ### **5️⃣ Grade (Column I)**

### **Formula:**

```excel
=IF(H2="","",INDEX(GradeMap!$C$2:$C$9,
MATCH(1, INDEX((H2>=GradeMap!$A$2:$A$9)*(H2<=GradeMap!$B$2:$B$9),0),0)))
```

### **Explanation:**

This formula determines which **grade** (O, A+, A...) corresponds to the student’s final percentage by checking the GradeMap table.

It works like this:

1. Checks if H2 (Final Percentage) is empty → If yes, leave blank.
2. Looks at the **GradeMap sheet** which has:

   * Min %
   * Max %
   * Grade
3. Uses `MATCH` to find the row where:

   * Final% ≥ Min%
   * Final% ≤ Max%
4. Uses `INDEX` to return the **Grade** from that row.

This allows full automation of the grade assignment.

---

## ### **6️⃣ Grade Points (SGPA) – Column J**

### **Formula:**

```excel
=IF(H2="","",INDEX(GradeMap!$D$2:$D$9,
MATCH(1, INDEX((H2>=GradeMap!$A$2:$A$9)*(H2<=GradeMap!$B$2:$B$9),0),0)))
```

### **Explanation:**

This works exactly like the Grade formula, but instead of returning:

* **Grade** (O, A+, A...)

It returns:

* **SGPA Points** (10, 9, 8...)

So if grade is **O**, SGPA = **10**.

---

# ✅ Summary Table 

| Column                  | Formula Purpose                                |
| ----------------------- | ---------------------------------------------- |
| D – ISA Percentage      | Converts marks to percentage                   |
| E – Predicted SEA Marks | Estimates external marks using ISA performance |
| G – SEA Percentage      | Converts SEA marks to percentage               |
| H – Final Percentage    | Calculates combined score                      |
| I – Grade               | Assigns grade using GradeMap                   |
| J – Grade Points        | Fetches SGPA based on grade                    |


