# AI Output Storage Backend - Data Models

A comprehensive data structure for storing and managing AI outputs, prompts, and related metadata in N8N workflows.

## 🏗️ Architecture Overview

The data model is organized into three primary domains:

### 1. **OUTPUTS Domain** 📤
Tables related to AI-generated content and their lifecycle management.

### 2. **INFERENCE Domain** 🤖  
Tables managing AI agents, assistants, models, and inference infrastructure.

### 3. **USERS Domain** 👥
Tables handling user interactions, prompts, sessions, and authentication.

---

## 📊 Data Model Diagrams

### **OUTPUTS Domain** - Comprehensive Output Lifecycle Management
```mermaid
graph TD
    O[outputs] --> OL[output_lifecycle]
    O --> OR[output_revisions]
    O --> OUA[output_usage_analytics]
    O --> OKE[output_knowledge_extraction]
    O --> OSR[output_semantic_relationships]
    O --> OVA[output_value_assessment]
    O --> OC[output_collections]
    
    O --> OT[output_tracking]
    O --> QA[quality_assessments]
    O --> BF[binary_file_data]
    O --> PII[pii_detection]
    
    QA --> QAT[qa_validation_taxonomy]
    O --> IS[information_sensitivity]
    IS --> ISP[information_sharing_policy]
    
    O --> RP[retention_policies]
    RP --> DRP[data_retention_policies]
    
    IFL[improvement_feedback_loop] --> O
    IFL --> AG[ai_agents]
    
    style O fill:#e1f5fe
    style OL fill:#e8f5e8
    style OR fill:#e8f5e8
    style OUA fill:#e8f5e8
    style QA fill:#f3e5f5
    style IS fill:#fff3e0
```

### **INFERENCE Domain**
```mermaid
graph TD
    AA[ai_assistants] --> SP[system_prompts]
    AA --> LLM[llm_models]
    AA --> STT[speech_to_text_models]
    
    AG[ai_agents] --> NW[n8n_workflows]
    
    API[api_usage] --> AP[api_parameters]
    API --> UI[ui_interfaces]
    
    MCP[mcp_usage]
    
    AA --> API
    AG --> API
    
    style AA fill:#e8f5e8
    style AG fill:#e8f5e8
    style LLM fill:#fff8e1
    style API fill:#fce4ec
```

### **USERS Domain**
```mermaid
graph TD
    U[users] --> S[sessions]
    S --> C[conversations]
    C --> P[prompts]
    P --> PT[prompt_tracking]
    
    U --> CR[credentials]
    P --> BF[binary_file_data]
    P --> PII[pii_detection]
    
    style U fill:#e3f2fd
    style S fill:#e3f2fd
    style C fill:#e3f2fd
    style P fill:#e1f5fe
```

### **Cross-Domain Relationships**
```mermaid
graph LR
    subgraph USERS
        U[users]
        P[prompts]
        S[sessions]
    end
    
    subgraph INFERENCE
        AA[ai_assistants]
        LLM[llm_models]
        API[api_usage]
    end
    
    subgraph OUTPUTS
        O[outputs]
        QA[quality_assessments]
        IS[information_sensitivity]
    end
    
    P --> O
    P --> API
    AA --> O
    LLM --> API
    O --> QA
    O --> IS
    
    style USERS fill:#e3f2fd,stroke:#1976d2
    style INFERENCE fill:#e8f5e8,stroke:#388e3c
    style OUTPUTS fill:#fff3e0,stroke:#f57c00
```

---

## 📑 Navigation Index

### **Core Tables** - Primary Data Storage
| Table | Description | View | Raw CSV |
|-------|-------------|------|---------|
| **Prompts** | User prompts with delivery methods & feedback | [📄](core-tables/prompts.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/core-tables/prompts.csv) |
| **Outputs** | AI responses with quality metrics & revisions | [📄](core-tables/outputs.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/core-tables/outputs.csv) |
| **Conversations** | Session grouping for prompts & outputs | [📄](core-tables/conversations.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/core-tables/conversations.csv) |
| **Binary File Data** | File storage with encryption & metadata | [📄](core-tables/binary_file_data.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/core-tables/binary_file_data.csv) |

### **System Tables** - AI Infrastructure Management
| Table | Description | View | Raw CSV |
|-------|-------------|------|---------|
| **AI Assistants** | Assistant definitions with performance metrics | [📄](system-tables/ai_assistants.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/system-tables/ai_assistants.csv) |
| **System Prompts** | System prompt versioning & management | [📄](system-tables/system_prompts.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/system-tables/system_prompts.csv) |
| **AI Agents** | N8N workflow agents with feedback tracking | [📄](system-tables/ai_agents.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/system-tables/ai_agents.csv) |
| **N8N Workflows** | Workflow execution & performance tracking | [📄](system-tables/n8n_workflows.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/system-tables/n8n_workflows.csv) |
| **Users** | User profiles & subscription management | [📄](system-tables/users.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/system-tables/users.csv) |
| **Sessions** | User interaction session tracking | [📄](system-tables/sessions.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/system-tables/sessions.csv) |
| **Credentials** | API credential management | [📄](system-tables/credentials.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/system-tables/credentials.csv) |

### **Tracking Tables** - Comprehensive Lifecycle Management
| Table | Description | View | Raw CSV |
|-------|-------------|------|---------|
| **Output Lifecycle** | Stage-by-stage output progression | [📄](tracking-tables/output_lifecycle.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_lifecycle.csv) |
| **Output Revisions** | Version control & improvement history | [📄](tracking-tables/output_revisions.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_revisions.csv) |
| **Output Usage Analytics** | Real-world usage & effectiveness tracking | [📄](tracking-tables/output_usage_analytics.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_usage_analytics.csv) |
| **Output Knowledge Extraction** | Insights & actionable items extraction | [📄](tracking-tables/output_knowledge_extraction.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_knowledge_extraction.csv) |
| **Output Semantic Relationships** | Inter-output connection mapping | [📄](tracking-tables/output_semantic_relationships.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_semantic_relationships.csv) |
| **Output Value Assessment** | Business & educational value scoring | [📄](tracking-tables/output_value_assessment.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_value_assessment.csv) |
| **Output Collections** | Curated high-value output collections | [📄](tracking-tables/output_collections.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_collections.csv) |
| **Agent Performance Metrics** | Daily agent performance tracking | [📄](tracking-tables/agent_performance_metrics.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/agent_performance_metrics.csv) |
| **Improvement Feedback Loop** | Systematic improvement tracking | [📄](tracking-tables/improvement_feedback_loop.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/improvement_feedback_loop.csv) |
| **Output Tracking** | Task management for outputs | [📄](tracking-tables/output_tracking.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/output_tracking.csv) |
| **Prompt Tracking** | Task management for prompts | [📄](tracking-tables/prompt_tracking.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/prompt_tracking.csv) |
| **Quality Assessments** | Output quality evaluation | [📄](tracking-tables/quality_assessments.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/tracking-tables/quality_assessments.csv) |

### **Lookup Tables** - Reference Data & Configuration
| Table | Description | View | Raw CSV |
|-------|-------------|------|---------|
| **LLM Models** | Model definitions with costs & capabilities | [📄](lookup-tables/llm_models.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/llm_models.csv) |
| **Speech-to-Text Models** | STT models with accuracy ratings | [📄](lookup-tables/speech_to_text_models.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/speech_to_text_models.csv) |
| **UI Interfaces** | Interface definitions & capabilities | [📄](lookup-tables/ui_interfaces.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/ui_interfaces.csv) |
| **API Parameters** | API parameter specifications | [📄](lookup-tables/api_parameters.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/api_parameters.csv) |
| **QA Validation Taxonomy** | Quality assessment criteria & weights | [📄](lookup-tables/qa_validation_taxonomy.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/qa_validation_taxonomy.csv) |
| **Data Retention Policies** | Enhanced retention rules & conditions | [📄](lookup-tables/data_retention_policies.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/data_retention_policies.csv) |
| **API Usage** | API call tracking & cost monitoring | [📄](lookup-tables/api_usage.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/api_usage.csv) |
| **MCP Usage** | Model Context Protocol tool usage | [📄](lookup-tables/mcp_usage.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/mcp_usage.csv) |
| **Retention Policies** | Basic retention policy definitions | [📄](lookup-tables/retention_policies.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/lookup-tables/retention_policies.csv) |

### **Security Tables** - Compliance & Privacy Management
| Table | Description | View | Raw CSV |
|-------|-------------|------|---------|
| **PII Detection** | Personal information tracking & masking | [📄](security-tables/pii_detection.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/security-tables/pii_detection.csv) |
| **Information Sensitivity** | 4-tier sensitivity classification | [📄](security-tables/information_sensitivity.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/security-tables/information_sensitivity.csv) |
| **Information Sharing Policy** | Sharing rules by sensitivity level | [📄](security-tables/information_sharing_policy.csv) | [📊](https://raw.githubusercontent.com/danielrosehill/AI-Output-Storage-Backend-Data-Models/main/security-tables/information_sharing_policy.csv) |

### **Documentation**
| Document | Description | View |
|----------|-------------|------|
| **Data Model Overview** | Comprehensive technical documentation | [📖](docs/data-model-overview.md) |

---

## 📁 Directory Structure

```
├── core-tables/           # Primary data storage
│   ├── prompts.csv
│   ├── outputs.csv
│   ├── conversations.csv
│   └── binary_file_data.csv
├── system-tables/         # AI system management
│   ├── ai_assistants.csv
│   ├── system_prompts.csv
│   ├── ai_agents.csv
│   ├── n8n_workflows.csv
│   ├── users.csv
│   ├── sessions.csv
│   └── credentials.csv
├── tracking-tables/       # Comprehensive output lifecycle & improvement
│   ├── output_tracking.csv
│   ├── prompt_tracking.csv
│   ├── quality_assessments.csv
│   ├── output_lifecycle.csv
│   ├── output_revisions.csv
│   ├── output_usage_analytics.csv
│   ├── output_knowledge_extraction.csv
│   ├── output_semantic_relationships.csv
│   ├── output_value_assessment.csv
│   ├── output_collections.csv
│   ├── agent_performance_metrics.csv
│   └── improvement_feedback_loop.csv
├── lookup-tables/         # Reference data
│   ├── llm_models.csv
│   ├── speech_to_text_models.csv
│   ├── ui_interfaces.csv
│   ├── api_parameters.csv
│   ├── qa_validation_taxonomy.csv
│   ├── retention_policies.csv
│   ├── data_retention_policies.csv
│   ├── api_usage.csv
│   └── mcp_usage.csv
├── security-tables/       # Security & compliance
│   ├── pii_detection.csv
│   ├── information_sensitivity.csv
│   └── information_sharing_policy.csv
└── docs/                  # Documentation
    └── data-model-overview.md
```

---

## 🔗 Key Relationships

### **Primary Data Flow**
1. **User** creates **Session** → **Conversation** → **Prompt**
2. **Prompt** processed by **AI Assistant** using **LLM Model**
3. **AI Assistant** generates **Output** 
4. **Output** undergoes **Quality Assessment** and **Tracking**

### **Relational Fields**

#### **Core Relationships**
- `prompts.conversation_id` → `conversations.id`
- `outputs.prompt_id` → `prompts.id`
- `outputs.assistant_id` → `ai_assistants.id`

#### **Security & Compliance**
- `pii_detection.prompt_id` → `prompts.id`
- `pii_detection.output_id` → `outputs.id`
- `information_sensitivity.id` → `data_retention_policies.sensitivity_level_id`

#### **Quality Management**
- `quality_assessments.output_id` → `outputs.id`
- `qa_validation_taxonomy.id` → `quality_assessments.criteria_id`

#### **Usage Tracking**
- `api_usage.prompt_id` → `prompts.id`
- `api_usage.output_id` → `outputs.id`
- `api_usage.assistant_id` → `ai_assistants.id`

---

## 🚀 N8N Integration Points

### **Webhook Endpoints**
- **Input Processing**: `POST /webhook/ai-prompt`
- **Output Storage**: `POST /webhook/ai-output`
- **Quality Review**: `POST /webhook/qa-review`

### **Workflow Triggers**
1. **Prompt Processing**: New prompt → AI inference → Output storage
2. **Quality Assessment**: New output → QA validation → Tracking update
3. **Retention Management**: Scheduled → Policy evaluation → Archive/Delete

### **Data Enrichment**
- **PII Detection**: Automated scanning on prompt/output creation
- **Sensitivity Classification**: Rule-based classification
- **Usage Tracking**: Real-time API call logging

---

## 📋 Implementation Notes

### **Data Types & Formats**
- **Timestamps**: UTC ISO 8601 format
- **JSON Fields**: Flexible configuration storage
- **Boolean Fields**: Multi-modal delivery tracking
- **Scores**: 0-10 scale for quality metrics

### **Security Features**
- **Encryption**: Binary files and sensitive data
- **PII Masking**: Automatic detection and masking
- **Access Control**: Role-based data access
- **Audit Trails**: Complete change tracking

### **Performance Considerations**
- **Indexing**: Primary keys, foreign keys, timestamps
- **Partitioning**: Large tables by date/user
- **Archival**: Automated based on retention policies
- **Cleanup**: Scheduled deletion of expired data

---

## 🔧 Getting Started

1. **Import CSV files** into your N8N database
2. **Configure workflows** using the provided webhook endpoints
3. **Set up retention policies** based on your requirements
4. **Enable PII detection** for compliance
5. **Configure quality assessment** workflows

For detailed implementation guidance, see [`docs/data-model-overview.md`](docs/data-model-overview.md).

---

## 📈 Monitoring & Analytics

The data model supports comprehensive analytics:
- **Usage Patterns**: API calls, model performance, user behavior
- **Quality Metrics**: Output quality trends, assessment scores
- **Cost Tracking**: Token usage, API costs per user/model
- **Compliance**: PII detection rates, retention policy adherence
