# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository defines a comprehensive database schema for storing and managing AI outputs, prompts, and related metadata in N8N workflows. The data model is structured as CSV files representing database tables, organized into four main categories:

- **core-tables/**: Primary data storage (prompts, outputs, conversations, binary files)
- **system-tables/**: AI infrastructure management (assistants, agents, workflows, users, sessions)
- **tracking-tables/**: Lifecycle management and analytics (quality, revisions, usage, feedback loops)
- **security-tables/**: Compliance and privacy (PII detection, information sensitivity, sharing policies)
- **lookup-tables/**: Reference data (LLM models, STT models, API parameters, retention policies)

## Architecture Domains

The data model is organized into three interconnected domains:

### 1. OUTPUTS Domain
Manages AI-generated content lifecycle:
- Primary: `outputs`, `output_tracking`, `quality_assessments`, `binary_file_data`
- Lifecycle: `output_lifecycle`, `output_revisions`, `output_usage_analytics`
- Knowledge: `output_knowledge_extraction`, `output_semantic_relationships`, `output_value_assessment`
- Security: `pii_detection`, `information_sensitivity`, `retention_policies`

### 2. INFERENCE Domain
Manages AI infrastructure and execution:
- Core: `ai_assistants`, `ai_agents`, `system_prompts`
- Models: `llm_models`, `speech_to_text_models`
- Execution: `n8n_workflows`, `api_usage`, `mcp_usage`
- Configuration: `api_parameters`, `ui_interfaces`

### 3. USERS Domain
Manages user interactions and sessions:
- Core: `users`, `sessions`, `conversations`, `prompts`
- Tracking: `prompt_tracking`
- Auth: `credentials`

## Key Data Flow

The primary data flow through the system:
1. User creates Session → Conversation → Prompt
2. Prompt processed by AI Assistant using LLM Model
3. AI Assistant generates Output
4. Output undergoes Quality Assessment and Tracking
5. Improvement Feedback Loop feeds back to AI Agents/Assistants

## CSV File Structure

All tables follow a consistent CSV format:
- **Headers**: First row contains column names (snake_case)
- **Data Types**: Implicit from content (strings, integers, floats, booleans, timestamps)
- **Timestamps**: UTC ISO 8601 format (e.g., `2025-08-09T11:09:33Z`)
- **Booleans**: `true`/`false` (lowercase)
- **JSON Fields**: Stringified JSON for flexible configuration storage
- **IDs**: String-based identifiers with prefixes (e.g., `conv_001`, `user_123`, `agent_cascade`)

## Critical Relationships

When modifying tables, maintain these key foreign key relationships:

### Core Data Flow
- `prompts.conversation_id` → `conversations.id`
- `prompts.user_id` → `users.id`
- `prompts.session_id` → `sessions.id`
- `outputs.prompt_id` → `prompts.id`
- `outputs.assistant_id` → `ai_assistants.id`
- `outputs.conversation_id` → `conversations.id`

### Quality & Tracking
- `quality_assessments.output_id` → `outputs.id`
- `output_tracking.output_id` → `outputs.id`
- `prompt_tracking.prompt_id` → `prompts.id`
- `qa_validation_taxonomy.id` → `quality_assessments.criteria_id`

### Security & Compliance
- `pii_detection.prompt_id` → `prompts.id`
- `pii_detection.output_id` → `outputs.id`
- `information_sensitivity.id` → `data_retention_policies.sensitivity_level_id`

### Infrastructure
- `ai_assistants.model_id` → `llm_models.id`
- `ai_agents.n8n_workflow_id` → `n8n_workflows.id`
- `api_usage.assistant_id` → `ai_assistants.id`
- `api_usage.prompt_id` → `prompts.id`
- `api_usage.output_id` → `outputs.id`

### Feedback Loops
- `improvement_feedback_loop.output_id` → `outputs.id`
- `improvement_feedback_loop.agent_id` → `ai_agents.id`
- `agent_performance_metrics.agent_id` → `ai_agents.id`

## Working with CSV Files

### Adding New Rows
When adding sample data:
1. Maintain consistent ID prefixes (`conv_`, `user_`, `agent_`, `sess_`, etc.)
2. Use UTC timestamps in ISO 8601 format
3. Ensure foreign key references exist in related tables
4. Include `created_at` and `updated_at` timestamps
5. Use realistic but anonymized data (especially for user information)

### Adding New Columns
When extending the schema:
1. Add the new column to the CSV header row
2. Populate existing rows with default/null values
3. Update the documentation in `README.md` and `docs/data-model-overview.md`
4. Consider impact on relationships with other tables
5. Update Mermaid diagrams in `README.md` if adding new relationships

### Adding New Tables
When creating new tables:
1. Choose the appropriate directory (core-tables, system-tables, tracking-tables, security-tables, lookup-tables)
2. Follow the naming convention (snake_case, plural nouns)
3. Include standard fields: `id`, `created_at`, `updated_at`
4. Add the table to `README.md` navigation index with description
5. Update the appropriate Mermaid diagram in `README.md`
6. Document in `docs/data-model-overview.md`

## Validation Checklist

When making changes, verify:
- [ ] All foreign key references are valid
- [ ] Timestamps are in UTC ISO 8601 format
- [ ] Boolean values use lowercase `true`/`false`
- [ ] No trailing commas in CSV rows
- [ ] Headers match the number of columns in data rows
- [ ] New tables are documented in README.md
- [ ] Mermaid diagrams reflect new relationships
- [ ] ID prefixes are consistent with table names

## N8N Integration Context

This data model is designed for N8N workflow integration:
- **Webhook endpoints** defined in `n8n_workflows.webhook_url`
- **Agent configuration** stored in `ai_agents.configuration_json`
- **Workflow triggers** for prompt processing, QA validation, retention management
- **Cost tracking** via `api_usage` table

When adding features, consider how they integrate with N8N workflow automation patterns.

## Documentation

- **README.md**: Primary documentation with full table navigation and Mermaid diagrams
- **docs/data-model-overview.md**: Technical implementation notes and relationship details
- Tables are linked to both GitHub-rendered CSV views and raw CSV URLs for programmatic access

## Important Conventions

- **Scoring**: Quality metrics use 0-10 scale
- **Sensitivity Levels**: 4-tier classification (Public, Internal, Confidential, Restricted)
- **Priority Levels**: normal, low, high, urgent
- **Status Fields**: Use consistent values (pending, in_progress, completed, failed, archived)
- **JSON Configuration**: Use for flexible, schema-less configuration storage
- **Encryption**: Binary files and credentials should be marked with `is_encrypted` flags
