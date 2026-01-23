# Option B: Detailed Qualification Survey

## Overview
- **Goal**: Quality leads with reasonable conversion
- **Expected Conversion**: 25-45%
- **Use Case**: Follow-up to Option A, beta program signups, early access
- **Timing**: Send 24-48 hours after initial waitlist signup
- **Completion Time**: ~2 minutes

---

## When to Use This Form

### Primary Use Cases:
1. **Follow-up Survey**: Email to all Option A waitlist signups (Day 2-3)
2. **Beta Application**: Direct link for beta program applications
3. **Sales Qualification**: Pre-qualify leads before demo calls

### Incentive to Complete:
"Complete this 2-minute survey to get priority access + 20% launch discount"

---

## Google Form Setup Instructions

### Step 1: Create New Form
1. Go to https://forms.google.com
2. Click "+ Blank form"
3. Title: "AMINA AI - Priority Access Survey"
4. Description:
```
Help us understand your business better to provide the best experience.

Complete this survey to:
✅ Get priority access to AMINA AI
✅ Unlock 20% launch discount
✅ Receive personalized onboarding

Takes only 2 minutes.
```

### Step 2: Form Settings
- ✅ **Collect email addresses**: ON
- ✅ **Limit to 1 response**: ON
- ✅ **Send response receipts**: ON
- ❌ **Require sign-in**: OFF
- **Progress bar**: ON (Settings → Presentation → "Show progress bar")

---

## Questions (8 fields)

### Section 1: Company Information

#### Question 1: Work Email
- **Question**: Work Email
- **Type**: Short answer
- **Required**: YES
- **Validation**: Text → Contains → `@`
- **Note**: This links responses to original waitlist signup

---

#### Question 2: Full Name
- **Question**: Full Name
- **Type**: Short answer
- **Required**: YES

---

#### Question 3: Company Name
- **Question**: Company Name
- **Type**: Short answer
- **Required**: YES

---

#### Question 4: Industry
- **Question**: What industry is your business in?
- **Type**: Dropdown
- **Required**: YES
- **Options**:
```
E-commerce/Retail
SaaS/Technology
Financial Services/Fintech
Healthcare
Telecommunications
Travel/Hospitality
Education
Professional Services
Government/Public Sector
Manufacturing
Real Estate
Media/Entertainment
Other (please specify)
```
- **Tip**: Click "Add 'Other'" at bottom of options list

---

#### Question 5: Company Size
- **Question**: How many employees does your company have?
- **Type**: Dropdown
- **Required**: YES
- **Options**:
```
1-10 employees
11-50 employees
51-200 employees
201-1,000 employees
1,001+ employees
```

---

### Section 2: Support Context
*Click "Add section" to create a new section titled "Customer Support Context"*

#### Question 6: Monthly Support Volume
- **Question**: How many customer inquiries does your business handle per month?
- **Type**: Dropdown
- **Required**: YES
- **Description**: "Include all channels: email, chat, phone, social media, etc."
- **Options**:
```
Less than 100 inquiries/month
100-500 inquiries/month
501-2,000 inquiries/month
2,001-5,000 inquiries/month
5,000-10,000 inquiries/month
10,000+ inquiries/month
```
- **🎯 CRITICAL**: This is the #1 qualification metric

---

#### Question 7: Primary Support Challenge
- **Question**: What is your PRIMARY customer support challenge?
- **Type**: Dropdown
- **Required**: YES
- **Options**:
```
High volume overwhelming our team
Slow response times (missing SLAs)
Too many repetitive questions
Need 24/7 coverage without hiring night shifts
Scaling support without hiring more agents
High agent turnover/burnout
Poor customer satisfaction scores (CSAT/NPS)
Language barriers (multilingual support needed)
Integration with existing tools (CRM, helpdesk)
Other (please specify)
```

---

#### Question 8: Timeline
- **Question**: When do you need a customer support solution?
- **Type**: Dropdown
- **Required**: NO (optional)
- **Description**: "This helps us prioritize onboarding"
- **Options**:
```
Immediately (within 2 weeks)
Within 1 month
1-3 months
3-6 months
6-12 months
Just exploring options
```

---

## Confirmation Message

```
Thank you! Your priority access survey is complete. 🎉

Based on your responses, here's what happens next:

✅ Priority Access Confirmed
Your 20% launch discount is reserved and will be sent via email.

✅ Beta Program Consideration
We're reviewing your submission for our exclusive beta program (Feb 2026).
If selected, you'll get:
• Free access for 3 months
• Dedicated onboarding support
• Direct line to our product team

✅ What's Next?
• High-priority leads: We'll contact you within 48 hours for a personalized demo
• All respondents: You'll receive weekly updates and early access invitations

Questions? Email us at hello@amina-ai.com

— The AMINA AI Team
```

---

## Lead Scoring Framework

### Automatic Scoring (Use Google Sheets formulas)

#### High Priority (Score: 80-100) 🔥
**Criteria**:
- Industry: Telecom, Finance, E-commerce, SaaS
- Company Size: 51-1,000 employees
- Volume: 500+ inquiries/month
- Timeline: Immediately or within 1 month
- Challenge: High volume, slow response, scaling

**Action**: Personal email + discovery call within 48 hours

---

#### Medium Priority (Score: 50-79) ⭐
**Criteria**:
- Industry: Healthcare, Education, Travel, Professional Services
- Company Size: 11-50 or 1,000+ employees
- Volume: 100-500/month
- Timeline: 1-3 months
- Challenge: Repetitive questions, 24/7 coverage, agent turnover

**Action**: Nurture campaign with case studies, invite to webinar

---

#### Low Priority (Score: 0-49) 📊
**Criteria**:
- Company Size: 1-10 employees
- Volume: <100/month
- Timeline: Just exploring or 6+ months
- Challenge: Integration, language barriers

**Action**: Automated email sequence, self-service resources

---

## Google Sheets Lead Scoring Formula

### Step 1: Link to Sheets
1. Responses tab → Sheets icon → "Create spreadsheet"
2. Name: "AMINA AI Priority Survey - Lead Scores"

### Step 2: Add Scoring Column
In column J (or after last question column), add header: **Lead Score**

### Step 3: Scoring Formula
Paste this formula in J2 (adjust column letters to match your sheet):

```excel
=
(IF(E2="Telecommunications",25,
 IF(E2="Financial Services/Fintech",25,
 IF(E2="E-commerce/Retail",20,
 IF(E2="SaaS/Technology",20,10)))))
+
(IF(F2="51-200 employees",20,
 IF(F2="201-1,000 employees",20,
 IF(F2="11-50 employees",15,
 IF(F2="1,001+ employees",10,5)))))
+
(IF(G2="5,000-10,000 inquiries/month",30,
 IF(G2="10,000+ inquiries/month",30,
 IF(G2="2,001-5,000 inquiries/month",25,
 IF(G2="501-2,000 inquiries/month",20,
 IF(G2="100-500 inquiries/month",10,5))))))
+
(IF(I2="Immediately (within 2 weeks)",15,
 IF(I2="Within 1 month",15,
 IF(I2="1-3 months",10,
 IF(I2="3-6 months",5,2)))))
+
(IF(H2="High volume overwhelming our team",10,
 IF(H2="Slow response times (missing SLAs)",10,
 IF(H2="Scaling support without hiring more agents",10,5))))
```

### Step 4: Add Priority Label
In column K, add header: **Priority**

Formula in K2:
```excel
=IF(J2>=80,"🔥 HIGH",IF(J2>=50,"⭐ MEDIUM","📊 LOW"))
```

### Step 5: Conditional Formatting
1. Select column K (Priority column)
2. Format → Conditional formatting
3. Format rules:
   - Text contains "HIGH" → Red background
   - Text contains "MEDIUM" → Yellow background
   - Text contains "LOW" → Green background

---

## Email Invitation Template (Day 2-3 after Option A signup)

### Subject Line Options:
1. "[Name], unlock your AMINA AI priority access (2 min survey)"
2. "Quick survey = 20% discount + priority access 🎁"
3. "[Company] - Complete your AMINA AI application"

### Email Body:

```
Hi [Name],

Thanks for joining the AMINA AI waitlist!

We're building AI customer support specifically for businesses like [Company Name].

To give you the best experience, we'd love to learn more about your needs.

👉 Complete this 2-minute survey to unlock:
✅ Priority access when we launch
✅ 20% launch discount (3 months)
✅ Beta program consideration (free for 3 months)

[Complete Priority Survey] ← CTA Button

This helps us:
• Prioritize features for your industry
• Personalize your onboarding
• Match you with the right pricing plan

Takes only 2 minutes.

Best regards,
[Your Name]
Founder, AMINA AI

P.S. High-volume businesses (500+ inquiries/month) will be contacted within 48 hours for a personalized demo.
```

---

## Response Rate Optimization

### Target Response Rate: 40-60%

### If response rate is LOW (<30%):
1. **Send Reminder Email** (Day 5):
   - Subject: "Last chance: 20% discount expires in 24 hours"
   - Urgency: "Only 50 beta spots available"
2. **Add Incentive**: Free 1-month extension on launch discount
3. **Shorten Survey**: Remove optional Question 8 (Timeline)
4. **Personalize**: Mention their specific company/industry in email

### If response rate is HIGH (>60%):
1. **Keep momentum**: Send thank you email immediately
2. **Add social proof**: "Join 300+ businesses who completed the survey"
3. **Share results**: "75% of respondents struggle with high volume"

---

## Integration with Option A

### Linking Responses
To match Option B survey with original Option A signup:

1. **In Google Sheets**: Use VLOOKUP to combine data
   - Sheet 1: Option A responses (waitlist)
   - Sheet 2: Option B responses (survey)
   - Match on: Email address

2. **Formula in Option A sheet** (to pull survey data):
```excel
=IFERROR(VLOOKUP(B2,'Option B'!B:G,3,FALSE),"Not completed")
```
This pulls Industry from Option B based on email match.

3. **Track Completion Rate**:
   - Total Option A signups: COUNT(Sheet1!A:A)
   - Completed Option B: COUNT(Sheet2!A:A)
   - Completion Rate: =Sheet2Count/Sheet1Count

---

## Follow-Up Actions by Priority

### 🔥 HIGH Priority (Score 80+)
**Within 48 hours**:
1. Send personalized email (see template below)
2. Offer discovery call with calendar link
3. Prepare custom demo showcasing their industry use case
4. Add to CRM as "Hot Lead"

**Email Template**:
```
Subject: [Name], let's solve [Company]'s [Challenge]

Hi [Name],

I reviewed your priority survey for [Company Name].

Handling [Volume] inquiries/month is challenging, especially with [Challenge].

I'd love to show you how AMINA AI can:
• Reduce response time by 80%
• Handle repetitive questions automatically
• Give your team breathing room to focus on complex issues

Are you available for a 20-minute call this week?

[Book a Time] ← Calendar link

Looking forward to it!

[Your Name]
Founder, AMINA AI
```

---

### ⭐ MEDIUM Priority (Score 50-79)
**Within 7 days**:
1. Add to nurture email campaign
2. Send case study relevant to their industry
3. Invite to product demo webinar
4. Follow up in 2 weeks

**Nurture Email Sequence**:
- Email 1 (Day 1): Case study - "[Industry] company reduced tickets by 70%"
- Email 2 (Day 7): Webinar invitation - "See AMINA AI in action"
- Email 3 (Day 14): Feature spotlight - "How AI handles [Challenge]"
- Email 4 (Day 30): Launch announcement + early bird pricing

---

### 📊 LOW Priority (Score <50)
**Automated sequence**:
1. Add to general email list
2. Monthly newsletter with product updates
3. Self-service resources (blog, knowledge base)
4. Re-qualify in 6 months

---

## Success Metrics

### Week 1-2 (Survey Launch)
- **Target**: 40-60% completion rate from Option A signups
- **High Priority Leads**: 15-20% of respondents
- **Response time**: <48 hours for high-priority outreach

### Week 3-4 (Qualification Phase)
- **Discovery Calls**: 50% of high-priority leads book calls
- **Beta Acceptance**: 20-30 companies confirmed for beta
- **Lead Quality**: Average lead score >60

### Month 2-3 (Pre-Launch)
- **Pipeline Value**: Track potential ARR from qualified leads
- **Conversion Rate**: 20-40% of high-priority leads convert to beta/trial
- **Feedback Loop**: Weekly product feedback from beta users

---

## Beta Program Selection Criteria

### Ideal Beta Customer (Select 20-30 companies):
- ✅ Lead Score: 80-100
- ✅ Industry: Mix of Telecom, Finance, E-commerce, SaaS
- ✅ Volume: 500+ inquiries/month
- ✅ Timeline: Immediate or within 1 month
- ✅ Engaged: Responded quickly, detailed answers
- ✅ Referenceable: Willing to provide testimonial/case study

### Beta Benefits to Offer:
- 3 months free access (full features)
- Dedicated onboarding + weekly check-ins
- Direct Slack/WhatsApp channel with founders
- Feature voting rights
- Co-marketing opportunity (case study, testimonial)
- Lifetime 25% discount after beta

---

## Files Reference
- Minimal form: `OPTION_A_MINIMAL_FORM.md`
- Demo request form: `OPTION_C_DEMO_FORM.md`
- Email templates: `EMAIL_TEMPLATES.md`
- Lead scoring: `LEAD_SCORING_SPREADSHEET.md`
