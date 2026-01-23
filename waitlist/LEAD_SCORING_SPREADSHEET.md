# AMINA AI Lead Scoring Spreadsheet

Complete guide to setting up automated lead scoring and segmentation in Google Sheets.

---

## Overview

**Purpose**: Automatically score and prioritize waitlist leads based on qualification criteria

**How it works**:
1. Google Forms responses feed into Google Sheets
2. Formulas calculate lead scores (0-100)
3. Leads are automatically segmented (High/Medium/Low priority)
4. Conditional formatting highlights hot leads
5. Dashboard provides visual analytics

---

## Step 1: Link Forms to Sheets

### For Option A (Minimal Waitlist Form)

1. Open your Option A Google Form
2. Click "Responses" tab
3. Click green Sheets icon 📊 "Create Spreadsheet"
4. Choose "Create a new spreadsheet"
5. Name it: **"AMINA AI - Waitlist Responses"**

### For Option B (Priority Survey)

1. Open your Option B Google Form
2. Click "Responses" tab
3. Click green Sheets icon 📊
4. Name it: **"AMINA AI - Priority Survey Responses"**

---

## Step 2: Master Spreadsheet Setup

Create a master spreadsheet that combines both forms:

1. Create new Google Sheet: **"AMINA AI - Lead Scoring Master"**
2. Create 4 tabs:
   - **Dashboard** (visual overview)
   - **Waitlist Data** (import from Option A)
   - **Survey Data** (import from Option B)
   - **Scored Leads** (combined + scored)

---

## Step 3: Waitlist Data Tab Setup

### Import Option A Data

1. Go to "Waitlist Data" tab
2. In cell A1, use IMPORTRANGE formula:

```excel
=IMPORTRANGE("URL_OF_OPTION_A_RESPONSES_SHEET", "Form Responses 1!A:F")
```

Replace `URL_OF_OPTION_A_RESPONSES_SHEET` with the actual URL of your Option A responses sheet.

3. Click "Allow access" when prompted

### Expected Columns:
- A: Timestamp
- B: Work Email
- C: Full Name
- D: Company Name
- E: Company Size
- F: Biggest Challenge (optional)

---

## Step 4: Survey Data Tab Setup

### Import Option B Data

1. Go to "Survey Data" tab
2. In cell A1, use IMPORTRANGE formula:

```excel
=IMPORTRANGE("URL_OF_OPTION_B_RESPONSES_SHEET", "Form Responses 1!A:I")
```

3. Click "Allow access"

### Expected Columns:
- A: Timestamp
- B: Work Email
- C: Full Name
- D: Company Name
- E: Industry
- F: Company Size
- G: Monthly Support Volume
- H: Primary Support Challenge
- I: Timeline

---

## Step 5: Scored Leads Tab Setup

### Column Headers (Row 1):

| A | B | C | D | E | F | G | H | I | J | K | L | M |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Email | Full Name | Company | Industry | Company Size | Monthly Volume | Challenge | Timeline | Signup Date | Survey Completed | Lead Score | Priority | Actions |

### Formula Setup

#### Column A (Email) - Row 2:
```excel
=QUERY('Waitlist Data'!B:B, "SELECT * WHERE Col1 IS NOT NULL AND Col1 != 'Work Email'", 0)
```

#### Column B (Full Name) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Waitlist Data'!B:C,2,FALSE),"")
```

#### Column C (Company) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Waitlist Data'!B:D,3,FALSE),"")
```

#### Column D (Industry) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Survey Data'!B:E,4,FALSE),"Not surveyed")
```

#### Column E (Company Size) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Survey Data'!B:F,5,FALSE),VLOOKUP(A2,'Waitlist Data'!B:E,4,FALSE))
```

#### Column F (Monthly Volume) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Survey Data'!B:G,6,FALSE),"Unknown")
```

#### Column G (Challenge) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Survey Data'!B:H,7,FALSE),VLOOKUP(A2,'Waitlist Data'!B:F,5,FALSE))
```

#### Column H (Timeline) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Survey Data'!B:I,8,FALSE),"Unknown")
```

#### Column I (Signup Date) - Row 2:
```excel
=IFERROR(VLOOKUP(A2,'Waitlist Data'!B:A,1,FALSE),"")
```

#### Column J (Survey Completed) - Row 2:
```excel
=IF(D2="Not surveyed","❌ No","✅ Yes")
```

---

## Step 6: Lead Scoring Formula (Column K)

### Scoring Logic:

**Total Score: 0-100 points**

- **Industry Score** (0-25 points)
- **Company Size Score** (0-20 points)
- **Monthly Volume Score** (0-30 points)
- **Timeline Score** (0-15 points)
- **Challenge Score** (0-10 points)

### Formula in K2:

```excel
=IF(D2="Not surveyed",0,
  (IF(D2="Telecommunications",25,
   IF(D2="Financial Services/Fintech",25,
   IF(D2="E-commerce/Retail",20,
   IF(D2="SaaS/Technology",20,
   IF(D2="Healthcare",15,
   IF(D2="Travel/Hospitality",15,
   IF(D2="Education",10,5)))))))
  +
  (IF(E2="51-200 employees",20,
   IF(E2="201-1,000 employees",20,
   IF(E2="11-50 employees",15,
   IF(E2="1,001+ employees",10,
   IF(E2="1-10 employees",5,0))))))
  +
  (IF(F2="10,000+ inquiries/month",30,
   IF(F2="5,000-10,000 inquiries/month",30,
   IF(F2="2,001-5,000 inquiries/month",25,
   IF(F2="501-2,000 inquiries/month",20,
   IF(F2="100-500 inquiries/month",10,
   IF(F2="Less than 100 inquiries/month",5,0)))))))
  +
  (IF(H2="Immediately (within 2 weeks)",15,
   IF(H2="Within 1 month",15,
   IF(H2="1-3 months",10,
   IF(H2="3-6 months",5,
   IF(H2="6-12 months",2,0))))))
  +
  (IF(OR(G2="High volume overwhelming our team",G2="Slow response times (missing SLAs)",G2="Scaling support without hiring more agents"),10,
   IF(OR(G2="Too many repetitive questions",G2="Need 24/7 coverage without hiring night shifts"),8,
   IF(OR(G2="High agent turnover/burnout",G2="Poor customer satisfaction scores (CSAT/NPS)"),6,5))))
))
```

### Copy Formula Down:
1. Click cell K2
2. Copy (Ctrl+C)
3. Select K3 to K[last row]
4. Paste (Ctrl+V)

---

## Step 7: Priority Label (Column L)

### Formula in L2:

```excel
=IF(K2=0,"⏸️ INCOMPLETE",
  IF(K2>=80,"🔥 HIGH",
  IF(K2>=50,"⭐ MEDIUM","📊 LOW")))
```

### Copy Formula Down:
Same as Column K (copy L2, paste to L3:L[last row])

---

## Step 8: Action Items (Column M)

### Formula in M2:

```excel
=IF(L2="🔥 HIGH","Call within 48h + Demo",
  IF(L2="⭐ MEDIUM","Nurture campaign + Case study",
  IF(L2="📊 LOW","Automated email sequence",
  "Send survey")))
```

---

## Step 9: Conditional Formatting

### Highlight High Priority Leads:

1. Select column L (Priority column), starting from L2
2. Format → Conditional formatting
3. Format rules:
   - **Rule 1**: Text contains "HIGH" → Background: Red (#FF0000), Text: White
   - **Rule 2**: Text contains "MEDIUM" → Background: Yellow (#FFFF00), Text: Black
   - **Rule 3**: Text contains "LOW" → Background: Green (#00FF00), Text: Black
   - **Rule 4**: Text contains "INCOMPLETE" → Background: Gray (#CCCCCC), Text: Black

### Highlight Lead Scores:

1. Select column K (Lead Score), starting from K2
2. Format → Conditional formatting
3. Color scale:
   - Min value: 0 → Red
   - Midpoint: 50 → Yellow
   - Max value: 100 → Green

---

## Step 10: Dashboard Tab Setup

### Key Metrics (Visual Summary)

#### A1: Total Waitlist Signups
```excel
=COUNTA('Scored Leads'!A2:A)
```

#### B1: Survey Completion Rate
```excel
=COUNTIF('Scored Leads'!J2:J,"✅ Yes")/COUNTA('Scored Leads'!A2:A)
```
Format as percentage (Format → Number → Percent)

#### C1: High Priority Leads
```excel
=COUNTIF('Scored Leads'!L2:L,"🔥 HIGH")
```

#### D1: Medium Priority Leads
```excel
=COUNTIF('Scored Leads'!L2:L,"⭐ MEDIUM")
```

#### E1: Low Priority Leads
```excel
=COUNTIF('Scored Leads'!L2:L,"📊 LOW")
```

#### F1: Average Lead Score
```excel
=AVERAGE('Scored Leads'!K2:K)
```

### Dashboard Layout:

```
┌─────────────────────────────────────────────────────────────┐
│  AMINA AI - Waitlist Dashboard                              │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Total Signups: [A1]         Survey Completion: [B1]       │
│                                                              │
│  🔥 High Priority: [C1]                                     │
│  ⭐ Medium Priority: [D1]                                   │
│  📊 Low Priority: [E1]                                      │
│                                                              │
│  Average Lead Score: [F1]                                   │
│                                                              │
├─────────────────────────────────────────────────────────────┤
│  INDUSTRY BREAKDOWN                                          │
│  (Insert pivot table or chart)                              │
├─────────────────────────────────────────────────────────────┤
│  COMPANY SIZE BREAKDOWN                                      │
│  (Insert pivot table or chart)                              │
├─────────────────────────────────────────────────────────────┤
│  MONTHLY VOLUME BREAKDOWN                                    │
│  (Insert pivot table or chart)                              │
└─────────────────────────────────────────────────────────────┘
```

### Create Charts:

#### Chart 1: Priority Distribution (Pie Chart)
1. Insert → Chart
2. Data range: Dashboard!C1:E1
3. Chart type: Pie chart
4. Customize: Add labels with values

#### Chart 2: Industry Breakdown (Bar Chart)
1. Data → Pivot table
2. Rows: Industry
3. Values: COUNT of Industry
4. Insert → Chart from pivot table
5. Chart type: Bar chart

#### Chart 3: Lead Scores Over Time (Line Chart)
1. Data range: 'Scored Leads'!I2:I, K2:K (Signup Date, Lead Score)
2. Chart type: Line chart
3. X-axis: Signup Date
4. Y-axis: Lead Score

---

## Step 11: Automated Notifications

### Set Up Email Alerts for High Priority Leads:

1. Tools → Script editor
2. Paste this Google Apps Script:

```javascript
function sendHighPriorityAlert() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Scored Leads');
  const data = sheet.getDataRange().getValues();

  // Get last row data
  const lastRow = data[data.length - 1];
  const email = lastRow[0];
  const name = lastRow[1];
  const company = lastRow[2];
  const score = lastRow[10];
  const priority = lastRow[11];

  // If high priority, send alert
  if (priority === "🔥 HIGH") {
    const recipient = "your-email@example.com"; // Replace with your email
    const subject = `🔥 High Priority Lead: ${company}`;
    const body = `
New high-priority lead detected!

Name: ${name}
Company: ${company}
Email: ${email}
Lead Score: ${score}

Action: Contact within 48 hours for demo.

View lead: ${SpreadsheetApp.getActiveSpreadsheet().getUrl()}
    `;

    MailApp.sendEmail(recipient, subject, body);
  }
}
```

3. Save (Ctrl+S), name it "High Priority Alert"
4. Set up trigger:
   - Edit → Current project's triggers
   - Add Trigger
   - Function: sendHighPriorityAlert
   - Event source: From spreadsheet
   - Event type: On form submit
   - Save

---

## Step 12: Weekly Reporting

### Automated Weekly Email Report:

Add this function to the same Google Apps Script:

```javascript
function sendWeeklyReport() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Dashboard');

  const totalSignups = sheet.getRange('A1').getValue();
  const surveyRate = (sheet.getRange('B1').getValue() * 100).toFixed(1);
  const highPriority = sheet.getRange('C1').getValue();
  const mediumPriority = sheet.getRange('D1').getValue();
  const lowPriority = sheet.getRange('E1').getValue();
  const avgScore = sheet.getRange('F1').getValue().toFixed(1);

  const recipient = "your-email@example.com"; // Replace
  const subject = `📊 AMINA AI Waitlist Weekly Report`;
  const body = `
AMINA AI Waitlist - Weekly Report

📈 GROWTH METRICS:
• Total signups: ${totalSignups}
• Survey completion rate: ${surveyRate}%
• Average lead score: ${avgScore}

🎯 LEAD QUALITY:
• 🔥 High priority: ${highPriority}
• ⭐ Medium priority: ${mediumPriority}
• 📊 Low priority: ${lowPriority}

📊 View full dashboard: ${SpreadsheetApp.getActiveSpreadsheet().getUrl()}

— Automated Report
  `;

  MailApp.sendEmail(recipient, subject, body);
}
```

### Set Up Weekly Trigger:
1. Edit → Current project's triggers
2. Add Trigger
3. Function: sendWeeklyReport
4. Event source: Time-driven
5. Type: Week timer
6. Day: Monday
7. Time: 9am-10am
8. Save

---

## Step 13: Export for CRM

### Prepare High-Priority Leads for Export:

1. Go to "Scored Leads" tab
2. Data → Create a filter
3. Filter column L (Priority) → Select "🔥 HIGH"
4. File → Download → CSV

### Import to CRM:
- **HubSpot**: Contacts → Import
- **Salesforce**: Leads → Import
- **Zoho CRM**: Leads → Import

### Map Fields:
- Email → Email
- Full Name → Name
- Company → Company Name
- Lead Score → Custom field: "Lead Score"
- Priority → Custom field: "Priority"

---

## Step 14: Advanced Analytics

### Add These Formulas to Dashboard:

#### Survey Completion by Priority:
```excel
=COUNTIFS('Scored Leads'!J2:J,"✅ Yes",'Scored Leads'!L2:L,"🔥 HIGH")/COUNTIF('Scored Leads'!L2:L,"🔥 HIGH")
```

#### Average Time to Survey Completion:
```excel
=AVERAGE(ARRAYFORMULA(IF('Scored Leads'!J2:J="✅ Yes",
  VLOOKUP('Scored Leads'!A2:A,'Survey Data'!B:A,1,FALSE)-'Scored Leads'!I2:I,"")))
```

#### Conversion Rate (High Priority):
```excel
=COUNTIF('Scored Leads'!L2:L,"🔥 HIGH")/COUNTA('Scored Leads'!A2:A)
```

---

## Sample Data for Testing

### Add Sample Rows to Test Formulas:

| Email | Full Name | Company | Industry | Size | Volume | Challenge | Timeline |
|-------|-----------|---------|----------|------|--------|-----------|----------|
| test1@telecom.com | John Doe | Telecom Co | Telecommunications | 51-200 | 5,000-10,000 | High volume | Immediately |
| test2@fintech.ng | Jane Smith | FinPay | Financial Services | 201-1,000 | 2,001-5,000 | Slow response | Within 1 month |
| test3@shop.com | Ahmed Hassan | E-Shop | E-commerce | 11-50 | 501-2,000 | Repetitive questions | 1-3 months |

Expected Scores:
- test1@telecom.com: **95** (🔥 HIGH)
- test2@fintech.ng: **90** (🔥 HIGH)
- test3@shop.com: **65** (⭐ MEDIUM)

---

## Troubleshooting

### Formula Errors:

**#REF! Error**:
- Check IMPORTRANGE URLs are correct
- Ensure you clicked "Allow access"

**#N/A Error**:
- VLOOKUP can't find match
- Add IFERROR to handle missing data

**#VALUE! Error**:
- Check data types (text vs. number)
- Ensure column references are correct

### Data Not Updating:

1. Check IMPORTRANGE formulas
2. Refresh the page (Ctrl+R)
3. Data → "Refresh all" (if using pivot tables)

### Slow Performance:

1. Limit IMPORTRANGE to only needed columns
2. Use QUERY instead of VLOOKUP for large datasets
3. Create a daily snapshot instead of live import

---

## Maintenance Schedule

### Daily:
- Check for new high-priority leads (email alerts)
- Review and respond to high-priority leads within 48h

### Weekly:
- Review dashboard metrics
- Export high-priority leads to CRM
- Send follow-up surveys to incomplete leads

### Monthly:
- Analyze lead quality trends
- Adjust scoring formula based on actual conversions
- Clean up duplicate entries

---

## Success Metrics (Track Monthly)

### Lead Quality Metrics:
- **High Priority %**: Target 15-20% of total signups
- **Survey Completion**: Target 40-60%
- **Average Lead Score**: Target >60

### Conversion Metrics (Post-Launch):
- **High Priority → Demo**: Target 50%
- **Demo → Trial**: Target 40%
- **Trial → Paid**: Target 25%

### Response Metrics:
- **Time to Contact**: <48 hours for high priority
- **Email Open Rate**: Target 40%+
- **Email Reply Rate**: Target 5%+

---

## Files Reference
- Forms: `OPTION_A_MINIMAL_FORM.md`, `OPTION_B_SURVEY.md`
- Email templates: `EMAIL_TEMPLATES.md`
- Implementation guide: `IMPLEMENTATION_GUIDE.md`
