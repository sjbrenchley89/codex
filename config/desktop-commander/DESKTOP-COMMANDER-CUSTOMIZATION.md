# Desktop Commander Customization for 9 Turnbull Court (9TC)

## Overview

This customization tailors the Desktop Commander MCP (Model Context Protocol) server for the specific needs of the 9 Turnbull Court residential duplex development project management workflow.

**Project:** 9 Turnbull Court Duplex Development  
**Location:** Brunswick West VIC 3055  
**Purpose:** Streamline document management, project tracking, and team coordination

## What is Desktop Commander?

Desktop Commander is an MCP server that extends Claude's capabilities to:
- Search, read, and manage files on your computer
- Execute terminal commands and manage processes
- Handle Excel, PDF, and DOCX files natively
- Provide real-time process interaction (SSH, databases, servers)
- Stream command output and manage long-running tasks

## Customizations for 9TC

### 1. **Custom Configuration** (`9tc-desktop-commander-config.json`)

Enhanced safety and project-specific settings:

#### Project Defaults
- **Google Drive Folder ID** - Link to 9TC master folder for document sync
- **Document Register Sheet ID** - Reference to master PMO workbook
- **Project Data Path** - Local backup and cache location
- **Folder Organization** - Predefined structure for:
  - Drawings & CAD files
  - Documents Register
  - Invoices & Financial Records
  - Permits & Approvals
  - RFI Correspondence

#### File Type Associations
Automatic detection and routing for:
- **Drawings**: `.dwg`, `.pdf`, `.dxf`, `.rvt` (Revit)
- **Specifications**: `.pdf`, `.docx`, `.txt`
- **Schedules**: `.xlsx`, `.xls`, `.csv`
- **Invoices**: `.pdf`, `.xlsx`
- **Correspondence**: `.pdf`, `.docx`, `.eml`
- **Site Documentation**: `.jpg`, `.png`, `.gif`, `.heic`

#### Auto-Classification Rules
Pattern matching for intelligent document routing:
- **Invoice Detection**: "INV-", "Invoice", "Payment Request"
- **RFI Detection**: "RFI", "Request for Information"
- **Drawing Detection**: "DWG", "Drawing", "Plan", "Section", "Elevation"
- **Permit Detection**: "Permit", "Approval", "Certificate", "Compliance"
- **Variation Detection**: "Variation", "Change Order", "CO"

#### Safety Settings
- ✅ Audit logging enabled with 10MB rotation
- ✅ Command timeout: 300 seconds (5 minutes)
- ✅ Max concurrent processes: 5
- ✅ Symlink traversal prevention
- ✅ Confirmation required for file deletion

#### Performance Settings
- Directory depth limit: 5 levels
- Context overflow protection enabled
- Large file threshold: 100MB
- Caching enabled with 1-hour TTL

### 2. **Custom Onboarding Prompts** (`9tc-onboarding-prompts.json`)

10 project-specific quick-start templates:

#### Document & File Management
1. **Process New Project Documents** - Scan Downloads, classify, and organize into project structure
2. **Analyze Project Drawings & Plans** - Extract, catalog, and track construction drawings
3. **Supplier & Contractor Database** - Build master contact list from existing documents

#### Financial Tracking
4. **Invoice & Payment Tracking** - Extract invoice data, identify overdue payments, track budget

#### Project Coordination
5. **RFI (Request for Information) Management** - Track, organize, and follow up on RFIs
6. **Variation Orders & Change Management** - Track change orders and budget impacts
7. **Meeting Minutes & Action Items** - Extract and track meeting outcomes and responsibilities

#### Compliance & Documentation
8. **Permits & Approvals Tracking** - Monitor regulatory compliance and approval status
9. **Site Progress & Photo Documentation** - Catalog and organize visual project records

#### Reporting
10. **Generate 9TC Project Status Report** - Create comprehensive project summaries

## Implementation

### Step 1: Set Up Configuration Files

The custom config and prompts files should be placed in the Desktop Commander configuration directory:

**For Claude Desktop:**
```
~/.claude/desktop-commander/config/
├── config.json (9TC version)
└── onboarding-prompts.json (9TC version)
```

**For Docker:**
```
/app/config/
├── config.json (9TC version)
└── onboarding-prompts.json (9TC version)
```

### Step 2: Configure Project Paths

Update these values in `9tc-desktop-commander-config.json`:

```json
"projectDefaults": {
  "googleDriveFolderId": "YOUR_9TC_GOOGLE_DRIVE_FOLDER_ID",
  "documentRegisterSheetId": "1Qs4tnxCadvpaKB5b-JMtZ-IurA1cZoQtFL5NL-Pw8po",
  "projectDataPath": "~/9TC-Project-Data"
}
```

- **Google Drive Folder ID**: Found in the URL of your 9TC master folder
  - URL: `https://drive.google.com/drive/folders/YOUR_FOLDER_ID`
  
- **Document Register Sheet ID**: From the 9TC PMO Master Google Sheet URL
  - Already configured: `1Qs4tnxCadvpaKB5b-JMtZ-IurA1cZoQtFL5NL-Pw8po`

- **Project Data Path**: Local directory where you want project files cached/organized

### Step 3: Create Project Directory Structure

Desktop Commander can auto-create this structure. Run:

```
/Desktop Commander
  Create organized knowledge/documents folder
  Location: ~/9TC-Project-Data
```

Or manually create:

```
~/9TC-Project-Data/
├── Drawings & CAD/
│   ├── Floor Plans/
│   ├── Elevations/
│   ├── Sections/
│   └── Details/
├── Documents Register/
│   ├── Specifications/
│   ├── Schedules/
│   └── General Correspondence/
├── Invoices/
│   ├── Pending/
│   ├── Paid/
│   └── Overdue/
├── Permits & Approvals/
│   ├── Building Permit/
│   ├── Council Approvals/
│   └── Compliance Certificates/
├── RFI Register/
│   ├── Pending/
│   ├── Resolved/
│   └── Supplier Responses/
├── Site Photos/
│   ├── Progress Reports/
│   └── Milestones/
└── Meeting Minutes/
    └── Action Items/
```

## Key Features for 9TC Workflow

### 🏗️ Construction Document Management
- **Automatic Classification**: Documents are intelligently routed based on type
- **Revision Tracking**: Drawing revisions are identified and superseded versions marked
- **Specification Management**: Technical docs extracted and cataloged

### 💰 Financial Tracking
- **Invoice Data Extraction**: Supplier, amount, GST, due date automatically extracted
- **Payment Status**: Identifies overdue invoices and cash flow issues
- **Budget Monitoring**: Tracks variations and cost impacts
- **Supplier Reports**: Generates summaries by contractor/supplier

### 📧 RFI & Correspondence Management
- **Auto-logging**: New RFIs automatically added to register
- **Response Tracking**: Monitors due dates and response status
- **Impact Assessment**: Flags blocking or critical RFIs
- **Audit Trail**: Complete history of all correspondence

### ✅ Compliance & Permits
- **Permit Tracking**: All approvals logged with valid periods
- **Expiry Alerts**: Identifies permits expiring soon
- **Compliance Certificates**: Tracks certification status
- **Regulatory Documentation**: Organizes council requirements

### 🔄 Change Control
- **Variation Orders**: All changes logged and tracked
- **Cost Impact**: Automatic cost variation calculation
- **Schedule Impact**: Tracks schedule changes and delays
- **Approval Workflow**: Monitors change approval status

### 📸 Visual Documentation
- **Photo Organization**: Site photos cataloged by date/location
- **Progress Tracking**: Visual milestones documented
- **Before/After**: Comparison photos organized
- **Metadata Preservation**: Camera, date, location data retained

## Usage Tips

### Quick Start Examples

**Process documents in your Downloads:**
```
/Desktop Commander → Process New Project Documents
```

**Analyze invoices and extract data:**
```
/Desktop Commander → Invoice & Payment Tracking
```

**Track RFI responses:**
```
/Desktop Commander → RFI Management
```

**Generate project status report:**
```
/Desktop Commander → Generate 9TC Project Status Report
```

### Advanced Usage

**Custom Queries:**
- "Show me all overdue invoices in ~/9TC-Project-Data/Invoices"
- "Analyze the latest drawings and create a marked-up list of revisions"
- "Generate a supplier payment summary for the last month"
- "Find all RFIs mentioning structural or foundation work"
- "Create a visual progress timeline from site photos"

**Process Management:**
- Monitor long-running data export processes
- Run batch document classification jobs
- Schedule regular syncs with Google Drive
- Execute backup scripts with real-time output

## Security & Safety

### Protected Operations
✅ Symlink traversal prevention  
✅ Command blocklist for dangerous operations  
✅ File deletion confirmation required  
✅ Comprehensive audit logging  
✅ Automatic log rotation (10MB max)  

### Blocked Commands (Safety)
The following dangerous commands are blocked:
- `format`, `mount`, `umount`, `mkfs`, `fdisk`, `dd`
- `sudo`, `su`, `passwd`
- User management: `adduser`, `useradd`, `usermod`, `groupadd`
- Destructive patterns: `rm -rf /`, `dd if=/dev/zero`

### Audit Trail
All tool calls are logged with:
- Timestamp
- Command/tool used
- Arguments and parameters
- Success/failure status
- User context

Logs rotate at 10MB and include operation history for compliance and troubleshooting.

## Troubleshooting

### Configuration Not Loading
1. Ensure JSON is valid (use a JSON validator)
2. Check file permissions (should be readable by Claude Desktop)
3. Restart Claude Desktop after updating config

### Prompts Not Appearing
1. Verify `onboarding-prompts.json` is in the correct location
2. Check that the `categories` array includes `"9tc-project"`
3. Clear Claude Desktop cache: `rm -rf ~/.claude/cache`

### Google Drive Integration
1. Verify Folder ID is correct (from URL)
2. Check that the folder is accessible from your Google account
3. Ensure Google Drive API is enabled in your project settings

### File Organization Issues
1. Verify project paths exist and are writable
2. Check folder permissions
3. Use "Create organized knowledge/documents folder" prompt to auto-generate structure

## Integration with 9TC PMO System

### With 9TC PMO Automation (Google Apps Script)
- Desktop Commander can read and organize files before Apps Script processes them
- Preprocessed documents are cleaner for classification
- Local cache improves processing speed

### With 9TC PM Hub (React/TanStack)
- Desktop Commander handles backend data extraction
- Export features can feed data to PM Hub dashboards
- File analysis can populate backend databases

### With Codex Repository
- Store analysis scripts and templates in Codex
- Version control for Desktop Commander configs
- Reusable prompts and commands in wiki

## Repository Integration

This customization is tracked in:
- **Branch**: `claude/desktop-commander-customize-qql3xu`
- **Repositories**:
  - `sjbrenchley89/-9tc-pmo-automation`
  - `sjbrenchley89/9-turnbull-pm-hub`
  - `sjbrenchley89/codex`

### Configuration Files Location
```
/config/
├── desktop-commander/
│   ├── 9tc-config.json
│   └── 9tc-onboarding-prompts.json
└── README.md (this file)
```

## Updates & Maintenance

### Updating Prompts
Edit `9tc-onboarding-prompts.json` to:
- Modify prompt text
- Add new project-specific templates
- Update categories and tags
- Change icons or descriptions

### Updating Configuration
Edit `9tc-config.json` to:
- Add new file type associations
- Update auto-classification patterns
- Modify safety settings
- Change performance settings

### Versioning
- Configuration version tracked in `config.json`
- Prompts version tracked in `onboarding-prompts.json`
- All changes should be committed to the designated branch

## Support & Feedback

For issues or feature requests:
1. Check the [Desktop Commander FAQ](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/main/FAQ.md)
2. Review [SECURITY.md](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/main/SECURITY.md)
3. Open an issue on the [Desktop Commander GitHub](https://github.com/wonderwhy-er/DesktopCommanderMCP)

## License

This customization is for the 9 Turnbull Court PMO project.  
Desktop Commander is licensed under [MIT License](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/main/LICENSE)

---

**Last Updated**: August 2026  
**Maintained By**: 9TC PMO Team  
**Branch**: `claude/desktop-commander-customize-qql3xu`
