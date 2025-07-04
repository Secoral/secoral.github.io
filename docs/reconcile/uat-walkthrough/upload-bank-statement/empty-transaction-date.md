---
title: Empty Transaction Date
parent: Upload Bank Statement
nav_order: 1
last_modified_date: 2025-07-04
---

# Example: Empty Transaction Date

This example shows what happens when the **Transaction Date** column is left empty in one or more rows.

## Sample Data Used

| Value Date | Transaction Date | Description | Deposit | Withdrawal | Balance | Ref No      | Institution | Category |
| ---------- | ---------------- | ----------- | ------- | ---------- | ------- | ----------- | ----------- | -------- |
| 02/05/2025 | _(empty)_        | Example 1   | 100     | 0          | 500     | 2025-05-001 |             |          |
| 02/05/2025 | 02/05/2025       | Example 2   | 200     | 0          | 700     | 2025-05-002 |             |          |

## Upload Outcome

After uploading this file:

1. The system will display:
2. Navigate to **Job Status** to check processing results.
3. In the Job Status table, you will see an entry similar to:

   | Job ID | System | Status |
   | ------ | ------ | ------ |
   | ...    | Bank   | Failed |

4. Download the result file to view validation errors.

## Validation Result Example

The downloaded file will include additional columns highlighting the detected issues:

| Value Date | Transaction Date | Description | Deposit | Withdrawal | Balance | Ref No      | Institution | Category | Has_Error | Validation_Errors               |
| ---------- | ---------------- | ----------- | ------- | ---------- | ------- | ----------- | ----------- | -------- | --------- | ------------------------------- |
| 02/05/2025 | _(empty)_        | Example 1   | 100     | 0          | 500     | 2025-05-001 |             |          | Y         | Invalid Transaction Date Format |
| 02/05/2025 | 02/05/2025       | Example 2   | 200     | 0          | 700     | 2025-05-002 |             |          | N         |                                 |

## How to Fix

1. Open the file in Excel.
2. Correct the **Transaction Date** for any rows marked with errors.
3. Recalculate or verify **Balance** if necessary.
4. Save the corrected file.
5. Re-upload to complete processing.
