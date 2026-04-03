# Email Capture Setup for Receivly Landing Page

Your landing page is now ready to collect emails! You just need to connect it to an email service.

## Quick Setup (5 minutes) - Web3Forms (Recommended)

**Why Web3Forms?**
- ✅ Completely FREE
- ✅ No signup required initially
- ✅ Emails sent directly to your inbox
- ✅ Simple setup

**Steps:**
1. Go to [https://web3forms.com](https://web3forms.com)
2. Enter your email address
3. You'll receive an **Access Key** instantly
4. Open `invoiceflow-landing.html`
5. Find this line (around line 605):
   ```html
   <input type="hidden" name="access_key" value="YOUR_ACCESS_KEY_HERE">
   ```
6. Replace `YOUR_ACCESS_KEY_HERE` with your actual Access Key
7. Done! ✓

**Testing:**
- Open your landing page in a browser
- Enter an email and click "Notify me"
- You should receive the submission in your inbox

---

## Alternative Options

### Option 2: Google Forms (Simple but less branded)
1. Create a Google Form with just an email field
2. Get the form's submission URL
3. Replace the form action in the HTML

### Option 3: Formspree (Free tier: 50 submissions/month)
1. Sign up at [https://formspree.io](https://formspree.io)
2. Create a new form
3. Get your form endpoint (e.g., `https://formspree.io/f/YOUR_FORM_ID`)
4. Replace the form action in the HTML

### Option 4: Google Sheets (Track in spreadsheet)
1. Use a service like [SheetDB](https://sheetdb.io) or [AppScript](https://developers.google.com/apps-script)
2. Connect your form to auto-populate a Google Sheet
3. View all submissions in real-time

---

## What's Been Improved

### ✅ Removed:
- "Three headline options to A/B test" section (internal marketing content)
- Mock email submission (non-functional)

### ✅ Added:
- Real email form with proper submission handling
- Success/error states for user feedback
- Loading state during submission
- Professional error handling

### ✅ Clean Validation-Ready Page:
Your landing page now has only essential sections:
1. Hero with clear value proposition
2. Three core benefits
3. Email capture CTA
4. Simple footer

---

## Next Steps After Setup

1. **Test the form** - Submit your own email to verify it works
2. **Share with clients** - Send them the link for feedback
3. **Track responses** - Check your inbox for new submissions
4. **Iterate** - Based on feedback, adjust messaging

---

## Need Help?

If you run into issues:
- Check browser console for errors (F12 > Console tab)
- Verify your Access Key is correct
- Make sure you're testing on a live server (not just opening the HTML file)
- Some email services require HTTPS for form submissions

Good luck with your validation! 🚀
