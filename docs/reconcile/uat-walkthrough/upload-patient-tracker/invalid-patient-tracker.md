---
title: Invalid HRN and Missing Visit No
parent: Upload Patient Tracker
nav_order: 3
last_modified_date: 2025-07-04
---

# Invalid HRN and Missing Visit Number

This example shows what happens when you upload a Patient Tracker file with:

- **HRN that does not have 13 characters**
- **Missing Visit No**

---

## Example Input File

| Date_of_Procedure | Visit_No  | Location | Type            | HRN   | Patient_Name | NRIC   | Surgeon   | Mediclaim_Sub_Date | Mediclaim_Sub_Staff | Total_Amount | Deposit |
| ----------------- | --------- | -------- | --------------- | ----- | ------------ | ------ | --------- | ------------------ | ------------------- | ------------ | ------- |
| 2-May-25          | _(blank)_ | Novena   | Mediclaim Scans | A123B | John Tan     | S1123A | Jason Tan | 5-May-25           | Jackson Tan         | 392.4        | 392.4   |
| 6-May-25          | 1234      | Novena   | Mediclaim Scans | A124D | Jane Tan     | S1234B | Jason Tan | 8-May-25           | Jackson Tan         | 392.4        | 392.4   |

---

## Expected Result

1. After uploading the file, you will see **File uploaded successfully.**
2. Go to **Job Status**.
3. In the Job Status table, you will see:

   | Job ID | System          | Status |
   | ------ | --------------- | ------ |
   | ...    | Patient Tracker | Failed |

4. Download the error file. You should see the following columns and validation errors:

| Date of Procedure | Visit No  | Location | Type            | HRN   | Patient Name | NRIC   | Surgeon   | Mediclaim Sub Date | Mediclaim Sub Staff | Total Amount | Deposit | Has_Error | Validation_Error                                      |
| ----------------- | --------- | -------- | --------------- | ----- | ------------ | ------ | --------- | ------------------ | ------------------- | ------------ | ------- | --------- | ----------------------------------------------------- |
| 2-May-25          | _(blank)_ | Novena   | Mediclaim Scans | A123B | John Tan     | S1123A | Jason Tan | 5-May-25           | Jackson Tan         | 392.4        | 392.4   | Y         | Missing Visit_No; Invalid HRN (must be 13 characters) |
| 6-May-25          | 1234      | Novena   | Mediclaim Scans | A124D | Jane Tan     | S1234B | Jason Tan | 8-May-25           | Jackson Tan         | 392.4        | 392.4   | Y         | Invalid HRN (must be 13 characters)                   |
