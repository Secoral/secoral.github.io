---
title: Multiple Remittance Aggregation
parent: Reconcile
nav_order: 1
last_modified_date: 2025-07-04
---

# Multiple Remittance Aggregation Example

This walkthrough demonstrates how the system aggregates multiple remittance records into a **single bank statement reconciliation entry**, combining remittance and patient tracker data.

---

## Input Files

Below are examples of the uploaded files used in this scenario:

---

### Bank Statement

| Value Date | Transaction Date | Timestamp | Description         | Deposit  | Withdrawal | Balance  | Ref No      | Institution | Category  |
| ---------- | ---------------- | --------- | ------------------- | -------- | ---------- | -------- | ----------- | ----------- | --------- |
| 16/05/2025 | 16/05/2025       | _(empty)_ | Inward CR - GIRO... | 1,239.09 | 0          | 1,239.09 | 2025-05-283 | _(empty)_   | _(empty)_ |

---

### Remittance File

**Note:** 3 batches of remittances were included in a single upload.

### Remittance File

**Note:** This example includes multiple remittance batches.

Below is the **full table:**

| H        | 20250515      | 70359        |          |          |          |                |                |             |                      |             |                          |           |
| -------- | ------------- | ------------ | -------- | -------- | -------- | -------------- | -------------- | ----------- | -------------------- | ----------- | ------------------------ | --------- |
| Rec Type | HRN           | Patient Name | Sub Type | Sub Date | Sub Time | Deduction Date | Discharge Date | CPF Acc No. | Medishield Plan Type | Payable Amt | Medisave Int Amt Payable | Remarks   |
| C        | A12345678910B | Jason Tan    | AM       | 20250509 | 1616     | 20250514       | 20250423       | S123F       |                      |             |                          |           |
| M        | A12345678910B | Jason Tan    | AM       | 20250509 | 1616     | 20250514       | 20250423       | S123F       |                      | 0.19        |                          |           |
| T        | 2             | 0.19         |          |          |          |                |                |             |                      |             |                          | 16-May-25 |

---

| H        | 20250515      | 70359        |          |          |          |                |                |             |                      |             |                          |           |
| -------- | ------------- | ------------ | -------- | -------- | -------- | -------------- | -------------- | ----------- | -------------------- | ----------- | ------------------------ | --------- |
| Rec Type | HRN           | Patient Name | Sub Type | Sub Date | Sub Time | Deduction Date | Discharge Date | CPF Acc No. | Medishield Plan Type | Payable Amt | Medisave Int Amt Payable | Remarks   |
| C        | U12345678910B | Jack Tan     | FS       | 20250305 | 1554     | 20250514       | 20241029       | S123A       | 1                    |             |                          |           |
| M        | U12345678910B | Jack Tan     | FS       | 20250305 | 1554     | 20250514       | 20241029       | S123A       |                      | 638.9       |                          |           |
| T        | 3             | 638.9        |          |          |          |                |                |             |                      |             |                          | 16-May-25 |

---

| H        | 20250515      | 70359        |          |          |          |                |                |             |                      |             |                          |           |
| -------- | ------------- | ------------ | -------- | -------- | -------- | -------------- | -------------- | ----------- | -------------------- | ----------- | ------------------------ | --------- |
| Rec Type | HRN           | Patient Name | Sub Type | Sub Date | Sub Time | Deduction Date | Discharge Date | CPF Acc No. | Medishield Plan Type | Payable Amt | Medisave Int Amt Payable | Remarks   |
| C        | U12345678910D | Jake Tan     | FS       | 20250514 | 0903     | 20250514       | 20250513       | S123E       |                      |             |                          |           |
| M        | U12345678910D | Jake Tan     | FS       | 20250514 | 0903     | 20250514       | 20250513       | S123E       |                      | 300         |                          |           |
| C        | U12345678910C | James Tan    | FS       | 20250514 | 0905     | 20250514       | 20250513       | S123C       |                      |             |                          |           |
| M        | U12345678910C | James Tan    | FS       | 20250514 | 0905     | 20250514       | 20250513       | S123C       |                      | 300         |                          |           |
| T        | 4             | 600          |          |          |          |                |                |             |                      |             |                          | 16-May-25 |

---

### Patient Tracker

| Date of Procedure | Visit No | Location  | Type      | HRN           | Patient Name | NRIC  | Surgeon  | Mediclaim Sub Date | Mediclaim Sub Staff | Total Amount | Deposit |
| ----------------- | -------- | --------- | --------- | ------------- | ------------ | ----- | -------- | ------------------ | ------------------- | ------------ | ------- |
| 13-05-25          | Visit-1  | _(blank)_ | _(blank)_ | U12345678910C | James Tan    | S123C | John Tan | 14-05-25           | Jacob Tan           | 419.65       | 419.65  |
| 13-05-25          | Visit-2  | _(blank)_ | _(blank)_ | U12345678910D | Jake Tan     | S123E | John Tan | 14-05-25           | Jacob Tan           | 534.1        | 534.1   |

---

## Reconciliation Output

After reconciliation, the following output file was produced:

| Bank Ref No | Bank Transaction Date | Category | Institution | Rec Type | Location | Remittance Ref | HRN           | Name      | Remittance Amount | Sub Date   | Sub Time | Visit No  |
| ----------- | --------------------- | -------- | ----------- | -------- | -------- | -------------- | ------------- | --------- | ----------------- | ---------- | -------- | --------- |
| 2025-05-283 | 16/05/2025            | Medisave | MSV         | M        | MSV      | 70359          | A12345678910B | Jason Tan | 0.19              | 2025-05-09 | 1616     | _(blank)_ |
| 2025-05-283 | 16/05/2025            | Medisave | MSV         | M        | MSV      | 70359          | U12345678910B | Jack Tan  | 638.90            | 2025-03-05 | 1554     | _(blank)_ |
| 2025-05-283 | 16/05/2025            | Medisave | MSV         | M        | MSV      | 70359          | U12345678910D | Jake Tan  | 300.00            | 2025-05-14 | 0903     | Visit-2   |
| 2025-05-283 | 16/05/2025            | Medisave | MSV         | M        | MSV      | 70359          | U12345678910C | James Tan | 300.00            | 2025-05-14 | 0905     | Visit-1   |

---

## What This Example Shows

**Aggregation:** All remittance records summing to match the bank statement total were consolidated under a single reference.

**Partial Enrichment:** Visit Numbers were only filled for records matching Patient Tracker data (James and Jake Tan).

**Manual Action Required:** For records missing Visit Numbers (Jason and Jack Tan), you must complete reconciliation manually.

---

## Expected User Actions

1. **Review the Reconciliation Output.**
2. **Identify records with empty Visit No.**
3. **Manually input Visit Numbers** for those records in the system UI or upload a supplemental mapping file.

---

## Manual Reconciliation Notes

{: .important }

During the [**Reconciliation**](#reconciliation-output) step, you can manually input missing values—such as **Visit No**, **HRN**, or **Bank Ref No**—directly into the reconciliation output file before uploading it for processing.

> **Important:**  
> If you manually enter a value that does **not** exist in the system database, the processed reconciliation will still fail validation.

### How to Address Missing References

- If the **Visit No** you enter is not recognized, you must upload or re-upload the **Patient Tracker** file that contains this Visit No.
- If the **HRN** is not found, you must ensure the corresponding **Remittance Statement** has been uploaded.
- If the **Bank Ref No** does not exist, you must confirm the correct **Bank Statement** has been uploaded.

This ensures the reconciliation engine can cross-reference your entries against valid records already stored in the system.

---

## Processed Reconciliation

After reviewing the reconciliation output, you will typically re-upload the file to the **Processed Reconciliation** endpoint to finalize the reconciliation.

---

### Steps

1. **Download** the reconciliation output file from the Job Status page.
2. **Upload** the file into the **Processed Reconciliation** page in the system UI.
3. **Review** the resulting Job Status and error report.

---

### Job Status Example

| Job ID | System              | Status  |
| ------ | ------------------- | ------- |
| ...    | processed-reconcile | Success |

> **Note:** Although the system status shows **success**, this only means the file was processed successfully.  
> Always review the error report to confirm which rows were actually reconciled.

---

### Error Message

> **Successfully reconciled 0 rows. 4 rows were not reconciled.**

---

### Downloaded Error File Example

Below is an example of the error file produced:

| Bank Ref No | Bank Transaction Date | Category | Institution | Rec Type | Location | Remittance Ref | HRN           | Name      | Remittance Amount | Sub Date   | Sub Time | Visit No  | Has_Error | Validation_Error                                    |
| ----------- | --------------------- | -------- | ----------- | -------- | -------- | -------------- | ------------- | --------- | ----------------- | ---------- | -------- | --------- | --------- | --------------------------------------------------- |
| 2025-05-283 | 2025-05-16            | Medisave | MSV         | M        |          | 70359          | A12345678910B | Jason Tan | 0.19              | 2025-05-09 | 1616     | _(empty)_ | Y         | Column 13 (Visit No) is empty; Visit_No is missing  |
| 2025-05-283 | 2025-05-16            | Medisave | MSV         | M        |          | 70359          | U12345678910B | Jack Tan  | 638.90            | 2025-03-05 | 1554     | _(empty)_ | Y         | Column 13 (Visit No) is empty; Visit_No is missing  |
| 2025-05-283 | 2025-05-16            | Medisave | MSV         | M        |          | 70359          | U12345678910D | Jake Tan  | 300.00            | 2025-05-14 | 0903     | Visit-2   | Y         | Group incomplete; another row has validation issues |
| 2025-05-283 | 2025-05-16            | Medisave | MSV         | M        |          | 70359          | U12345678910C | James Tan | 300.00            | 2025-05-14 | 0905     | Visit-1   | Y         | Group incomplete; another row has validation issues |

---

### About the "Group Incomplete" Error

**Why does this happen?**

- When a remittance reference includes **multiple rows**, _all rows in the group must have valid Visit Numbers_.
- If any record in the group is missing a Visit No, all related rows are marked as **Group incomplete**.
- This ensures the reconciliation process treats the set as a single consistent unit.

**How to Resolve:**

- Ensure all rows with the same **Remittance Ref** include a valid **Visit No**.
- Re-upload the corrected file to finalize reconciliation.
