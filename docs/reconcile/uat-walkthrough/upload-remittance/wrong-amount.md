---
title: Wrong Amount Example
parent: Upload Remittance
nav_order: 1
last_modified_date: 2025-07-04
---

# Wrong Amount Example

This walkthrough demonstrates how the system detects and flags invalid or zero **Payable Amount** in a remittance file.

---

## 🎯 Scenario

The uploaded file includes a Medisave row (**M**) where the **Payable Amount** is missing or invalid.

---

## 📝 Example Input File

Below is the example remittance file, with a **wrong amount** in one record:

| H | 20250502 | 1000 | | | | | | | | | | |
| Rec Type | HRN | Patient Name | Sub Type | Sub Date | Sub Time | Deduction Date | Discharge Date | CPF Acc No. | Medishield Plan Type | Payable Amt | Medisave Int Amt Payable | Remarks |
| ----------- | ------------- | ------------ | -------- | -------- | -------- | -------------- | -------------- | ----------- | -------------------- | ---------------- | ------------------------ | ---------- |
| C | A12345678910I | John Tan | FS | 20250424 | 1029 | 20250430 | 20250414 | S1234567A | 1 | | | |
| M | A12345678910I | John Tan | FS | 20250424 | 1029 | 20250430 | 20250414 | S1234567A | | **WRONG AMOUNT** | | |
| C | A34567891011C | Jane Tan | FS | 20250429 | 1525 | 20250430 | 20250419 | S2345678B | 1 | | | |
| M | A34567891011C | Jane Tan | FS | 20250429 | 1525 | 20250430 | 20250419 | S2345678B | | 1000 | | |
| T | 4 | 2275.48 | | | | | | | | | | 2025-05-05 |

---

## ✅ Expected System Behavior

1. Upload the file via **Upload Remittance**.
2. A **File uploaded successfully** message will appear.
3. Navigate to **Job Status**.
4. You will see an entry:

   | Job ID | System     | Status |
   | ------ | ---------- | ------ |
   | ...    | Remittance | Failed |

5. Download the processed file to view the validation results.

---

## 📝 Example Output File

Below is what the processed file will look like (columns simplified for clarity):

| H | 20250502 | 1000 | | | | | | | | | | | | |
| Rec Type | HRN | Patient Name | Sub Type | Sub Date | Sub Time | Deduction Date | Discharge Date | CPF Acc No. | Medishield Plan Type | Payable Amt | Medisave Int Amt Payable | Remarks | | |
| C | A12345678910I | John Tan | FS | 20250424 | 1029 | 20250430 | 20250414 | S1234567A | 1 | | | | | |
| M | A12345678910I | John Tan | FS | 20250424 | 1029 | 20250430 | 20250414 | S1234567A | | WRONG AMOUNT | | | Y | Invalid or zero Payable Amt |
| C | A34567891011C | Jane Tan | FS | 20250429 | 1525 | 20250430 | 20250419 | S2345678B | 1 | | | | | |
| M | A34567891011C | Jane Tan | FS | 20250429 | 1525 | 20250430 | 20250419 | S2345678B | | 1000 | | | | |
| T | 4 | 2275.48 | | | | | | | | | | 2025-05-05 00:00:00 | | |

---

**💡 Note:**

- Only the affected row (`M`) is flagged.
- The error message clearly states:  
  `Invalid or zero Payable Amt`

---
