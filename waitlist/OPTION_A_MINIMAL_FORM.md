# Option A: Minimal Friction Waitlist Form (RECOMMENDED FOR LAUNCH)

## Overview
- **Goal**: Maximize signups, build hype, low commitment
- **Expected Conversion**: 35-85%
- **Use Case**: Initial launch, social media campaigns, early awareness
- **Completion Time**: <60 seconds

---

## Google Form Setup Instructions

### Step 1: Create New Form
1. Go to https://forms.google.com
2. Click "+ Blank form"
3. Title: "Join the AMINA AI Waitlist"
4. Description:
```
Be among the first to transform your customer support with AI.
Join 500+ businesses waiting for AMINA AI to launch.

Get early access, special pricing, and exclusive updates.
```

### Step 2: Form Settings
Click the gear icon (Settings) and configure:
- ✅ **Collect email addresses**: ON
- ✅ **Limit to 1 response**: ON
- ✅ **Send response receipts**: ON
- ❌ **Require sign-in**: OFF (reduces friction)
- **Confirmation message**: See template below

### Step 3: Add Questions (5 fields)

---

#### Question 1: Work Email
- **Question**: Work Email
- **Type**: Short answer
- **Required**: YES (toggle required)
- **Validation**:
  - Click ⋮ (three dots) → Response validation
  - Select "Text" → "Contains"
  - Pattern: `@`
  - Custom error text: "Please enter a valid work email address"

---

#### Question 2: Full Name
- **Question**: Full Name
- **Type**: Short answer
- **Required**: YES
- **Validation**: None

---

#### Question 3: Company Name
- **Question**: Company Name
- **Type**: Short answer
- **Required**: YES
- **Validation**: None

---

#### Question 4: Company Size
- **Question**: Company Size
- **Type**: Dropdown
- **Required**: YES
- **Options** (copy/paste each line):
```
1-10 employees
11-50 employees
51-200 employees
201-1,000 employees
1,001+ employees
```

---

#### Question 5: Biggest Challenge
- **Question**: What's your biggest customer support challenge?
- **Type**: Paragraph
- **Required**: NO (optional to avoid dropoff)
- **Description**: "Help us understand how AMINA AI can best serve you (optional)"

---

## Step 4: Confirmation Message

Click "Settings" → "Presentation" → Edit confirmation message:

```
Thank you for joining the AMINA AI waitlist! 🎉

You're now part of an exclusive group getting early access to AI-powered customer support.

Here's what happens next:
✅ We'll email you when AMINA AI launches (Q1 2026)
✅ Early access to beta program for qualified businesses
✅ Special launch pricing (20% off first 3 months)

Want priority access? We'll send you a quick survey in 24 hours.

Questions? Email us at hello@amina-ai.com

— The AMINA AI Team
```

---

## Step 5: Theme Customization

1. Click the palette icon (top right)
2. **Header**: Choose "Header" option
3. **Upload header image** (recommended size: 1600 x 400px)
   - Use your AMINA AI logo/banner
4. **Theme color**: Choose your brand color
5. **Background color**: White or light gray
6. **Font style**: Modern sans-serif (e.g., "Basic" or "Modern")

---

## Step 6: Get Shareable Link

1. Click "Send" button (top right)
2. Click the link icon 🔗
3. ✅ Check "Shorten URL"
4. Copy the link (e.g., `https://forms.gle/abc123`)

**Use this link for**:
- Website embed
- Social media posts
- Email signature
- Marketing campaigns

---

## Step 7: Set Up Response Notifications

1. Click "Responses" tab
2. Click ⋮ (three dots) → "Get email notifications for new responses"
3. This sends you an email every time someone joins the waitlist

---

## Step 8: View & Export Responses

### View in Google Sheets
1. Click "Responses" tab
2. Click the Sheets icon 📊 "Create spreadsheet"
3. Choose "Create a new spreadsheet"
4. Name it: "AMINA AI Waitlist Responses"

### Response Columns
Your spreadsheet will have:
- Timestamp
- Work Email
- Full Name
- Company Name
- Company Size
- Biggest Challenge

---

## Embedding on Website

### Option 1: iFrame Embed
```html
<iframe
  src="https://docs.google.com/forms/d/e/YOUR_FORM_ID/viewform?embedded=true"
  width="640"
  height="800"
  frameborder="0"
  marginheight="0"
  marginwidth="0">
  Loading…
</iframe>
```

### Option 2: Direct Link Button
```html
<a href="https://forms.gle/YOUR_SHORT_URL"
   class="cta-button"
   target="_blank">
  Join the Waitlist
</a>
```

---

## Social Media Copy Templates

### LinkedIn Post
```
🚀 Exciting News: AMINA AI is coming soon!

Tired of overwhelming customer support inquiries?

We're building an AI-powered platform that handles customer questions 24/7,
so your team can focus on what matters.

✨ Early Access Benefits:
• Be first to try AMINA AI
• 20% launch discount
• Priority support

Join 500+ businesses on the waitlist 👉 [link]

#CustomerSupport #AISupport #SaaS #CustomerService
```

### Twitter/X Post
```
🤖 AMINA AI is launching soon!

Transform your customer support with AI that works 24/7.

Join the waitlist for:
✅ Early access
✅ 20% launch discount
✅ Exclusive updates

[link]

#AI #CustomerSupport #SaaS
```

### Instagram Story/Post
```
[Visual: AMINA AI logo + "Coming Soon"]

Join 500+ businesses transforming customer support with AI 🚀

Link in bio to join the waitlist 👆

#AminaAI #AISupport #CustomerService #SaaS
```

---

## Email Signature
```
---
John Doe
CEO, AMINA AI

🚀 Join our waitlist: [link]
AI-powered customer support is coming.
```

---

## Success Metrics to Track

### Week 1-2 (Launch Phase)
- Target: 100+ signups
- Conversion rate: 25%+ (form views → signups)
- Channel performance: Track which sources drive most signups

### Week 3-4 (Growth Phase)
- Target: 300+ total signups
- Weekly growth rate: 50+ new signups/week
- Geographic distribution: Focus on Nigerian businesses

### Quality Metrics
- Company size distribution: Aim for 60%+ in 11-1,000 employee range
- Challenge completion rate: 40%+ (indicates engagement)
- Email domain quality: 70%+ corporate emails (not Gmail/Yahoo)

---

## Next Steps After Launch

1. **Day 1**: Launch form, share on LinkedIn, Twitter, email list
2. **Day 2**: Send Welcome Email (see email templates)
3. **Day 3**: Send Detailed Survey (Option B) to all signups
4. **Week 2**: Begin lead scoring and segmentation
5. **Week 3**: Start outreach to high-priority leads
6. **Week 4**: Announce beta program to qualified leads

---

## Troubleshooting

### Low Conversion Rate (<15%)
- Simplify headline/description
- Reduce fields (already minimal at 5)
- Add social proof ("Join 500+ businesses")
- Test different CTAs

### High Bounce Rate (>70%)
- Check form loading speed
- Ensure mobile-friendly
- Simplify first question
- Add progress indicator

### Low Quality Leads
- Add email validation (block free domains)
- Make company size required
- Add "Job Title" field as Question 6

---

## Files Reference
- Email templates: `EMAIL_TEMPLATES.md`
- Landing page copy: `LANDING_PAGE_COPY.md`
- Lead scoring: `LEAD_SCORING.md`
- Follow-up survey (Option B): `OPTION_B_SURVEY.md`
