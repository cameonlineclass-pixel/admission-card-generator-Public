Here is a comprehensive `README.md` file for your Admission Card Generator system. It documents how to use the tool and details the specific Excel structure required.

***

# Admission Card Generator

A lightweight, web-based tool designed to generate printable examination admission cards in bulk from Excel data. This system runs entirely in the browser (no backend required) and formats cards to fit 4 per A4 page for efficient printing.

## Features
* **Bulk Generation:** Upload an Excel file (`.xlsx`) or paste data directly to generate hundreds of cards instantly.
* **Smart Eligibility Check:** Automatically filters students based on their "Eligibility" status or by checking their Attendance and Payment completion.
* **Print-Ready Layout:** Automatically formats output to A4 landscape, fitting 4 admission cards per page.
* **Global Configuration:** Easily set common details (Program, Batch, Module, Exam Type) for the entire batch if they aren't included in the Excel file.
* **Manual Entry:** Add individual students manually if needed.

## How to Use

### 1. Open the System
Simply open the `index.html` file in any modern web browser (Google Chrome, Edge, Firefox, etc.). No installation is required.

### 2. Configure Document Information
At the top of the interface, fill in the official document details. These appear on every card:
* **Doc No:** (e.g., IJSE/EXAM/A-12)
* **Revision:** (e.g., 00 / -)
* **Issue Date:** (e.g., 01 / 25-06-2023)

### 3. Load Student Data
You have two options to load data:
* **Upload Excel:** Click "Choose File" and select your `.xlsx` file.
* **Paste Data:** Copy rows from Excel and paste them into the text area.

> **Important:** The system will only generate cards for "Eligible" students. If a student is marked "Not Eligible" or has incomplete payments/attendance, they will be skipped unless you manually override.

### 4. Set Global Fields
If your Excel file only contains student names and IDs, you can set the following details for the whole batch using the "Set Program / Batch / Module" section:
* **Program:** (e.g., GDSE)
* **Batch:** (e.g., 75)
* **Module:** (e.g., OOP)
* **Exam Types:** Check "Written", "Practical", or "Viva" as required.

### 5. Print
1.  Click the green **Print 4-per-Page** button.
2.  Your browser's print dialog will open.
3.  Ensure the **Paper Size** is set to **A4** and **Layout** is **Landscape**.
4.  Print to PDF or your physical printer.

---

## Required Excel File Structure

For the system to work correctly, your Excel file (`.xlsx`) must contain specific column headers. The system uses these headers to identify data.

**Required Columns:**
The file **MUST** contain at least these columns (order does not matter):

| Header Name | Description |
| :--- | :--- |
| **Student ID** | The unique ID of the student (e.g., `252751037`). |
| **Name** | The full name of the student. |
| **Attendance (80%)** | Must contain the word **"Completed"** for the student to be valid (unless explicitly marked Eligible). |
| **Payment Completion**| Must contain the word **"Completed"** for the student to be valid. |
| **Eligibility** | The final status. If this column says **"Eligible"**, the student is approved regardless of other columns. |

**Optional Columns:**
You can include these in the Excel file to specify details per student. If omitted, the "Global Fields" you type in the interface will be used.

| Header Name | Description |
| :--- | :--- |
| **Program** | The course name (e.g., CMJD, GDSE). |
| **Batch** | The batch number (e.g., 75). |
| **Module** | The subject or module name. |

### Example Data Format
Your Excel sheet should look like this:

| Student ID | Name | Attendance (80%) | Payment Completion | Eligibility |
| :--- | :--- | :--- | :--- | :--- |
| 252751037 | Sanduni Himasara | Not Completed | Completed | Not Eligible |
| 252751039 | Selvaraja Kalpanath | Completed | Completed | Eligible |
| 252751008 | Sadika Thihara | Completed | Completed | Eligible |

## Troubleshooting

* **"Choose an Excel file first"**: You pressed "Load Excel" without selecting a file.
* **No cards appear after loading**: 
    1. Check if your Excel headers match the "Required Columns" list above.
    2. Check if the students in your file are actually marked as "Eligible" or "Completed". The system hides ineligible students by default.
* **Layout looks wrong when printing**: Ensure your printer settings are set to **Landscape** and **Margins** are set to "Default" or "None".

## Technical Details
* **Frameworks:** TailwindCSS (via CDN), SheetJS (via CDN).
* **Compatibility:** Works on all modern browsers. Internet Connection is required to load the styles and libraries initially.

### 📂 Sample Excel File
You can view or download the official sample file here to see the correct format:

**[Google Sheets Sample Reference](https://docs.google.com/spreadsheets/d/1bDUAB2QCpqd-doKLYpcU2DXxNEIgKqt3EUmTp7HHdnM/edit?usp=sharing)**

To use this file:
1.  Open the link above.
2.  Go to **File > Download > Microsoft Excel (.xlsx)**.
3.  Upload the downloaded file into the Admission Card Generator.

#### Structure Verification
The reference file correctly uses the following headers which map to the system's logic:
* **Student ID**: Maps to `id`
* **Name**: Maps to `name`
* **Attendance (80%)**: Maps to `attendance` (Checks for "Completed")
* **Payment Completion**: Maps to `payment` (Checks for "Completed")
* **Eligibility**: Maps to `eligibility` (Overrides other checks if "Eligible")