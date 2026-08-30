# Google Apps Script Deployment Instructions

## Problem
The grid save functionality is not working because the Google Apps Script needs to be redeployed after recent changes.

## Solution

### Step 1: Copy the Updated Code to Google Apps Script

1. Open your Google Apps Script project:
   - Go to your Google Sheet: `https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID`
   - Click **Extensions** → **Apps Script**

2. In the Apps Script editor:
   - Delete the old `saveGridSlots.gs` file (if it exists as a separate file)
   - Make sure `calendar-gas-v7.gs` is the main file with all code

3. The `saveGridSlots` function should be in `calendar-gas-v7.gs` (it's already there)

### Step 2: Deploy a New Version

1. In the Apps Script editor, click **Deploy** → **New deployment**
2. Choose **Type**: Select "Web app"
3. Set the following:
   - **Execute as**: Your email/account that owns the spreadsheet
   - **Who has access**: "Anyone" or "Anyone with the link" (depending on your preference)
4. Click **Deploy**
5. **Copy the new deployment URL** that's shown in the dialog

### Step 3: Update the Frontend URL

1. Go back to `index.html` in your VS Code workspace
2. Find line 881 where `SHEET_URL` is defined
3. Replace the current URL with the new deployment URL from Step 2:
   ```javascript
   const SHEET_URL='https://script.google.com/macros/s/YOUR_NEW_DEPLOYMENT_ID/exec';
   ```

### Step 4: Test

1. Save the files
2. Reload the calendar in your browser (Ctrl+F5 for hard refresh)
3. Try saving on the IG Grid page again

## If It Still Doesn't Work

Check the browser console (F12 → Console tab) for error messages. Common issues:

1. **404 error**: The new deployment URL wasn't copied correctly
2. **CORS error**: Make sure the deployment is set to "Anyone with the link" access
3. **Timeout error**: The sheet might have too many rows - try archiving old data
4. **"signal is aborted"**: The request timed out (30 seconds) - check if the sheet is too large

## Need Help?

If you see specific error messages in the console, share them for more specific troubleshooting.
