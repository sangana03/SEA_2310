#2310

# 📊 Student Performance Analysis – Automated Excel Sheet

This project provides an Excel-based automated system for calculating student performance using internal marks, external marks, weightages, grade boundaries, and SGPA mapping.
All calculations are performed using Excel formulas, ensuring **accuracy**, **automation**, and **easy scalability** for multiple students.

---

## ✅ **📁 Project Overview**

This Excel tool is designed to simplify the evaluation of students by automatically computing:

* Percentage scores
* Weighted marks (internal + external)
* Final combined score
* Final overall percentage
* Grade assignment (using a Grade Map sheet)
* SGPA mapping

The tool ensures that teachers or evaluators only enter raw marks — the sheet handles the rest on its own.

---

## 📌 **🔧 Key Features**

### **1. Automatic Percentage Calculation (Column D & E)**

* **D2:** Calculates the **percentage of internal marks**, only when both internal score (B2) and max internal marks (C2) are provided.

  ```excel
  =IF(AND(B2<>"",C2<>""),(B2/C2)*100,"")
  ```

* **E2:** Calculates the **weighted internal marks**, rounded to a whole number.

  ```excel
  =IF(B2="","",ROUND((B2/C2)*F2,0))
  ```

### **2. External Marks Percentage (Column G)**

Calculates the percentage score for external marks only when both score and out-of marks are present:

```excel
=IF(AND(E2<>"",F2<>""),(E2/F2)*100,"")
```

### **3. Final Combined Score (Column H)**

This formula averages internal and external marks **only if both values exist**.
If one is missing, it uses the available value.

```excel
=IF(AND(D2<>"",G2<>""),(D2+G2)/2,IF(D2<>"",D2,IF(G2<>"",G2,"")))
```

### **4. Grade Assignment (Column I)**

Uses the **GradeMap sheet** to automatically look up the correct grade based on the final percentage:

```excel
=IF(H2="","",INDEX(GradeMap!$C$2:$C$9, MATCH(1, INDEX((H2>=GradeMap!$A$2:$A$9)*(H2<=GradeMap!$B$2:$B$9),0),0)))
```

### **5. SGPA Mapping (Column J)**

Similar lookup method to fetch SGPA values from the grade map:

```excel
=IF(H2="","",INDEX(GradeMap!$D$2:$D$9, MATCH(1, INDEX((H2>=GradeMap!$A$2:$A$9)*(H2<=GradeMap!$B$2:$B$9),0),0)))
```

---

## 🗂 **📄 GradeMap Sheet**

This secondary sheet contains:

| Min % | Max % | Grade | SGPA |
| ----- | ----- | ----- | ---- |
| 90    | 100   | O     | 10   |
| 80    | 89    | A+    | 9    |
| …     | …     | …     | …    |

The main sheet uses these ranges to automatically determine:

* The letter grade
* The SGPA

---

## 🎯 **📘 What This Project Achieves**

✔ Eliminates manual calculations
✔ Minimizes human error
✔ Automatically assigns grade & SGPA
✔ Fully customizable for any department or university
✔ Easy to update grade boundaries
✔ Suitable for any batch size

---

## 🚀 **How to Use**

1. Enter student marks in the highlighted input columns (Internal, External).
2. All percentages, weights, final scores, grades, and SGPA are generated automatically.
3. Modify the **GradeMap** sheet to match your institution’s rules.

---

## 📥 **Files Included**

* `StudentPerformance.xlsx` – Main automated calculation sheet
* `GradeMap` – Grade & SGPA mapping table
* `Explanation.md` - explanation of all the formulas 
---




