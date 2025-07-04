---
title: Deposit Contains Character
parent: Upload Bank Statement
nav_order: 2
last_modified_date: 2025-07-04
---

# Deposit Contains Character

This walkthrough demonstrates how the system responds when the **Deposit** column contains an invalid character.

## Scenario

In this example, a bank statement Excel file is uploaded where **Row 2** contains the letter `A` instead of a numeric deposit value.

## Example Input

Below is the content of the uploaded bank statement:

| Value Date | Transaction Date | Timestamp | Description | Deposit | Withdrawal | Balance     | Ref No | Institution | Category |
| ---------- | ---------------- | --------- | ----------- | ------- | ---------- | ----------- | ------ | ----------- | -------- |
| 02/05/2025 | 01/05/2025       | EXAMPLE-1 | 100         | 0       | 500        | 2025-05-001 |        |             |
| 02/05/2025 | 02/05/2025       | EXAMPLE-2 | A           | 0       | 700        | 2025-05-002 |        |             |
| 02/05/2025 | 02/05/2025       | EXAMPLE-3 | 300         | 0       | 1000       | 2025-05-003 |        |             |

## Expected System Behavior

1. **File Upload:**  
   After uploading this file via the **Upload Bank Statement** page, you will receive a _File uploaded successfully_ confirmation.

2. **Navigate to Job Status:**  
   Go to the **Job Status** section to view the processing results.

3. In the **Job Status** table, you will see an entry similar to:

| Job ID | System | Status |
| ------ | ------ | ------ |
| ...    | Bank   | Failed |

4. **Download the annotated file:**  
   Download the output file to review validation errors.

## Example Output

The downloaded Excel file will include additional columns highlighting validation issues:

| Value Date | Transaction Date | Description | Deposit | Withdrawal | Balance | Ref No      | Institution | Category | Has_Error | Validation_Errors      |
| ---------- | ---------------- | ----------- | ------- | ---------- | ------- | ----------- | ----------- | -------- | --------- | ---------------------- |
| 02/05/2025 | 01/05/2025       | EXAMPLE-1   | 100     | 0          | 500     | 2025-05-001 |             |          |           |                        |
| 02/05/2025 | 02/05/2025       | EXAMPLE-2   | A       | 0          | 700     | 2025-05-002 |             |          | Y         | Invalid Deposit Format |
| 02/05/2025 | 02/05/2025       | EXAMPLE-3   | 300     | 0          | 1000    | 2025-05-003 |             |          |           |                        |
