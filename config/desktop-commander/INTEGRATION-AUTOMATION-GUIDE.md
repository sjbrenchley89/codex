# Desktop Commander Integration Automation Guide
## 9 Turnbull Court (9TC) PMO

**Version:** 2.0.0-integration  
**Updated:** August 2026  
**Purpose:** Seamless workflow automation between Desktop Commander, Google Sheets, Email, and Project Systems

---

## Table of Contents

1. [Overview](#overview)
2. [Integration Architecture](#integration-architecture)
3. [Google Sheets Auto-Sync](#google-sheets-auto-sync)
4. [Email Auto-Import](#email-auto-import)
5. [Automated Backups](#automated-backups)
6. [Data Export & Reporting](#data-export--reporting)
7. [Automation Workflows](#automation-workflows)
8. [Setup Instructions](#setup-instructions)
9. [Troubleshooting](#troubleshooting)

---

## Overview

### What is Integration Automation?

Integration Automation connects Desktop Commander with your existing 9TC systems to create seamless, hands-free workflows:

- **Google Sheets Sync** - Real-time data synchronization
- **Email Auto-Import** - Automatic document processing from inbox
- **Automated Backups** - Daily encrypted backups to Google Drive
- **Report Generation** - Automatic monthly reports to stakeholders
- **Alert Monitoring** - Expiry alerts, overdue tracking, escalation

### Benefits

✅ **Save Time** - Eliminate manual data entry and file organization  
✅ **Reduce Errors** - Consistent data classification and filing  
✅ **Stay Current** - Always working with latest versions  
✅ **Prevent Delays** - Proactive alerts for critical items  
✅ **Professional Communication** - Automated reports and statements  
✅ **Data Protection** - Secure backups and version control  
✅ **Compliance** - Complete audit trail for regulations  

---

## Integration Architecture

```
┌─────────────────────────────────────────────────────────────┐
│              9TC Project Integration System                  │
└─────────────────────────────────────────────────────────────┘

    ┌──────────────┐
    │ Gmail Inbox  │
    │  (Incoming)  │
    └──────┬───────┘
           │ Auto-Extract
           ▼
    ┌──────────────────────────┐
    │ Desktop Commander        │
    │ - File Processing        │
    │ - Classification         │
    │ - Organization           │
    └──────┬───────────────────┘
           │
    ┌──────┴────────┬──────────────┬──────────────┐
    │               │              │              │
    ▼               ▼              ▼              ▼
┌─────────┐  ┌───────────────┐  ┌──────────┐  ┌──────────┐
│ Google  │  │ Local Backup  │  │ Google   │  │ Reports  │
│ Sheets  │  │ & Archive     │  │ Drive    │  │ & Email  │
│ (Sync)  │  │ (Daily)       │  │ (Cloud)  │  │ (Auto)   │
└────┬────┘  └───────────────┘  └──────────┘  └──────────┘
     │
     │ Update & Validate
     ▼
┌──────────────────────┐
│ Stakeholder Reports  │
│ - Monthly Status     │
│ - Supplier Statements│
│ - Compliance Reports │
└──────────────────────┘
```

---

## Google Sheets Auto-Sync

### Overview

Real-time synchronization between Desktop Commander and 9TC PMO Master Sheet ensures all stakeholders have current data.

**Master Sheet ID:** `1Qs4tnxCadvpaKB5b-JMtZ-IurA1cZoQtFL5NL-Pw8po`

### Synchronized Sheets

#### 1. **Invoices Sheet** (🧾 INVOICES)
**Sync Frequency:** Every 15 minutes

**Sync Direction:** Bi-directional
- Desktop Commander → Google Sheets: New invoices, status updates
- Google Sheets → Desktop Commander: Payment confirmations, adjustments

**Data Columns:**
| Column | Field | Auto-Populated |
|--------|-------|---|
| A | Supplier | Yes (from email) |
| B | Invoice Number | Yes (from PDF) |
| C | Amount | Yes (OCR from invoice) |
| D | GST | Calculated |
| E | Due Date | Yes (from invoice) |
| F | Date Received | Yes (from email) |
| G | Status | Manual - Pending/Paid/Overdue |
| H | Notes | Optional |

**Automatic Actions:**
- ✅ Extract invoice data from PDF attachments
- ✅ Calculate GST automatically
- ✅ Flag overdue invoices (>30 days)
- ✅ Categorize by supplier
- ✅ Alert on payment deadline (3 days before)

#### 2. **RFI Register** (📝 RFI_REGISTER)
**Sync Frequency:** Every 15 minutes

**Data Columns:**
| Column | Field | Auto-Populated |
|--------|-------|---|
| A | RFI Number | Yes (auto-generated) |
| B | Date Issued | Yes (from email) |
| C | Contractor | Yes (from sender) |
| D | Description | Yes (from email body) |
| E | Due Date | Yes (from RFI) |
| F | Date Responded | Manual - when response received |
| G | Status | Auto - Open/Responded/Late |
| H | Impact | Manual - High/Medium/Low |

**Automatic Actions:**
- ✅ Log RFIs automatically
- ✅ Calculate response time
- ✅ Alert on approaching due dates
- ✅ Escalate overdue RFIs (7+ days)
- ✅ Track by contractor

#### 3. **Variations** (⚡ VARIATIONS)
**Sync Frequency:** Every 15 minutes

**Data Columns:**
| Column | Field | Auto-Populated |
|--------|-------|---|
| A | Variation Number | Yes (auto-generated) |
| B | Date Issued | Yes (from document) |
| C | Description | Yes (from CO) |
| D | Original Amount | Yes (from CO) |
| E | Variation Amount | Yes (from CO) |
| F | Schedule Days | Yes (from CO) |
| G | Status | Manual - Pending/Approved/Rejected |
| H | Approval Date | Manual - when approved |

**Automatic Actions:**
- ✅ Extract variation details
- ✅ Calculate total cost impact
- ✅ Track schedule impact
- ✅ Alert on approval deadline
- ✅ Maintain variation history

#### 4. **Document Register** (📚 DOCUMENT_REGISTER)
**Sync Frequency:** Every 30 minutes

**Data Columns:**
| Column | Field | Auto-Populated |
|--------|-------|---|
| A | Document ID | Yes (auto-generated) |
| B | Title | Yes (from filename/content) |
| C | Type | Yes (from classification) |
| D | Date Received | Yes (from file date) |
| E | Source | Yes (from email/folder) |
| F | Location | Yes (filepath/URL) |
| G | Status | Manual - Current/Archived/Superseded |
| H | Notes | Optional |

**Automatic Actions:**
- ✅ Index all project documents
- ✅ Tag by type and date
- ✅ Mark superseded versions
- ✅ Maintain file locations
- ✅ Create audit trail

#### 5. **Permits & Approvals** (📜 PERMITS_APPROVALS)
**Sync Frequency:** Daily

**Data Columns:**
| Column | Field | Auto-Populated |
|--------|-------|---|
| A | Permit Type | Manual |
| B | Permit Number | Yes (from document) |
| C | Date Issued | Yes (from permit) |
| D | Expiry Date | Yes (from permit) |
| E | Authority | Manual |
| F | Status | Yes (calculates from expiry) |
| G | Notes | Optional |

**Automatic Actions:**
- ✅ Extract permit numbers and dates
- ✅ Calculate expiry status (Current/Expiring/Expired)
- ✅ Alert 60, 30, 14 days before expiry
- ✅ Flag expired permits (red alert)
- ✅ Track renewal status

### Setup Instructions

#### Step 1: Google Service Account Setup

```bash
# 1. Go to Google Cloud Console
# https://console.cloud.google.com/

# 2. Create new project: "9TC-Desktop-Commander"

# 3. Enable APIs:
# - Google Sheets API
# - Google Drive API

# 4. Create Service Account
# - Service account name: "9tc-commander"
# - Grant roles: "Editor"

# 5. Create JSON key
# - Download and save to: ~/.9tc/google-credentials.json
# - Set permissions: chmod 600 ~/.9tc/google-credentials.json

# 6. Share master sheet with service account
# - Copy service account email (ends with @iam.gserviceaccount.com)
# - Share 9TC PMO Master Sheet with "Editor" access
```

#### Step 2: Configure Desktop Commander

```json
// In 9tc-integration-automation-config.json
"googleSheets": {
  "enabled": true,
  "masterSheetId": "1Qs4tnxCadvpaKB5b-JMtZ-IurA1cZoQtFL5NL-Pw8po",
  "authentication": {
    "credentialsPath": "~/.9tc/google-credentials.json",
    "scopes": ["sheets", "drive"]
  }
}
```

#### Step 3: Enable Sync

```bash
# In Claude Desktop
/Desktop Commander → Set Up Google Sheets Auto-Sync

# Verify connection
/Desktop Commander → Test Google Sheets Connection
```

---

## Email Auto-Import

### Overview

Automatically process incoming emails and extract project documents into the appropriate folders and sheets.

### Auto-Import Rules

#### Rule 1: Invoice Auto-Import

**Trigger:** Email labeled "9TC-Invoices"
**Filters:**
- From: `invoices@*`, `accounts@*`, `billing@*`
- Subject contains: "invoice", "payment request", "tax invoice"
- Has attachment

**Actions:**
1. Extract PDF/Excel attachments
2. Save to `~/9TC-Project-Data/Invoices/`
3. Classify invoice data
4. Add to 🧾 INVOICES sheet
5. Tag email as "imported"
6. Alert if amount > $50,000

**Example Flow:**
```
Email arrives from supplier
         ↓
Filter matches "9TC-Invoices" + "Invoice"
         ↓
Extract PDF attachment
         ↓
OCR extract: Amount, Supplier, Due Date
         ↓
Save to ~/9TC-Project-Data/Invoices/
         ↓
Add row to 🧾 INVOICES sheet
         ↓
Email tagged "imported"
         ↓
Notification: "Invoice from Supplier added"
```

#### Rule 2: RFI Auto-Import

**Trigger:** Email labeled "9TC-RFIs"
**Filters:**
- Subject contains: "RFI", "Request for Information", "clarification"
- Has attachment

**Actions:**
1. Extract attachments
2. Save to `~/9TC-Project-Data/RFI Register/`
3. Extract RFI metadata
4. Add to 📝 RFI_REGISTER sheet
5. Tag email "rfi-pending"
6. Mark for review

**Auto-Extracted Data:**
- RFI Number (if available)
- Issue Date
- Contractor/Sender
- Due Date
- Description

#### Rule 3: Drawing Auto-Import

**Trigger:** Email labeled "9TC-Drawings"
**Filters:**
- Subject contains: "drawing", "plan", "CAD", "dwg", "revit"
- Attachment types: `.dwg`, `.pdf`, `.dxf`, `.rvt`, `.zip`

**Actions:**
1. Extract drawing files
2. Detect and extract revision (A, B, C, etc.)
3. Organize by type (Plans, Elevations, Sections, Details)
4. Save to `~/9TC-Project-Data/Drawings & CAD/`
5. Update 📚 DOCUMENT_REGISTER
6. Mark superseded versions
7. Detect if revision is new

**Drawing Organization:**
```
Drawings & CAD/
├── Floor Plans/
│   ├── A100_FloorPlan_Rev-B.pdf (CURRENT)
│   ├── A100_FloorPlan_Rev-A.pdf (SUPERSEDED)
│   └── A100_FloorPlan_Rev-C.pdf (NEW)
├── Elevations/
│   ├── A101_Elevations_Rev-B.pdf
│   └── A101_Elevations_Rev-A.pdf
├── Sections/
└── Details/
```

#### Rule 4: Permit Auto-Import

**Trigger:** Email labeled "9TC-Permits"
**Filters:**
- Subject contains: "permit", "approval", "certificate", "compliance"
- Has attachment

**Actions:**
1. Extract permit documents
2. Parse for expiry date
3. Save to `~/9TC-Project-Data/Permits & Approvals/`
4. Add to 📜 PERMITS_APPROVALS sheet
5. Set expiry alert (30 days before)
6. Tag email "permit-active"

**Auto-Extracted Data:**
- Permit Type
- Permit Number
- Date Issued
- Expiry Date
- Authority

### Setup Instructions

#### Step 1: Create Gmail Labels

```
In Gmail:
1. Settings → Labels → Create Label
2. Create these labels:
   - 9TC-Invoices
   - 9TC-RFIs
   - 9TC-Drawings
   - 9TC-Permits
   - 9TC-Imported (auto-apply)
```

#### Step 2: Create Gmail Filters

For each email type:
```
Gmail → Settings → Filters and Blocked Addresses → Create a new filter

Filter 1: Invoice Auto-Import
  From: invoices@*, accounts@*, billing@*
  Subject: contains "invoice" OR "payment request"
  Action: Apply label → 9TC-Invoices
  
Filter 2: RFI Auto-Import
  Subject: contains "RFI" OR "Request for Information"
  Action: Apply label → 9TC-RFIs
  
Filter 3: Drawing Auto-Import
  Subject: contains "drawing" OR "plan" OR "dwg"
  Attachment: has attachment
  Action: Apply label → 9TC-Drawings
  
Filter 4: Permit Auto-Import
  Subject: contains "permit" OR "approval"
  Action: Apply label → 9TC-Permits
```

#### Step 3: Configure in Desktop Commander

```bash
/Desktop Commander → Configure Email Auto-Import Rules
```

---

## Automated Backups

### Overview

Daily encrypted backups protect your 9TC project data against loss or corruption.

### Backup Configuration

**Frequency:** Daily at 2:00 AM  
**Location:** Google Drive (9TC Project Backups)  
**Encryption:** AES-256  
**Compression:** ZIP  
**Retention:** 7 daily, 4 weekly, 12 monthly  

### Backup Contents

#### Local Files
```
~/9TC-Project-Data/
├── Drawings & CAD/
├── Documents Register/
├── Invoices/
├── Permits & Approvals/
├── RFI Register/
├── Site Photos/
└── Meeting Minutes/
```

#### Google Sheets
```
9TC PMO Master Sheet
├── ⚙️ CONFIG
├── 🤖 AUTOMATION_SETUP
├── 📥 GMAIL_IMPORT
├── 📚 DOCUMENT_REGISTER
├── 🧾 INVOICES
├── 📝 RFI_REGISTER
├── 📜 PERMITS_APPROVALS
├── 🛒 PROCUREMENT
└── ⚡ VARIATIONS
```

### Retention Policy

| Backup Type | Retention | Count | Use Case |
|---|---|---|---|
| Daily | 7 days | 7 | Quick recovery (this week) |
| Weekly | 4 weeks | 4 | Recent recovery (this month) |
| Monthly | 12 months | 12 | Long-term archive |

**Oldest backups auto-delete when limits exceeded**

### Recovery Process

**Restore from daily backup:**
```bash
/Desktop Commander → Restore from Backup

Select:
- Backup date: [choose]
- Components: [select what to restore]
- Restore location: [choose]
```

**Restore steps:**
1. Choose backup date
2. Verify contents
3. Select restore location
4. Confirm and execute
5. Verify restoration

---

## Data Export & Reporting

### Automated Reports

#### 1. Monthly Project Report

**Schedule:** 1st of month at 9:00 AM  
**Recipients:** Project Manager, Principal, Finance, Contractor  
**Format:** PDF

**Contents:**
- Executive Summary
  - Project status (% complete)
  - Key metrics
  - Risks and issues
  
- Budget Status
  - Spent to date
  - Remaining budget
  - Cost variations
  - Contingency status
  
- Schedule Status
  - Progress vs. plan
  - Schedule variances
  - Critical path items
  - Delay impacts
  
- Invoice Summary
  - Total invoiced
  - Paid to date
  - Outstanding balance
  - Overdue invoices
  - Payment forecast
  
- RFI Status
  - Total issued
  - Responses received
  - Outstanding RFIs
  - Average response time
  - Overdue RFIs
  
- Variation Summary
  - Total variations
  - Cost impact
  - Schedule impact
  - Approved vs. pending
  
- Permits Status
  - Current permits
  - Expiring soon
  - Expired permits
  - Compliance status
  
- Risk Register
  - Active risks
  - Risk scores
  - Mitigation status
  - New risks
  
- Upcoming Milestones
  - Next 30 days
  - Critical dates
  - Resource planning

#### 2. Weekly Status Report

**Schedule:** Monday at 9:00 AM  
**Recipients:** Project Team  
**Format:** Email + PDF

**Contents:**
- Week summary
- Completed tasks
- In-progress items
- This week's issues
- Next week priorities
- Risks and blockers

#### 3. Supplier Payment Statement

**Schedule:** Monthly or on-demand  
**Recipients:** Individual suppliers  
**Format:** Excel + PDF

**Contents:**
- Supplier details
- All invoices (paid and pending)
- Payment dates and amounts
- Aging analysis
- Account balance
- Terms
- Notes

#### 4. Compliance & Permits Report

**Schedule:** Weekly  
**Recipients:** Project Manager, Principal  
**Format:** PDF

**Contents:**
- All active permits
- Expiry alerts (30, 60, 90 days)
- Compliance certificates
- Outstanding approvals
- Renewal requirements
- Action items

### Custom Report Generation

**Generate on-demand:**
```bash
/Desktop Commander → Generate 9TC Project Status Report

Select:
- Report type: [Monthly / Weekly / Supplier / Compliance]
- Date range: [choose]
- Recipients: [select]
- Format: [PDF / Excel / CSV]

Action: Generate and email
```

---

## Automation Workflows

### Daily Sync Workflow

**Time:** 6:00 AM daily

```
1. Sync Google Sheets ↓ local cache
2. Check new emails (tagged 9TC-*)
3. Process email attachments
4. Update document register
5. Check permit expiries
6. Check overdue RFIs
7. Check overdue invoices
8. Verify backup completion
9. Send health check summary
```

**Output:** Daily health check email

### Weekly Automation

**Schedule:** Monday 9:00 AM

```
1. Generate weekly status report
2. Update project dashboard
3. Calculate KPIs
4. Export drawing register
5. Email to stakeholders
6. Archive completed tasks
```

### Monthly Automation

**Schedule:** 1st of month 9:00 AM

```
1. Generate monthly report
2. Export financials
3. Generate supplier statements
4. Send to payment recipients
5. Archive previous month data
6. Generate compliance report
7. Email to stakeholders
8. Backup and verify
```

---

## Setup Instructions

### Phase 1: Google Sheets Integration (Week 1)

1. ✅ Create Google service account
2. ✅ Configure Desktop Commander
3. ✅ Test sync with one sheet
4. ✅ Expand to all sheets
5. ✅ Verify data accuracy

### Phase 2: Email Auto-Import (Week 2)

1. ✅ Create Gmail labels
2. ✅ Create Gmail filters
3. ✅ Set up Desktop Commander rules
4. ✅ Test with sample emails
5. ✅ Enable auto-tagging

### Phase 3: Automated Backups (Week 2)

1. ✅ Configure backup destination
2. ✅ Test first backup
3. ✅ Verify backup integrity
4. ✅ Test restore process
5. ✅ Enable automatic daily backups

### Phase 4: Reports & Exports (Week 3)

1. ✅ Configure report templates
2. ✅ Set up distribution lists
3. ✅ Test report generation
4. ✅ Schedule automated reports
5. ✅ Verify email delivery

### Phase 5: Monitoring & Alerts (Week 4)

1. ✅ Enable expiry alerts
2. ✅ Configure escalation workflows
3. ✅ Set up alert email groups
4. ✅ Test alert delivery
5. ✅ Review and refine thresholds

---

## Troubleshooting

### Google Sheets Connection Issues

**Problem:** "Connection refused" when syncing

**Solutions:**
1. Verify service account credentials file exists
   ```bash
   ls -l ~/.9tc/google-credentials.json
   ```

2. Check permissions are 600
   ```bash
   chmod 600 ~/.9tc/google-credentials.json
   ```

3. Verify service account has editor access to sheet
   - Share 9TC PMO Master Sheet with service account email
   
4. Check Google APIs are enabled
   - Console → APIs & Services → Enabled APIs
   - Verify "Google Sheets API" and "Google Drive API" are on

5. Restart Desktop Commander and test connection

**Problem:** "Sheet ID not found"

**Solution:**
- Verify sheet ID in config matches actual sheet
- Sheet ID is the long string in the URL
- Example: `https://docs.google.com/spreadsheets/d/1Qs4tnxCadvpaKB5b-JMtZ-IurA1cZoQtFL5NL-Pw8po/edit`
- ID is: `1Qs4tnxCadvpaKB5b-JMtZ-IurA1cZoQtFL5NL-Pw8po`

### Email Auto-Import Issues

**Problem:** Emails not being imported

**Solutions:**
1. Verify Gmail labels are created
   - Settings → Labels → Look for 9TC-* labels
   
2. Check email filters exist and are active
   - Settings → Filters and Blocked Addresses
   - Look for 9TC-* filters

3. Test filter manually
   - Send yourself a test email matching filter
   - Should auto-label within 1 minute

4. Verify Desktop Commander has Gmail access
   - Settings → Connected Accounts → Gmail
   - Should show "Connected"

5. Check attachment permissions
   - Some file types may be blocked
   - Verify .pdf, .xlsx, .dwg are allowed

**Problem:** Documents not going to right folder

**Solution:**
- Check file path in config
- Verify folders exist on filesystem
- Create folders if missing:
  ```bash
  mkdir -p ~/9TC-Project-Data/{Invoices,RFI\ Register,Drawings\ \&\ CAD,Permits\ \&\ Approvals,Site\ Photos}
  ```

### Backup Issues

**Problem:** Backup failed or incomplete

**Solutions:**
1. Check Google Drive space
   ```bash
   /Desktop Commander → Check Google Drive Storage
   ```

2. Verify backup destination folder exists
   - Check 9TC Project Backups folder in Google Drive

3. Check encryption key is available
   - Encryption key stored locally
   - Should not be moved or deleted

4. Review backup logs
   ```bash
   /Desktop Commander → View Backup Logs
   ```

### Report Generation Issues

**Problem:** Reports not being generated or emailed

**Solutions:**
1. Verify automation is enabled
   - Config: `"automation": {"enabled": true}`

2. Check task scheduler (varies by OS)
   - Windows: Task Scheduler
   - macOS: launchd
   - Linux: crontab

3. Verify recipient email addresses
   - Check distribution list in config
   - Verify emails are correct format

4. Test manual report generation
   - `/Desktop Commander → Generate 9TC Project Status Report`
   - If manual works, automation may be disabled

5. Check email account permissions
   - Verify service account has send permissions

---

## Best Practices

✅ **Regular Testing**
- Test each automation monthly
- Verify data accuracy in sheets
- Check backup integrity

✅ **Data Validation**
- Review auto-extracted data for accuracy
- Correct OCR errors manually
- Flag unusual values for review

✅ **Security**
- Keep credentials file secure (chmod 600)
- Never commit credentials to git
- Rotate credentials annually
- Enable 2FA on Google account

✅ **Monitoring**
- Review health check emails daily
- Check alert emails for issues
- Monitor backup completion
- Track automation success rates

✅ **Documentation**
- Document custom rules
- Keep audit logs
- Track changes to configurations
- Maintain recovery procedures

---

## Support & Maintenance

### Daily Checklist
- [ ] Review health check email
- [ ] Check for new RFIs/invoices
- [ ] Verify no sync errors

### Weekly Checklist
- [ ] Review weekly report
- [ ] Check backup status
- [ ] Verify permit alerts
- [ ] Check overdue items

### Monthly Checklist
- [ ] Review monthly report
- [ ] Verify all automations running
- [ ] Test backup recovery
- [ ] Review alert thresholds
- [ ] Archive completed tasks

---

**For issues or questions:**
- Contact: 9TC PMO Team
- Email: 9turnbull@gmail.com
- Documentation: This guide
- Version: 2.0.0-integration

---

_Last Updated: August 2026_  
_Maintained By: 9TC Integration Team_  
_Branch: claude/desktop-commander-customize-qql3xu_
