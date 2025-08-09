# AI Output Storage Backend - Data Model Overview

## Core Tables

### 1. **prompts.csv** - User Input Storage
Stores all user prompts with delivery method tracking and metadata.
- **Key Fields**: `conversation_id`, `username`, `prompt_text`, `delivery_*` booleans
- **Relationships**: Links to `outputs`, `conversations`, `users`, `sessions`

### 2. **outputs.csv** - AI Response Storage  
Stores AI-generated responses in multiple formats with quality metrics.
- **Key Fields**: `output_text`, `output_html`, `output_markdown`, `output_structured`
- **Relationships**: Links to `prompts`, `conversations`, `ai_assistants`

### 3. **conversations.csv** - Session Grouping
Groups related prompts and outputs into logical conversations.
- **Key Fields**: `conversation_name`, `total_prompts`, `total_outputs`
- **Relationships**: Parent to `prompts` and `outputs`

## AI System Tables

### 4. **ai_assistants.csv** - Assistant Definitions
Defines available AI assistants and their capabilities.
- **Key Fields**: `name`, `provider`, `model_name`, `capabilities`
- **Relationships**: Referenced by `outputs`, `api_usage`

### 5. **system_prompts.csv** - System Prompt Management
Manages system prompts used by assistants.
- **Key Fields**: `prompt_text`, `version`, `assistant_id`
- **Relationships**: Links to `ai_assistants`

### 6. **ai_agents.csv** - N8N Agent Definitions
Defines N8N workflow-based agents.
- **Key Fields**: `n8n_workflow_id`, `capabilities`, `configuration_json`
- **Relationships**: Links to `n8n_workflows`

### 7. **n8n_workflows.csv** - Workflow Management
Tracks N8N workflows used in the system.
- **Key Fields**: `workflow_id`, `trigger_type`, `execution_count`
- **Relationships**: Referenced by `ai_agents`

## User & Session Management

### 8. **users.csv** - User Profiles
Stores user information and preferences.
- **Key Fields**: `username`, `timezone`, `subscription_tier`
- **Relationships**: Referenced by most other tables

### 9. **sessions.csv** - User Sessions
Tracks user interaction sessions.
- **Key Fields**: `session_token`, `start_time`, `total_prompts`
- **Relationships**: Links to `users`, referenced by `prompts`

### 10. **credentials.csv** - API Credential Management
Manages API keys and credentials (encrypted).
- **Key Fields**: `provider`, `credential_type`, `expires_at`
- **Relationships**: Used by system for API calls

## Usage Tracking

### 11. **api_usage.csv** - API Call Tracking
Tracks all API calls with cost and performance metrics.
- **Key Fields**: `tokens_input`, `tokens_output`, `cost_usd`, `response_time_ms`
- **Relationships**: Links to `prompts`, `outputs`, `users`

### 12. **mcp_usage.csv** - MCP Tool Usage
Tracks Model Context Protocol tool usage.
- **Key Fields**: `server_name`, `tool_name`, `success`, `tokens_used`
- **Relationships**: Links to `prompts`, `outputs`

## Quality & Task Management

### 13. **quality_assessments.csv** - Output Quality Tracking
Stores quality assessments for outputs.
- **Key Fields**: `accuracy_score`, `relevance_score`, `overall_score`
- **Relationships**: Links to `outputs`, `prompts`

### 14. **output_tracking.csv** - Output Task Management
Tracks follow-up tasks for outputs (reviews, improvements).
- **Key Fields**: `tracking_type`, `status`, `assigned_to`, `due_date`
- **Relationships**: Links to `outputs`

### 15. **prompt_tracking.csv** - Prompt Task Management
Tracks follow-up tasks for prompts (optimization, analysis).
- **Key Fields**: `tracking_type`, `status`, `priority_level`
- **Relationships**: Links to `prompts`

### 16. **retention_policies.csv** - Data Retention Rules
Defines data retention and archival policies.
- **Key Fields**: `retention_days`, `archive_after_days`, `delete_after_days`
- **Relationships**: Applied to all data tables

## Key Relationships

```
users → sessions → conversations → prompts → outputs
                                  ↓         ↓
                            prompt_tracking  output_tracking
                                            ↓
                                    quality_assessments

ai_assistants → system_prompts
ai_agents → n8n_workflows

api_usage ← prompts/outputs
mcp_usage ← prompts/outputs
```

## Implementation Notes

- All timestamps use UTC format
- Boolean fields for delivery methods enable multi-modal tracking
- JSON fields store flexible configuration data
- Quality scores use 0-10 scale
- Retention policies support conditional logic via JSON
- All tables include `created_at` and `updated_at` for audit trails

## N8N Integration Points

1. **Webhook Endpoints**: `n8n_workflows.webhook_url`
2. **Agent Configuration**: `ai_agents.configuration_json`
3. **Execution Tracking**: `n8n_workflows.execution_count`
4. **Cost Monitoring**: `api_usage` table for all API calls
