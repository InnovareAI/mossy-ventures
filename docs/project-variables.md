# Mossy Ventures Project Variables & Configuration

## Airtable Configuration
### Base Structure
- **Base ID**: `appBgMykPwnIR54yz`
- **Base URL**: https://airtable.com/appBgMykPwnIR54yz/tbleRwanWbTRz2F1S/viwHuwsXzcR2gmasy
- **Primary Tables**:
  - Investors (`tbleRwanWbTRz2F1S`)
  - Startups (tblXXXXXXXXXXXXXX)
  - Programs (tblXXXXXXXXXXXXXX)
  - Deals (tblXXXXXXXXXXXXXX)
  - Events (tblXXXXXXXXXXXXXX)
  - Content (tblXXXXXXXXXXXXXX)

### Field Mappings
#### Investors Table
- Name (fldXXXXXX)
- Email (fldXXXXXX)
- Phone (fldXXXXXX)
- LinkedIn URL (fldXXXXXX)
- Investment Stage (single select: New, Active, Experienced, Mentor)
- Program Participation (multi-select: SAC, APIS, SIA, Trans-Atlantic)
- Investment History (linked records to Deals)
- Total Invested (rollup)
- Portfolio Companies (count)
- Status (single select: Prospect, Qualified, Active, Alumni)
- Tags (multi-select)
- Notes (long text)
- Created Date (created time)
- Last Contact (date)

#### Startups Table
- Company Name (fldXXXXXX)
- Founder Name (fldXXXXXX)
- Founder Email (fldXXXXXX)
- Website (fldXXXXXX)
- Industry (single select)
- Stage (single select: Pre-seed, Seed, Series A, Series B+)
- Program Applied (multi-select: SAC, APIS, SIA, Trans-Atlantic)
- Pitch Deck (attachment)
- Status (single select: Applied, Screening, Accepted, Funded, Rejected)
- Funding Ask (currency)
- Valuation (currency)
- Next Steps (long text)

#### Programs Table
- Program Name (fldXXXXXX)
- Program Type (single select: SAC, APIS, SIA, Trans-Atlantic)
- Start Date (date)
- End Date (date)
- Cohort Number (number)
- Max Participants (number)
- Current Enrollment (count)
- Status (single select: Planning, Open, In Progress, Completed)
- Investment Amount (currency)
- Participating Investors (linked records)
- Selected Startups (linked records)

### API Access
- **Personal Access Token**: `pat6vpRqhoZH8q798.c2f2eb4ea290699c7849442f55b1be19f2c1495a136a439ff2713419abbe33b1`
- **Environment Variables**:
  - `AIRTABLE_PAT`: (stored securely)
  - `AIRTABLE_BASE_ID`: appBgMykPwnIR54yz
  - `AIRTABLE_API_URL`: https://api.airtable.com/v0/

### Business Rules
- Never delete investor or startup records (archive instead)
- Investor journey stages must follow: Prospect → Qualified → Active → Alumni
- Startup pipeline must follow: Applied → Screening → Accepted → Funded
- All program participants must have signed agreements before "Active" status
- Investment records require both investor and startup linked records
- Content performance metrics update daily via automation

## ActiveCampaign Configuration
### Account Details
- **Account URL**: https://mossyventures.activehosted.com
- **API URL**: https://mossyventures.api-us1.com
- **API Key**: (to be configured)

### Lists
1. **All Contacts** (Master List)
2. **Angel Investors** (Segmented by experience level)
3. **Startup Founders** (Active fundraising)
4. **Program Alumni** (Past participants)
5. **Newsletter Subscribers** (General interest)

### Tags Structure
#### Investor Tags
- `investor_new` - New to angel investing
- `investor_active` - Currently investing
- `investor_experienced` - 5+ investments
- `investor_mentor` - Available for mentorship
- `program_sac` - Seattle Angel Conference
- `program_apis` - APIS Health Angels
- `program_sia` - Startup Investor Accelerator
- `program_transatlantic` - Trans-Atlantic program

#### Startup Tags
- `startup_preseed` - Pre-seed stage
- `startup_seed` - Seed stage
- `startup_seriesa` - Series A
- `startup_healthcare` - Healthcare/MedTech focus
- `startup_b2b` - B2B SaaS
- `startup_b2c` - Consumer focused
- `pitch_ready` - Ready to pitch
- `funded` - Successfully funded

#### Engagement Tags
- `webinar_attended` - Attended webinar
- `event_registered` - Registered for event
- `high_engagement` - Opens all emails
- `download_guide` - Downloaded resources

### Custom Fields
- Investment Experience (dropdown)
- Investment Range (dropdown)
- Industry Preference (multiselect)
- LinkedIn URL (text)
- Company Name (text)
- Funding Stage (dropdown)
- Program Interest (multiselect)
- Investor Type (dropdown)

### Automation Workflows
1. **New Investor Welcome Series** (ID: 1)
2. **Startup Application Flow** (ID: 2)
3. **Program Preparation Series** (ID: 3)
4. **Post-Investment Follow-up** (ID: 4)
5. **Newsletter Engagement Scoring** (ID: 5)
6. **Event Registration Confirmation** (ID: 6)

## n8n Workflow Automation
### Instance Details
- **Workflow URL**: https://workflows.innovareai.com/workflow/ZIY8jUA8xY5Dr7Nb
- **API Base URL**: https://workflows.innovareai.com/api/v1/
- **API Key**: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI5Yzg4NDFiNy1kODhmLTRlYWMtYWZiOS03N2Y5ODlmYzk5MTYiLCJpc3MiOiJuOG4iLCJhdWQiOiJwdWJsaWMtYXBpIiwiaWF0IjoxNzUzNDY0OTYwLCJleHAiOjE3NTU5ODY0MDB9.jmZ_lVOGPFZ3bO_XnBYZ_zrmiXL386U0NaLgrvxaxNk`

### Workflows
1. **Airtable → ActiveCampaign Sync**
   - Workflow ID: ZIY8jUA8xY5Dr7Nb
   - Trigger: Airtable record changes
   - Actions: Update AC contacts, apply tags

2. **New Investor Processing**
   - Trigger: New Airtable investor record
   - Actions: Create AC contact, start welcome series, notify team

3. **Startup Application Handler**
   - Trigger: Form submission webhook
   - Actions: Create Airtable record, tag in AC, send confirmation

4. **Weekly Metrics Aggregation**
   - Schedule: Every Monday 9 AM PST
   - Actions: Pull metrics from AC, update Airtable dashboard

### Webhook Endpoints
- New Investor: `https://workflows.innovareai.com/webhook/mossy-investor-new`
- Startup Application: `https://workflows.innovareai.com/webhook/mossy-startup-apply`
- Event Registration: `https://workflows.innovareai.com/webhook/mossy-event-register`

## GitHub Repository
- **Repository**: InnovareAI/mossy-ventures
- **Main Branch**: main
- **Deploy Branch**: production
- **Documentation Path**: /docs/
- **Automation Scripts**: /automations/
- **Templates**: /templates/

## Integration Webhooks
### Airtable → ActiveCampaign (via n8n)
- New Investor: https://workflows.innovareai.com/webhook/mossy-investor-new
- Startup Application: https://workflows.innovareai.com/webhook/mossy-startup-apply
- Program Registration: https://workflows.innovareai.com/webhook/mossy-event-register

### ActiveCampaign → Airtable (via n8n)
- Email Engagement: https://workflows.innovareai.com/webhook/mossy-email-metrics
- Tag Updates: https://workflows.innovareai.com/webhook/mossy-tag-sync
- Unsubscribes: https://workflows.innovareai.com/webhook/mossy-unsubscribe

## Environment Variables Summary
```bash
# Airtable
AIRTABLE_PAT=pat6vpRqhoZH8q798.c2f2eb4ea290699c7849442f55b1be19f2c1495a136a439ff2713419abbe33b1
AIRTABLE_BASE_ID=appBgMykPwnIR54yz
AIRTABLE_INVESTORS_TABLE=tbleRwanWbTRz2F1S

# ActiveCampaign
ACTIVECAMPAIGN_API_KEY=[to be configured]
ACTIVECAMPAIGN_ACCOUNT_URL=https://mossyventures.activehosted.com

# n8n
N8N_API_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI5Yzg4NDFiNy1kODhmLTRlYWMtYWZiOS03N2Y5ODlmYzk5MTYiLCJpc3MiOiJuOG4iLCJhdWQiOiJwdWJsaWMtYXBpIiwiaWF0IjoxNzUzNDY0OTYwLCJleHAiOjE3NTU5ODY0MDB9.jmZ_lVOGPFZ3bO_XnBYZ_zrmiXL386U0NaLgrvxaxNk
N8N_INSTANCE_URL=https://workflows.innovareai.com
N8N_WORKFLOW_ID=ZIY8jUA8xY5Dr7Nb

# GitHub
GITHUB_TOKEN=[to be configured]
```

## Security Notes
- All API keys stored in environment variables
- Rotate tokens quarterly
- Use read-only permissions where possible
- Audit access logs monthly
- Backup Airtable data weekly
- n8n API token expires: Check expiration date regularly