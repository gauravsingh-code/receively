# Google Sheets Form Integration Setup

This guide shows you how to automatically save form submissions (Name, Email, Message) to Google Sheets.

---

## 🔔 Common Setup Note

**Seeing "Google hasn't verified this app" warning?**  
✅ **This is normal!** Click "Advanced" → "Go to [project name] (unsafe)" → "Allow"  
You're authorizing your own script to access your own spreadsheet. Completely safe.

---

## 📋 What You'll Get

- All form submissions automatically saved to a Google Sheet
- Timestamp for each submission
- View and export data anytime
- **100% Free** - no limits

---

## 🚀 Setup Instructions (10 minutes)

### Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Click **+ Blank** to create a new spreadsheet
3. Name it "Receivly Waitlist" (or whatever you prefer)
4. In the first row, add these column headers:
   ```
   A1: Timestamp
   B1: Name
   C1: Email
   D1: Message
   ```

### Step 2: Create the Apps Script

1. In your Google Sheet, click **Extensions** → **Apps Script**
2. Delete any existing code
3. **Copy and paste this ENTIRE code:**

```javascript
function doPost(e) {
  try {
    // Open the active spreadsheet
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    
    // Get form data
    var timestamp = new Date();
    var name = e.parameter.name || '';
    var email = e.parameter.email || '';
    var message = e.parameter.message || '';
    
    // Add a new row with the data
    sheet.appendRow([timestamp, name, email, message]);
    
    // Return success response
    return ContentService.createTextOutput(
      JSON.stringify({ result: 'success', row: sheet.getLastRow() })
    ).setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    // Return error response
    return ContentService.createTextOutput(
      JSON.stringify({ result: 'error', error: error.toString() })
    ).setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Click **Save** (disk icon) and name your project "Receivly Form Handler"

### Step 3: Deploy the Script

1. Click the **Deploy** button (top right) → **New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Configure the deployment:
   - **Description:** "Receivly Waitlist Form v1"
   - **Execute as:** Me (your email)
   - **Who has access:** **Anyone** ⚠️ (Important!)
5. Click **Deploy**

6. **⚠️ IMPORTANT: Authorize access (You'll see a warning - this is NORMAL!):**
   - Click "Authorize access"
   - Choose your Google account
   - **You'll see: "Google hasn't verified this app"** ← This is expected!
   - Click **"Advanced"** (bottom left)
   - Click **"Go to Receivly Form Handler (unsafe)"** or whatever you named it
   - Click **"Allow"**
   
   **Why this warning appears:** Google shows this for all personal scripts. Since YOU created this script and it only accesses YOUR spreadsheet, it's completely safe. You're just authorizing your own script.

7. **Copy the Web app URL** - it looks like:
   ```
   https://script.google.com/macros/s/AKfycbz.../exec
   ```

### Step 4: Connect to Your Landing Page

1. Open `invoiceflow-landing.html`
2. Find this line (around line 605):
   ```html
   <form action="YOUR_GOOGLE_SCRIPT_URL" method="POST"
   ```
3. Replace `YOUR_GOOGLE_SCRIPT_URL` with your actual Web app URL
4. Save the file

### Step 5: Test It! 🎉

1. Open your landing page in a browser
2. Fill out the form with test data
3. Click "Join Waitlist"
4. Check your Google Sheet - you should see a new row!

---

## ✅ Testing Checklist

- [ ] Google Sheet created with correct headers
- [ ] Apps Script code copied and saved
- [ ] Deployment created with "Anyone" access
- [ ] Web app URL copied
- [ ] Landing page updated with correct URL
- [ ] Test submission successful
- [ ] Data appears in Google Sheet

---

## 🔍 Troubleshooting

### ⚠️ "Google hasn't verified this app" Warning

**This is NORMAL and SAFE to proceed!**

When you see this warning during authorization:
1. Click **"Advanced"** (link at bottom left of warning)
2. Click **"Go to [Your Project Name] (unsafe)"**
3. Click **"Allow"** on the permissions screen

**Why you see this:**
- Google shows this warning for ALL personal Apps Script projects
- You are both the developer AND the only user
- The script only accesses YOUR Google Sheet
- No one else can access your data
- This is standard for personal automation scripts

**You're safe because:**
- ✅ You wrote the code (or copied trusted code)
- ✅ It only writes to your own spreadsheet
- ✅ No external services are involved
- ✅ You control the deployment settings

### "Form submission error" message

**Problem:** The script URL is incorrect or not deployed properly

**Solution:**
- Double-check the URL in your HTML matches the deployment URL
- Make sure you deployed as "Anyone" can access
- Try creating a new deployment

### Nothing appears in Google Sheet

**Problem:** The script might not be authorized properly

**Solution:**
- Go back to Apps Script → Deploy → Manage deployments
- Click Edit → Save → Deploy again
- Make sure you authorized the script during deployment

### "Authorization required" error

**Problem:** You need to authorize the script

**Solution:**
- In Apps Script, click the Run button (▶️) to test
- This will trigger the authorization flow
- After authorizing, deploy again

---

## 📊 Viewing Your Data

### In Google Sheets:
- All submissions appear in real-time
- Sort by timestamp to see newest first
- Use filters to find specific emails
- Export to Excel anytime (File → Download)

### Email Notifications (Optional):
Want to get emailed for each submission? Add this to your Apps Script:

```javascript
// Add this inside the doPost function, after sheet.appendRow():

MailApp.sendEmail({
  to: "your-email@example.com",
  subject: "New Receivly Waitlist Signup!",
  body: `New signup:\n\nName: ${name}\nEmail: ${email}\nMessage: ${message}`
});
```

---

## 🔒 Privacy & Security

- Your Google Sheet is private by default (only you can see it)
- The script has "Anyone" access BUT they can only submit data, not read it
- No one can view your existing submissions
- You can revoke access anytime from Apps Script deployments

---

## 🎨 Advanced: Customize the Sheet

You can add:
- Formulas to count total signups
- Conditional formatting to highlight new entries
- Additional columns (e.g., referral source)
- Charts to visualize signups over time

---

## Need Help?

Common issues:
1. **CORS errors:** Make sure deployment is set to "Anyone" access
2. **405 error:** Check that form method is POST, not GET
3. **Empty rows:** Verify field names match (name, email, message)

Still stuck? The error is usually in the deployment settings - try redeploying with "Anyone" access.

---

## Next Steps

Once everything works:
1. Share your landing page with potential clients
2. Monitor submissions in your Google Sheet
3. Follow up with interested users
4. Iterate based on feedback

Good luck! 🚀
