# Contexts Directory

This directory contains the foundational knowledge about your business that AI needs to generate relevant, accurate, and on-brand content. Think of this as your business's "memory" that AI can access to understand your company's unique situation, processes, and goals.

## Directory Structure

```
contexts/
├── departments/        # Department-specific context and knowledge
├── company/           # Overall company information and culture
├── processes/         # Business processes and workflows
├── industry/          # Industry-specific knowledge and compliance
├── products/          # Product and service information
├── customers/         # Customer segments and personas
├── competitors/       # Competitive landscape and positioning
└── metrics/           # Key performance indicators and goals
```

## What is Business Context?

Business context is the **environmental knowledge** that helps AI understand:

- **Who you are** as a company (mission, values, culture)
- **What you do** (products, services, business model)
- **How you operate** (processes, workflows, methodologies)
- **Who you serve** (customers, markets, personas)
- **Where you compete** (industry landscape, competitors)
- **What matters** (metrics, goals, priorities)

## Context vs Templates

| **Context Files** | **Template Files** |
|------------------|-------------------|
| Provide background knowledge | Define output formats |
| Describe "what is" | Structure "what to create" |
| Give AI understanding | Give AI instructions |
| Updated when business changes | Updated when communication needs change |

## How AI Uses Context

When you ask AI to create content, it will:

1. **Read relevant context files** to understand your business situation
2. **Apply appropriate templates** for the type of content needed
3. **Blend context + templates** to create personalized, accurate outputs
4. **Maintain consistency** across all communications

## Context File Structure

Each context file should follow this pattern:

```markdown
# [Context Area Name]

## Overview
Brief description of this business area and its role.

## Key Information
- Important facts AI should know
- Current status and priorities
- Recent changes or updates

## Relationships
How this area connects to other parts of the business.

## AI Guidance
Specific instructions for how AI should use this information.

## Last Updated
Date and notes about recent changes.
```

## Maintaining Context

Keep your context files:
- **Current**: Update when business situations change
- **Accurate**: Ensure information reflects reality
- **Specific**: Include details that make AI outputs more relevant
- **Organized**: Use consistent structure for easy AI comprehension

## Security Considerations

Context files may contain:
- Internal business information
- Strategic plans and priorities
- Financial data
- Customer information

**Best Practices:**
- Use `.gitignore` for sensitive context files
- Create sanitized versions for sharing
- Regular review access permissions
- Consider using environment variables for sensitive data 