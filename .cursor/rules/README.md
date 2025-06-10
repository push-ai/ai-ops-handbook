# Cursor Rules Directory

This directory contains modular **Cursor Rules** that enforce process-driven AI operations across different business units. Each rule file focuses on specific operational contexts to maximize efficiency and minimize token usage.

## Rule Structure by Operational Units

### 🎯 **`general-operations.mdc`** (Always Applied)
- **Scope**: Universal standards across all business functions
- **When Active**: Always loaded for every AI interaction
- **Purpose**: Core quality principles, collaboration standards, and risk management
- **Token Impact**: Minimal - only essential universal guidelines

### 📝 **`content-creation.mdc`** (Context-Aware)
- **Scope**: Blog posts, marketing materials, documentation, external communications
- **When Active**: Working with `/briefs/`, `/templates/marketing/`, content files
- **Purpose**: Multi-step content workflow, research requirements, brand consistency
- **Key Process**: Brief → Research → Strategy → Outline → Create → Review → Approve → Publish

### 🔧 **`issue-resolution.mdc`** (Context-Aware)
- **Scope**: Customer support, bug reports, technical troubleshooting
- **When Active**: Working with `/support/`, `/issues/`, `/troubleshooting/` directories
- **Purpose**: Systematic problem-solving, root cause analysis, documentation
- **Key Process**: Intake → Investigate → Analyze → Solve → Implement → Verify → Document → Follow-up

### 📋 **`ticket-management.mdc`** (Context-Aware)
- **Scope**: Project workflows, task tracking, team coordination, delivery management
- **When Active**: Working with `/projects/`, `/tasks/`, `/tickets/`, `/workflows/` directories
- **Purpose**: Structured project management, sprint planning, quality delivery
- **Key Process**: Create → Plan → Design → Implement → Test → Review → Deploy → Close

## Why This Modular Approach?

### ✅ **Token Efficiency**
- Only relevant rules load based on file context
- Reduces AI context overhead for better performance
- Focuses AI attention on applicable processes

### ✅ **Scalability**
- Easy to add new operational units (e.g., `sales-processes.mdc`, `hr-workflows.mdc`)
- Team-specific rules without affecting other functions
- Maintainable and focused rule sets

### ✅ **Context Relevance**
- Rules activate when working on relevant files/directories
- No confusion from irrelevant process guidelines
- Precise guidance for specific work types

## How Rules Activate

According to [Cursor's documentation](https://docs.cursor.com/context/rules), rules can be triggered by:

- **`alwaysApply: true`**: Rules always included (general-operations.mdc)
- **`globs` patterns**: Rules activate when working with matching file paths
- **Manual reference**: Using `@ruleName` in conversations
- **Agent decision**: AI chooses relevant rules based on task context

## Adding New Operational Units

To create a new operational unit rule:

1. **Identify the operational unit** (e.g., "sales-processes", "hr-workflows")
2. **Define file/directory patterns** that should trigger the rule
3. **Create focused process steps** specific to that business function
4. **Include quality standards** relevant to that type of work
5. **Test activation** by working in relevant directories

### Template for New Rules:
```markdown
---
description: [Operational unit] process rules for [specific activities]
globs: ["**/[relevant-directories]/**"]
alwaysApply: false
---

# [Operational Unit] Process Rules

## Multi-Step [Operation Type] Workflow
1. **Step 1**: Description and requirements
2. **Step 2**: Description and requirements
[...continue with 3-8 steps]

## Quality Standards
- Specific standards for this operational unit

## Emergency Procedures
- Fast-track options for urgent work
```

## Rule Maintenance

### Regular Review
- **Quarterly Assessment**: Evaluate rule effectiveness and usage patterns
- **Team Feedback**: Gather input on process pain points and improvements
- **Usage Analytics**: Monitor which rules are most/least used
- **Process Evolution**: Update rules as business needs change

### Best Practices
- **Keep Focused**: Each rule should cover one operational unit
- **Be Specific**: Provide concrete steps rather than vague guidance
- **Include Examples**: Show what good process execution looks like
- **Balance Automation**: Enforce process without being overly rigid
- **Document Decisions**: Record why specific rules were chosen

## Integration with AI Operations Handbook

These rules work together with the handbook's other components:

- **`/contexts/`**: Provide business knowledge and background information
- **`/templates/`**: Offer starting points for common deliverables  
- **`/briefs/`**: Capture initial requirements for content projects
- **`/examples/`**: Demonstrate successful implementations

The rules ensure that AI operations are **deliberate, reviewable, and consistently high-quality** across all business functions while maintaining efficiency through focused, context-aware activation. 