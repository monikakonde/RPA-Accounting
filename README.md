This project is an end-to-end UiPath automation that reads invoices from Excel, validates invoice totals using product line-item details, classifies invoices as Valid or Invalid, generates a new Excel file containing only valid invoices, and finally sends email notifications to the corresponding buyers.

---

📌 Project Overview

This automation performs the following steps:

1. Reads master Invoice data
From Invoices.xlsx, which contains:

Invoice ID

Name

Total Amount

Status

Email



2. Reads Product details
From InvoiceDetails.xlsx, which contains:

InvoiceID

ProductID

Price

Total Amount



3. Matches line-item details to each Invoice
For each InvoiceID, the bot:

Sums all individual item prices

Compares the sum with the expected Total Amount



4. Validates the Invoice

If sum of item prices == total amount, invoice is Valid

Else, invoice is Invalid



5. Updates status in the master Excel file

Status becomes: "Valid" or "Invalid"



6. Stores all Valid invoices into a new Excel file
Example: ValidInvoices.xlsx


7. Sends email notifications
Using Outlook:

Sends email only to entries marked Valid

Reads Email column from the Excel sheet


---

📁 Project Files Included

RPA - Accounting/
│
├── Main.xaml
├── RPA - Accounting.xaml
├── project.json
│
├── Invoices.xlsx                 # Master invoice sheet
├── InvoiceDetails.xlsx           # Product line-item sheet
│
├── ValidInvoices.xlsx            # Auto-generated (output)
│
├── .screenshots/                 # UiPath screenshots (ignored in Git)
├── .settings/                    # Project settings
└── .gitignore


---

⚙ How the Automation Works (Flow Summary)

1️⃣ Read Both Excel Sheets

Bot loads all invoice data and product detail rows into DataTables.


2️⃣ Process Each Invoice

For each invoice:

Reset total price counter

Extract the current InvoiceID

Loop through all product detail rows

If InvoiceID matches → add price to the sum

Store expected amount from the detail row


3️⃣ Validate

IF totalProductPrice == expectedTotalAmount
    mark as Valid
    add to dt_valid
ELSE
    mark as Invalid

4️⃣ Write Results

Update the master Invoices.xlsx with new statuses

Create a new file with only Valid invoices


5️⃣ Send Emails

Loop through valid invoices

Send Outlook email to the Email column in the Excel

Email body contains approval message



---

📦 Dependencies

This project uses:

UiPath.Excel.Activities

UiPath.Mail.Activities

UiPath.System.Activities


No external packages required.


---

📧 Email Requirements

To send email using Send Outlook Mail Message:

Outlook Desktop App must be installed

User must be logged in

Email account must allow automated sending or customize:

Email text

Valid/Invalid criteria

Add database integration

Add Orchestrator Queues

Add Logging and Exception Handling

Add Retry mechanism

Use REFramework for better scalability
