# Sales Pipeline Management Agent

## Overview

This example demonstrates how to implement an AI agent that automates sales pipeline management using **Model Context Protocol (MCP)** tools and the AI Operations Handbook for consistent, contextual sales operations.

## Agent Configuration

### Core Function
**Intelligent Lead Qualification & Deal Progression Automation**

The agent uses MCP tools to automatically qualify inbound leads, update deal stages, generate follow-up communications, and provide sales insights based on company methodology and proven templates.

### MCP Tool Configuration
```json
{
  "mcp_tools": {
    "salesforce": {
      "server": "mcp-salesforce",
      "capabilities": ["create_leads", "update_opportunities", "query_accounts", "create_activities"]
    },
    "hubspot": {
      "server": "mcp-hubspot",
      "capabilities": ["enrich_leads", "update_deals", "create_sequences", "track_engagement"]
    },
    "clearbit": {
      "server": "mcp-clearbit", 
      "capabilities": ["company_enrichment", "person_enrichment", "technographics"]
    },
    "email": {
      "server": "mcp-email",
      "capabilities": ["send_personalized", "create_sequences", "track_opens", "schedule_follow_up"]
    },
    "calendly": {
      "server": "mcp-calendly",
      "capabilities": ["create_booking_link", "schedule_meeting", "check_availability"]
    }
  }
}
```

### Context Integration
```yaml
# Agent Context Access
primary_contexts:
  - contexts/company/README.md          # Company positioning and value props
  - contexts/customers/README.md        # Buyer personas and decision criteria
  - contexts/competitors/README.md      # Competitive positioning and battle cards
  - contexts/departments/sales/         # Sales methodology and processes

template_access:
  - templates/sales/lead-qualification-email.md
  - templates/sales/discovery-call-agenda.md
  - templates/sales/proposal-outline.md
  - templates/sales/competitive-differentiation.md
```

## MCP Implementation Example

### Workflow: Inbound Lead Qualification

**Trigger**: New form submission or demo request

**MCP Tool Sequence**:

1. **Enrich Lead Data** (Clearbit MCP)
```json
{
  "tool": "mcp_clearbit_enrich_person",
  "parameters": {
    "email": "sarah.johnson@datatech.com",
    "include_company": true,
    "include_technographics": true
  }
}
```

2. **Company Intelligence** (Clearbit MCP)
```json
{
  "tool": "mcp_clearbit_company_lookup",
  "parameters": {
    "domain": "datatech.com",
    "include_metrics": ["employee_count", "revenue", "funding", "tech_stack"]
  }
}
```

3. **Calculate ICP Fit Score** (Custom Analysis)
Based on enriched data + customer persona contexts:
- Company size: 750 employees (✓ Fits mid-market ICP)
- Industry: SaaS/Technology (✓ High-fit industry)
- Role: VP of Operations (✓ Economic buyer persona)
- Pain points: Workflow automation (✓ Direct product fit)
**ICP Score: 8.5/10 (High Priority)**

4. **Create CRM Opportunity** (Salesforce MCP)
```json
{
  "tool": "mcp_salesforce_create_opportunity",
  "parameters": {
    "name": "DataTech Solutions - Workflow Automation",
    "account_name": "DataTech Solutions",
    "stage": "Qualification",
    "amount": 75000,
    "probability": 25,
    "close_date": "2024-04-15",
    "lead_source": "Website Demo Request",
    "icp_score": 8.5
  }
}
```

5. **Generate Personalized Outreach** (Content Generation)
Using contexts + templates + enriched data:

**Template Applied**: `templates/sales/high-priority-outreach.md`
**Context Used**: Company positioning + VP Operations persona + Tech industry context

6. **Send Qualification Email** (Email MCP)
```json
{
  "tool": "mcp_email_send_sequence",
  "parameters": {
    "to": "sarah.johnson@datatech.com",
    "sequence_id": "enterprise_qualification_v2",
    "personalization": {
      "company": "DataTech Solutions", 
      "role": "VP of Operations",
      "industry": "SaaS",
      "pain_points": ["manual reporting", "data silos", "team productivity"],
      "company_size": "750 employees"
    },
    "follow_up_schedule": [3, 7, 14]
  }
}
```

7. **Assign to Sales Rep** (Salesforce MCP)
```json
{
  "tool": "mcp_salesforce_assign_owner",
  "parameters": {
    "opportunity_id": "006XX000004C2Y3",
    "owner_id": "00570000001X5EAAA0",
    "assignment_reason": "High ICP fit - enterprise segment"
  }
}
```

8. **Create Meeting Link** (Calendly MCP)
```json
{
  "tool": "mcp_calendly_create_booking_link",
  "parameters": {
    "event_type": "enterprise_discovery_call",
    "duration": 30,
    "owner": "sarah.mitchell@techflow.com",
    "custom_questions": ["biggest_operational_challenge", "current_tools", "team_size"]
  }
}
```

### Generated Output Example

**Lead Data Input**:
- Company: DataTech Solutions (750 employees)
- Contact: Sarah Johnson, VP of Operations
- Source: Downloaded "Workflow Automation Guide"
- Form responses: "Manual reporting", "Data silos", "Team productivity"

**Agent-Generated Qualification Email**:
```
Subject: Streamlining Operations at DataTech Solutions - Quick Question

Hi Sarah,

I noticed you recently downloaded our workflow automation guide, and given your role as VP of Operations at DataTech Solutions, I imagine you're dealing with some of the exact challenges we help companies solve.

Based on your interest in automation and your focus on operational efficiency, I suspect your team might be struggling with:
- Manual reporting processes that eat up valuable time
- Data scattered across different systems making insights difficult  
- Productivity bottlenecks from repetitive manual tasks

These are incredibly common challenges for growing SaaS companies, and ones we've helped similar organizations solve with measurable results. For example, we recently helped a 800-person technology company reduce their monthly reporting time by 75% while improving data accuracy.

Given DataTech's growth trajectory and your focus on operational excellence, I'd love to understand:
1. What's your biggest operational efficiency challenge right now?
2. How are you currently handling workflow automation across your teams?
3. What would success look like if you could eliminate manual processes?

I have some specific ideas for how TechFlow could help DataTech achieve the kind of operational efficiency that supports your continued growth.

Would you be open to a brief 15-minute conversation to explore this?

[Book a time that works for you: calendly.com/sarah-mitchell/discovery]

Best regards,
Sarah Mitchell
Senior Account Executive, TechFlow Solutions

P.S. Since you're in the SaaS space, you might find our case study with CloudCorp interesting - they're a similar-sized company that achieved 300% productivity improvement with our platform.
```

## MCP Tool Capabilities

### 1. **Lead Intelligence MCP Tools**
- `mcp_clearbit_enrich_person`: Get detailed contact and company information
- `mcp_zoominfo_company_profile`: Access company size, revenue, and growth data
- `mcp_builtwith_tech_stack`: Analyze current technology infrastructure
- `mcp_apollo_contact_finder`: Find additional stakeholders and decision makers

### 2. **CRM Management MCP Tools**
- `mcp_salesforce_lead_conversion`: Convert qualified leads to opportunities
- `mcp_hubspot_deal_progression`: Automatically update deal stages based on activity
- `mcp_pipedrive_activity_logging`: Track all prospect interactions and engagement
- `mcp_salesforce_forecast_update`: Update sales forecasting based on pipeline changes

### 3. **Communication MCP Tools**
- `mcp_outreach_sequence_enrollment`: Add prospects to personalized email sequences
- `mcp_salesloft_cadence_management`: Manage multi-touch sales cadences
- `mcp_linkedin_sales_navigator`: Send personalized LinkedIn connection requests
- `mcp_vidyard_video_creation`: Generate personalized video messages

### 4. **Meeting & Scheduling MCP Tools**
- `mcp_calendly_smart_scheduling`: Intelligently schedule based on prospect timezone and preferences
- `mcp_chili_piper_routing`: Route qualified leads to appropriate sales reps
- `mcp_zoom_meeting_creation`: Generate custom meeting rooms with agenda templates
- `mcp_gong_call_analysis`: Analyze recorded calls for coaching and insights

## Automated Workflows

### Lead Scoring & Routing
```json
{
  "workflow_name": "intelligent_lead_routing",
  "trigger": "new_lead_created",
  "steps": [
    {
      "tool": "mcp_clearbit_enrich_person",
      "output": "enriched_profile"
    },
    {
      "tool": "mcp_custom_icp_scorer",
      "input": "enriched_profile", 
      "output": "icp_score"
    },
    {
      "condition": "icp_score >= 8.0",
      "tool": "mcp_salesforce_assign_to_enterprise_rep",
      "priority": "high"
    },
    {
      "condition": "icp_score >= 6.0 && icp_score < 8.0", 
      "tool": "mcp_salesforce_assign_to_mid_market_rep",
      "priority": "medium"
    },
    {
      "condition": "icp_score < 6.0",
      "tool": "mcp_hubspot_add_to_nurture_sequence",
      "priority": "low"
    }
  ]
}
```

### Deal Progression Automation
```json
{
  "workflow_name": "deal_stage_progression",
  "trigger": "opportunity_activity_update",
  "steps": [
    {
      "tool": "mcp_salesforce_get_opportunity_details",
      "output": "deal_data"
    },
    {
      "tool": "mcp_gong_analyze_recent_calls",
      "input": "deal_data.opportunity_id",
      "output": "call_insights"
    },
    {
      "condition": "call_insights.next_steps_defined == true",
      "tool": "mcp_salesforce_update_stage",
      "parameters": {"stage": "Discovery Complete"}
    },
    {
      "tool": "mcp_email_send_follow_up",
      "template": "post_discovery_follow_up",
      "personalization": "call_insights.key_points"
    }
  ]
}
```

## Performance Monitoring

### MCP Tool Performance Metrics
```json
{
  "tool_performance": {
    "mcp_clearbit": {
      "enrichment_rate": "94%",
      "response_time": "< 3 seconds",
      "data_accuracy": "96%"
    },
    "mcp_salesforce": {
      "sync_success_rate": "99.9%",
      "real_time_updates": "< 2 seconds", 
      "data_consistency": "99.8%"
    },
    "mcp_outreach": {
      "email_delivery_rate": "99.5%",
      "open_rate": "42%",
      "response_rate": "12%"
    }
  }
}
```

### Sales Impact Metrics  
- **Lead Response Time**: < 10 minutes from form submission to initial outreach
- **Qualification Accuracy**: 92% of agent-qualified leads accepted by sales reps
- **Conversion Improvement**: 35% increase in lead-to-opportunity conversion
- **Rep Productivity**: 60% more time spent on selling vs. administrative tasks

## Setup Instructions

### 1. MCP Server Configuration
```json
{
  "mcp_servers": {
    "salesforce": {
      "command": "mcp-salesforce",
      "args": ["--sandbox-mode", "false"],
      "env": {
        "SALESFORCE_USERNAME": "$SF_USERNAME",
        "SALESFORCE_PASSWORD": "$SF_PASSWORD",
        "SALESFORCE_SECURITY_TOKEN": "$SF_TOKEN"
      }
    },
    "clearbit": {
      "command": "mcp-clearbit",
      "env": {
        "CLEARBIT_API_KEY": "$CLEARBIT_KEY"
      }
    },
    "outreach": {
      "command": "mcp-outreach",
      "env": {
        "OUTREACH_CLIENT_ID": "$OUTREACH_ID",
        "OUTREACH_CLIENT_SECRET": "$OUTREACH_SECRET"
      }
    }
  }
}
```

### 2. Sales Methodology Integration
```bash
# Load sales contexts and templates
mcp-agent load-contexts ./contexts/sales/
mcp-agent load-contexts ./contexts/customers/ 
mcp-agent load-contexts ./contexts/competitors/
mcp-agent load-templates ./templates/sales/

# Configure ICP scoring model
mcp-agent configure-icp-model ./configs/icp-scoring-criteria.json
```

### 3. Workflow Deployment
```bash
# Deploy sales automation workflows
mcp-agent deploy-workflow lead-qualification.json
mcp-agent deploy-workflow deal-progression.json
mcp-agent deploy-workflow competitive-alerts.json

# Enable sales dashboard
mcp-agent enable-dashboard --url=/sales-automation
```

## Advanced MCP Integrations

### Multi-Tool Competitive Intelligence
```json
{
  "workflow_name": "competitive_deal_intelligence",
  "trigger": "competitor_mentioned_in_opportunity",
  "steps": [
    {
      "tool": "mcp_gong_extract_competitor_mentions",
      "input": "opportunity_id",
      "output": "competitor_intel"
    },
    {
      "tool": "mcp_klenty_competitive_battle_card",
      "input": "competitor_intel.competitor_name",
      "output": "battle_card"
    },
    {
      "tool": "mcp_email_send_competitive_follow_up",
      "input": ["battle_card", "competitor_intel"],
      "template": "competitive_differentiation.md"
    },
    {
      "tool": "mcp_salesforce_update_competitor_field",
      "input": "competitor_intel.competitor_name"
    }
  ]
}
```

### ROI Calculator Integration
```json
{
  "workflow_name": "automated_roi_calculation",
  "trigger": "discovery_call_completed",
  "steps": [
    {
      "tool": "mcp_gong_extract_pain_points",
      "input": "call_recording_id",
      "output": "discovered_pain_points"
    },
    {
      "tool": "mcp_custom_roi_calculator",
      "input": ["discovered_pain_points", "company_size", "industry"],
      "template": "roi_calculation.md",
      "output": "roi_analysis"
    },
    {
      "tool": "mcp_email_send_roi_follow_up",
      "input": "roi_analysis",
      "template": "roi_presentation_follow_up.md"
    },
    {
      "tool": "mcp_calendly_schedule_next_meeting",
      "input": "roi_analysis.next_steps"
    }
  ]
}
```

This MCP-based implementation shows how to build sophisticated sales automation using standardized tool protocols while maintaining the contextual awareness and personalization that drives successful sales outcomes. 