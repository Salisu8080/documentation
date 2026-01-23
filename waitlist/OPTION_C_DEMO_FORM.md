# Option C: Detailed Demo Request Form (For High-Intent Leads)

## Overview
- **Goal**: Qualify serious buyers for personalized demos
- **Expected Conversion**: 15-30%
- **Use Case**: "Request a Demo" CTA, enterprise outreach, high-intent leads
- **Completion Time**: ~3 minutes

---

## When to Use This Form

### Primary Use Cases:
1. **Demo Request Page**: Dedicated "Request a Demo" landing page
2. **High-Intent Leads**: Visitors from paid ads, enterprise referrals
3. **Sales Outreach**: After discovery call, send demo scheduling form
4. **Late-Stage Qualification**: Leads who completed Option B and showed strong interest

### DO NOT Use for:
- Initial waitlist signup (too many fields, will scare people off)
- Cold traffic from social media
- General "learn more" inquiries

---

## Google Form Setup Instructions

### Step 1: Create New Form
1. Go to https://forms.google.com
2. Click "+ Blank form"
3. Title: "Request a Personalized Demo - AMINA AI"
4. Description:
```
See AMINA AI in action with a personalized demo tailored to your business.

Our team will show you:
✅ How AMINA AI handles YOUR specific use cases
✅ Integration with your existing tools
✅ Custom ROI estimate for your business
✅ Implementation timeline and pricing

Takes 3 minutes to complete. We'll contact you within 24 hours to schedule.
```

---

### Step 2: Form Settings
- ✅ **Collect email addresses**: ON
- ✅ **Limit to 1 response**: ON
- ✅ **Send response receipts**: ON
- ❌ **Require sign-in**: OFF
- **Progress bar**: ON (Settings → Presentation)

---

## Questions (12 fields)

### Section 1: Contact Information
*Section header: "Contact Information"*

#### Question 1: Work Email
- **Question**: Work Email
- **Type**: Short answer
- **Required**: YES
- **Validation**:
  - Response validation: Text → Contains → `@`
  - For enterprise focus, block free emails:
    - Text → Regular expression → Does not match
    - Pattern: `(gmail|yahoo|hotmail|outlook)\.com`
    - Error: "Please use your company email address"

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

#### Question 4: Job Title/Role
- **Question**: What is your job title or role?
- **Type**: Dropdown
- **Required**: YES
- **Description**: "This helps us tailor the demo to your needs"
- **Options**:
```
Founder/CEO
Co-Founder
Head of Customer Success
Head of Customer Support
Customer Support Manager
Customer Experience Manager
Operations Manager
CTO/Head of Engineering
VP of Engineering
Product Manager
Head of Operations
Business Owner
Other (please specify)
```

---

### Section 2: Company Context
*Section header: "Tell Us About Your Business"*
*Section description: "This helps us prepare a relevant demo"*

#### Question 5: Industry
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
Professional Services (Legal, Consulting, etc.)
Government/Public Sector
Manufacturing
Real Estate
Media/Entertainment
Logistics/Delivery
Food & Beverage
Other (please specify)
```

---

#### Question 6: Company Size
- **Question**: How many employees does your company have?
- **Type**: Dropdown
- **Required**: YES
- **Options**:
```
1-10 employees
11-50 employees
51-200 employees
201-1,000 employees
1,001-5,000 employees
5,000+ employees
```

---

#### Question 7: Monthly Support Volume
- **Question**: How many customer inquiries does your business handle per month?
- **Type**: Dropdown
- **Required**: YES
- **Description**: "Include all channels: email, phone, chat, social media, etc."
- **Options**:
```
Less than 100 inquiries/month
100-500 inquiries/month
501-2,000 inquiries/month
2,001-5,000 inquiries/month
5,000-10,000 inquiries/month
10,000-20,000 inquiries/month
20,000+ inquiries/month
```

---

### Section 3: Current Support Setup
*Section header: "Current Support Operations"*

#### Question 8: Current Support Tool(s)
- **Question**: What tools do you currently use for customer support?
- **Type**: Checkboxes (allow multiple)
- **Required**: NO (optional)
- **Description**: "Select all that apply"
- **Options**:
```
□ Zendesk
□ Intercom
□ Freshdesk
□ Help Scout
□ Gorgias
□ HubSpot Service Hub
□ Salesforce Service Cloud
□ Zoho Desk
□ LiveChat
□ Tidio
□ Drift
□ Custom built solution
□ None - we use email only
□ None - we use phone only
□ None - we use WhatsApp only
□ Other (please specify)
```

---

#### Question 9: Support Channels Used
- **Question**: Which support channels does your business currently use?
- **Type**: Checkboxes (allow multiple)
- **Required**: NO (optional)
- **Description**: "Select all that apply"
- **Options**:
```
□ Email
□ Live web chat
□ Phone/Call center
□ WhatsApp Business
□ Facebook Messenger
□ Instagram Direct Messages
□ Twitter/X DMs
□ In-app messaging
□ SMS/Text
□ Help Center/Knowledge Base
□ Other (please specify)
```

---

### Section 4: Demo Focus
*Section header: "What Should We Focus On?"*

#### Question 10: Primary Support Challenge
- **Question**: What is your PRIMARY customer support challenge?
- **Type**: Dropdown
- **Required**: YES
- **Description**: "Choose the one that matters most to your business"
- **Options**:
```
High volume overwhelming our team
Slow response times (missing SLAs)
Too many repetitive questions
Need 24/7 coverage without hiring night shifts
Scaling support without hiring more agents
High agent turnover/burnout
Poor customer satisfaction scores (CSAT/NPS)
Language barriers (need multilingual support)
Integration with existing tools (CRM, helpdesk)
Lack of support analytics/insights
Inconsistent responses across team
Difficulty handling peak periods (seasonal, launches)
Other (please specify)
```

---

#### Question 11: Implementation Timeline
- **Question**: When do you need a customer support solution?
- **Type**: Dropdown
- **Required**: YES
- **Description**: "This helps us prioritize your demo"
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

#### Question 12: Phone Number
- **Question**: Phone Number (for callback/SMS updates)
- **Type**: Short answer
- **Required**: NO (optional)
- **Description**: "Optional - only if you'd like us to call you directly"
- **Validation** (if provided):
  - Response validation: Text → Regular expression → Matches
  - Pattern: `^\+?[1-9]\d{1,14}$`
  - Error: "Please enter a valid phone number (e.g., +2348012345678)"

---

#### Question 13: Additional Information
- **Question**: Anything else you'd like us to know before the demo?
- **Type**: Paragraph
- **Required**: NO (optional)
- **Description**: "Optional - share any specific questions, integration requirements, or use cases"

---

## Confirmation Message

```
Thank you for requesting a demo! 🎉

Here's what happens next:

✅ WITHIN 24 HOURS
Our team will review your information and email you to schedule your personalized demo.

✅ BEFORE THE DEMO
We'll prepare:
• Relevant case study from your industry ([Industry])
• Custom ROI estimate based on your volume ([Volume])
• Integration recommendations for your tools ([Current Tools])
• Solutions for your specific challenge ([Challenge])

✅ DURING THE DEMO (20-30 minutes)
We'll show you:
• How AMINA AI handles YOUR specific use cases
• Live walkthrough of the dashboard
• Integration with your existing channels
• Pricing options and implementation timeline
• Custom ROI calculation for your business

✅ AFTER THE DEMO
We'll send you:
• Recording of the demo (for your team)
• Detailed proposal with pricing
• Implementation roadmap
• Next steps if you're interested

Questions before your demo? Email us at hello@amina-ai.com

Talk soon!

— The AMINA AI Team

---

P.S. Based on your timeline ([Timeline]), we recommend booking your demo in the next [timeframe] to stay on track.
```

---

## Lead Scoring for Demo Requests

### Automatic Scoring (Higher threshold than Option B)

#### 🔥 CRITICAL Priority (Score: 90-100)
**Criteria**:
- Job Title: Founder/CEO, Head of Customer Success/Support
- Industry: Telecom, Finance, E-commerce, SaaS
- Company Size: 51-1,000 employees
- Volume: 5,000+ inquiries/month
- Timeline: Immediately or within 1 month
- Current Tool: Using enterprise solution (Zendesk, Salesforce, Intercom)

**Action**:
- Call within 2 hours (not email - call!)
- Founder/CTO should join demo
- Prepare detailed case study + custom proposal
- Offer beta access or expedited onboarding

---

#### 🔥 HIGH Priority (Score: 80-89)
**Criteria**:
- Job Title: Manager-level roles
- Industry: Healthcare, Travel, Education, Professional Services
- Company Size: 11-50 or 1,000+ employees
- Volume: 2,000-5,000/month
- Timeline: Within 1-3 months
- Current Tool: Mid-market solution or email only

**Action**:
- Email + call within 24 hours
- Standard demo with industry focus
- Share case study before demo
- Prepare pricing proposal

---

#### ⭐ MEDIUM Priority (Score: 60-79)
**Criteria**:
- Job Title: Operations Manager, Product Manager
- Company Size: 11-50 employees
- Volume: 500-2,000/month
- Timeline: 3-6 months
- Current Tool: Free/basic tool or none

**Action**:
- Email within 48 hours
- Standard demo
- Focus on education and ROI
- Nurture for later conversion

---

#### 📊 LOW Priority (Score: <60)
**Criteria**:
- Company Size: 1-10 employees
- Volume: <500/month
- Timeline: 6+ months or "just exploring"
- Job Title: Other/unspecified

**Action**:
- Automated email with demo video link
- Invite to group webinar instead of 1-on-1 demo
- Self-service resources
- Re-qualify in 3-6 months

---

## Demo Scheduling Email Template

**Subject Options** (A/B test):
1. "[Name], let's schedule your AMINA AI demo"
2. "Your personalized demo is ready - [Company Name]"
3. "[Name], see how AMINA AI can solve [Challenge]"

**Email Body**:

```
Hi [Name],

Thanks for requesting a demo of AMINA AI!

I reviewed your submission and I'm excited to show you how AMINA AI can help [Company Name] solve [Challenge].

WHAT I'LL PREPARE FOR YOUR DEMO:

Based on your information:
• Industry: [Industry]
• Monthly Volume: [Volume]
• Current Tools: [Tools]
• Primary Challenge: [Challenge]

I'll prepare:
✅ Case study from a [Industry] business with similar volume
✅ Live demo showing how to handle [Industry]-specific inquiries
✅ Integration walkthrough for [Current Tools]
✅ Custom ROI estimate (potential savings + efficiency gains)
✅ Implementation timeline to meet your [Timeline] target

THE DEMO (20-30 minutes):

I'll show you:
1. How AMINA AI learns from your knowledge base (5 min)
2. Live conversation examples for [Industry] (10 min)
3. Dashboard walkthrough + analytics (5 min)
4. Integration with [Channels] (5 min)
5. Pricing + Q&A (5 min)

SCHEDULE YOUR DEMO:

Pick a time that works for you:
[Calendar Link - Calendly/Google Calendar]

Or reply with your availability and I'll send a calendar invite.

WHO SHOULD JOIN?

I recommend inviting:
• Your support/success team lead (to discuss operations)
• Technical lead (to discuss integrations, if applicable)
• Decision-maker (to discuss pricing and timeline)

Looking forward to showing you what AMINA AI can do!

Best regards,
[Your Name]
[Title], AMINA AI
[Phone Number]
[Email]

P.S. Based on your [Timeline] timeline, I recommend scheduling this week so we can get your implementation started on time.

---

AMINA AI | AI-Powered Customer Support
[Website] | hello@amina-ai.com
```

---

## Demo Preparation Checklist

### Before the Demo (24 hours before):

- [ ] Research prospect's company (website, LinkedIn, social media)
- [ ] Identify 3-5 common inquiries for their industry
- [ ] Prepare relevant case study (same industry or similar volume)
- [ ] Calculate custom ROI estimate
- [ ] Test screen share and demo environment
- [ ] Prepare proposal template with their company name

### Day of Demo (1 hour before):

- [ ] Review their form responses
- [ ] Check if they're using any integration partners (Zoho, Salesforce, etc.)
- [ ] Prepare specific examples for their channels (WhatsApp, chat, etc.)
- [ ] Have pricing deck ready
- [ ] Test internet connection and audio

### During Demo:

- [ ] Start with their challenge, not your product
- [ ] Show, don't tell (live demo > slides)
- [ ] Use their company name and examples throughout
- [ ] Ask questions to keep them engaged
- [ ] Address objections as they come up
- [ ] End with clear next steps

### After Demo (within 2 hours):

- [ ] Send thank you email with recording
- [ ] Attach proposal with pricing
- [ ] Share relevant case studies
- [ ] Schedule follow-up call or trial start date
- [ ] Log notes in CRM

---

## Demo Script Outline (20-30 minutes)

### Introduction (2 min)
```
"Hi [Name], thanks for joining! Before we dive in, I want to make sure we focus on what matters to you.

I saw that [Company] handles [Volume] inquiries/month and your biggest challenge is [Challenge]. Is that still accurate? Anything else you'd like me to focus on today?"

[Listen and adjust demo accordingly]
```

### Problem Validation (3 min)
```
"So if I understand correctly, you're dealing with [restate their challenge]. How long has this been a problem? What have you tried so far?

[Listen and empathize]

Great, I think AMINA AI can really help here. Let me show you how..."
```

### Demo Part 1: Knowledge Base (5 min)
```
"First, I'll show you how AMINA AI learns from your business.

[Screen share: Upload knowledge base]

You upload your FAQs, product docs, policies—whatever your support team uses to answer questions. AMINA AI indexes everything in about 5 minutes.

[Show example document upload]

Now watch what happens when a customer asks a question...

[Show live conversation example]

AMINA AI doesn't just keyword match—it understands context. Let me show you a [Industry]-specific example..."

[Show 2-3 relevant examples]
```

### Demo Part 2: Omnichannel Support (5 min)
```
"Now, you mentioned you use [Channels]. Let me show you how AMINA AI works across all channels.

[Show WhatsApp integration / web chat / Facebook]

Customers can reach you on any channel, and AMINA AI handles conversations consistently. All data flows into one dashboard.

[Show unified inbox]

Your team sees all conversations in one place—no more switching between tools."
```

### Demo Part 3: Human Handoff (3 min)
```
"Of course, AI can't handle everything. When AMINA AI isn't confident (below 80% threshold), it escalates to your team with full context.

[Show handoff example]

See how your agent receives the full conversation history? No need to ask the customer to repeat themselves.

Your team can also jump in anytime to take over a conversation."
```

### Demo Part 4: Analytics (4 min)
```
"One of my favorite features is analytics. You get real-time insights into:
• Response times
• Resolution rates
• Customer satisfaction
• Most common questions
• AI performance

[Show dashboard]

This helps you identify trends, improve your knowledge base, and make data-driven decisions.

For [Company], based on your [Volume], you'd see [custom metric projections]."
```

### Custom ROI Calculation (3 min)
```
"Let me show you the potential ROI for [Company].

Current state:
• [Volume] inquiries/month
• Average handling time: [estimate] minutes
• Support team size: [estimate from their info]
• Monthly cost: ₦[estimate]

With AMINA AI (assuming 70% automation):
• [Calculated] inquiries automated
• [Calculated] hours saved per month
• Cost savings: ₦[Calculated]/month
• ROI: [Calculated]%

Does this align with your expectations?"
```

### Pricing & Next Steps (5 min)
```
"Based on your volume, I recommend the [Plan] plan at ₦[Price]/month.

This includes:
• [Benefits specific to their needs]
• Onboarding support
• Integration with [their tools]

Since you're looking to implement [Timeline], here's what the process looks like:

Week 1: Onboarding + knowledge base setup
Week 2: Testing + team training
Week 3: Soft launch on one channel
Week 4: Full rollout

We can get you live by [specific date].

What questions do you have?"
```

### Close (2 min)
```
"I'll send you:
• Recording of this demo
• Detailed proposal with pricing
• Case study from [Industry]
• Next steps to get started

Based on what you've seen, do you think AMINA AI is a good fit for [Company]?

[If yes]: Great! Let's schedule a follow-up to finalize details and kick off onboarding.

[If maybe]: No problem. What additional information would help you make a decision?

[If no]: I understand. Can you share what's holding you back so I can address it?"
```

---

## Common Objections & Responses

### Objection 1: "This seems expensive."
**Response**:
```
"I understand. Let's look at the ROI again. You're currently spending ₦[Estimate] on support. AMINA AI costs ₦[Price] but saves you ₦[Savings] per month by automating 70% of inquiries.

Net savings: ₦[Net]/month. That's a [X]% ROI.

Plus, you can scale support without scaling costs proportionally. What part of the pricing concerns you most?"
```

---

### Objection 2: "We tried chatbots before and they didn't work."
**Response**:
```
"That's a common experience, and I'm glad you brought it up. Most chatbots use pre-programmed responses—they break when customers ask something unexpected.

AMINA AI is different. It learns from YOUR specific business knowledge and understands context. It's not rule-based—it's AI-powered.

That's why our customers see 70-80% automation rates vs. 30-40% with traditional chatbots.

Would you like to do a trial so you can see the difference firsthand?"
```

---

### Objection 3: "We need to think about it."
**Response**:
```
"Absolutely, this is an important decision. To help you think through it, what specific concerns or questions do you still have?

[Listen and address]

Also, based on your [Timeline] timeline, when do you need to make a decision to stay on track?

[Create gentle urgency]

Would it help if I scheduled a follow-up call for [Date] so you have time to discuss with your team?"
```

---

### Objection 4: "Can it integrate with [obscure tool]?"
**Response**:
```
[If yes]: "Yes, we have a native integration with [Tool]. I'll include setup documentation in my follow-up email."

[If no, but possible]: "We don't have a native integration yet, but we support webhooks and APIs. Our technical team can help you connect [Tool] using Zapier or custom integration. Would you like me to loop in our technical team to discuss?"

[If no, not possible]: "We don't support [Tool] directly right now, but it's on our roadmap. In the meantime, you could use [Alternative workflow]. Would that work for your use case?"
```

---

## Success Metrics for Demo Requests

### Conversion Rates:
- **Demo Request → Demo Scheduled**: 70-80%
- **Demo Scheduled → Demo Completed**: 80-90% (account for no-shows)
- **Demo Completed → Trial Started**: 40-60%
- **Trial Started → Paid Customer**: 25-40%

### Response Times:
- **Critical Priority**: Call within 2 hours
- **High Priority**: Email + call within 24 hours
- **Medium Priority**: Email within 48 hours
- **Low Priority**: Automated email, group webinar invite

### Demo Quality:
- **Average demo duration**: 25-30 minutes
- **Follow-up email sent**: Within 2 hours of demo
- **Proposal sent**: Within 24 hours of demo
- **Follow-up call scheduled**: Within 5 days of demo

---

## Integration with CRM

### HubSpot Workflow:
1. Demo request submitted → Create deal in "Demo Requested" stage
2. Demo scheduled → Move to "Demo Scheduled" stage
3. Demo completed → Move to "Demo Completed" stage
4. Proposal sent → Move to "Proposal Sent" stage
5. Trial started → Move to "Trial" stage
6. Paid → Move to "Customer" stage

### Salesforce Lead Scoring:
- Add demo request fields to Lead object
- Create lead scoring rules based on criteria above
- Route high-priority leads to senior sales reps
- Auto-assign leads based on industry expertise

---

## Files Reference
- Minimal form: `OPTION_A_MINIMAL_FORM.md`
- Survey form: `OPTION_B_SURVEY.md`
- Email templates: `EMAIL_TEMPLATES.md`
- Landing page copy: `LANDING_PAGE_COPY.md`
- Implementation: `IMPLEMENTATION_GUIDE.md`
