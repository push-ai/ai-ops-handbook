# MCP Tools Example: Customer Outreach Agent

## Overview
This example shows how AI agents use **Model Context Protocol (MCP)** tools to automate business operations instead of custom Python code.

## MCP Tool Configuration
```json
{
  "mcp_servers": {
    "salesforce": {
      "command": "mcp-salesforce",
      "env": {
        "SALESFORCE_USERNAME": "$SF_USERNAME",
        "SALESFORCE_PASSWORD": "$SF_PASSWORD"
      }
    },
    "email": {
      "command": "mcp-email",
      "env": {
        "SMTP_HOST": "$EMAIL_HOST",
        "SMTP_USER": "$EMAIL_USER"
      }
    }
  }
}
```

## Agent Workflow Using MCP Tools

### 1. Get Customer Data
Instead of Python API calls, use MCP:
```json
{
  "tool": "mcp_salesforce_get_account",
  "parameters": {
    "account_id": "001XX000004C2Y3",
    "include_fields": ["name", "industry", "annual_revenue"]
  }
}
```

### 2. Generate Personalized Content
The agent uses handbook contexts automatically:
```json
{
  "content_generation": {
    "template": "sales/enterprise-outreach.md",
    "context_inputs": [
      "company_voice_guidelines",
      "target_persona_enterprise_buyer",
      "product_value_propositions"
    ],
    "personalization_data": "[salesforce_account_data]"
  }
}
```

### 3. Send Email via MCP
```json
{
  "tool": "mcp_email_send",
  "parameters": {
    "to": "decision.maker@enterprise.com",
    "subject": "Streamlining Operations at [Company Name]",
    "body": "[generated_personalized_content]",
    "tracking": true
  }
}
```

### 4. Log Activity
```json
{
  "tool": "mcp_salesforce_create_task",
  "parameters": {
    "whatId": "001XX000004C2Y3",
    "subject": "Personalized outreach sent",
    "description": "AI agent sent targeted enterprise email"
  }
}
```

## Key Benefits of MCP Approach

✅ **No Custom Code**: Use standardized tools instead of writing API integrations
✅ **Automatic Context**: Agent accesses handbook contexts seamlessly  
✅ **Tool Reliability**: MCP servers handle authentication, error handling, retries
✅ **Easy Scaling**: Add new tools by configuring MCP servers
✅ **Better Monitoring**: Built-in logging and performance tracking

## vs. Traditional Python Approach

**OLD WAY (Python):**
```python
import salesforce_api
import email_service

def send_outreach():
    # 50+ lines of custom API code
    # Manual error handling
    # Custom authentication logic
    # Template loading and processing
    # etc.
```

**NEW WAY (MCP):**
```json
{
  "workflow": [
    {"tool": "mcp_salesforce_get_account"},
    {"tool": "mcp_content_generate"},  
    {"tool": "mcp_email_send"},
    {"tool": "mcp_salesforce_log_activity"}
  ]
}
```

The MCP approach is simpler, more reliable, and leverages the handbook structure automatically. 