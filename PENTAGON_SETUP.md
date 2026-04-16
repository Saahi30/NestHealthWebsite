# Project Pentagon - Google Sheets Setup

## Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com) and create a new spreadsheet
2. Name it **"Project Pentagon - Early Access Signups"**
3. In Row 1, add these headers:
   - A1: `Timestamp`
   - B1: `First Name`
   - C1: `Last Name`
   - D1: `Email`
   - E1: `Phone`
   - F1: `Interest`

## Step 2: Create the Apps Script

1. In your Google Sheet, go to **Extensions → Apps Script**
2. Delete any existing code and paste this:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);

  sheet.appendRow([
    data.timestamp,
    data.firstName,
    data.lastName,
    data.email,
    data.phone,
    data.interest
  ]);

  return ContentService
    .createTextOutput(JSON.stringify({ status: "success" }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. Click **Save** (Ctrl+S)

## Step 3: Deploy as Web App

1. Click **Deploy → New deployment**
2. Click the gear icon next to "Select type" → choose **Web app**
3. Set:
   - **Description**: "Project Pentagon Form"
   - **Execute as**: Me
   - **Who has access**: Anyone
4. Click **Deploy**
5. Authorize the app when prompted
6. **Copy the Web app URL** (it looks like `https://script.google.com/macros/s/XXXX/exec`)

## Step 4: Update index.html

Find this line in `index.html`:

```javascript
var PENTAGON_SHEET_URL = "YOUR_GOOGLE_APPS_SCRIPT_URL";
```

Replace `YOUR_GOOGLE_APPS_SCRIPT_URL` with the URL you copied in Step 3.

## Done!

Every form submission will now add a row to your Google Sheet with the user's details.
