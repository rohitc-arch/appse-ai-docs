---
slug: /platform/key-concepts/nodes/ai-processor
title: AI Processor Node
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

The **AI Processor Node** is a built-in node that enables you to process data using AI models such as Google Gemini, OpenAI, and Anthropic Claude.

It allows you to generate, transform, and structure responses using prompts, system instructions, and optional configurations like temperature and structured output format.

This node is commonly used for:
- Content generation
- Data enrichment
- Classification and analysis
- Structured output for downstream workflows

---

## Configuration Overview

The AI Processor Node consists of:

- **Credential Configuration**
- **Prompt & Output Configuration**

---

## Steps to Use AI Processor Node

---

### 1. Select AI Processor Node

Select **AI Processor** from the node selection screen.

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\click-ai_agent-node.png" width="700"/
>
<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\select-ai-processor-node.png" width="700"/
>

---

### 2. Configure Credentials

In this step, select the AI provider, model, and credential type.

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-credential-configuration.png" width="700"/
>
---

#### Configure the following fields:

#### **LLM Provider** *

Select the AI provider:

- Google Gemini  
- OpenAI  
- Anthropic Claude  

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\select-llm-provider.png" width="700"/>

---

#### **Model** *

The available models depend on the selected provider.

<Tabs>

<TabItem value="openai" label="OpenAI">

Select one of the following models:

- GPT-4o  
- GPT-4o-mini  
- GPT-4.1  
- GPT-4.1-mini  

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-llm-openai-model.png" width="700"/>

</TabItem>

<TabItem value="gemini" label="Google Gemini">

Select one of the following models:

- Gemini 2.5 Flash  
- Gemini 2.5 Pro  
- Gemini 3 Flash (Preview)  

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-llm-gemini-model.png" width="700"/>

</TabItem>

<TabItem value="claude" label="Anthropic Claude">

Select one of the following models:

- Claude 4.5 Haiku  
- Claude 4.6 Sonnet  
- Claude 4.6 Opus  

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-llm-claude-model.png" width="700"/>

</TabItem>

</Tabs>

---

#### ℹ️ Credential Usage

The AI Processor Node supports two ways to execute requests based on credential configuration:

- **Bring Your Own Key (BYOK)**  
  Uses your own credential configured for the selected provider (e.g., OpenAI, Gemini, Claude)

- **Platform-Managed Credential**  
  Uses appse ai-managed credentials without requiring user-provided API keys

---

#### How to Select Credential Mode

The mode is controlled using the **BYOK toggle** in the Credential configuration step:

- **BYOK ON** → Uses your own credential  
- **BYOK OFF** → Uses platform-managed credential  

---

### 3. BYOK (Bring Your Own Key)

<Tabs>

<TabItem value="byok-on" label="BYOK ON">

**Turn on the BYOK toggle button**

<img src="/img/platform/key-concepts/nodes/built-in/ai_processor_node/ai-processor-byok-toggle.png" width="700"/>

---

#### **Account** *

- Required only when **BYOK is enabled**
- Provide your own API key through a credential
- Requests are executed using your selected credential

ℹ️ You can select an existing credential or create a new one

---

#### Create a New Credential

ℹ️ Credentials can be created either from the **Credentials page** or directly within the node.

- Use the **Credentials page** to manage and reuse credentials across workflows  
- Use the **Create a new credential** option in the node  

Credentials created from either location will be available in the **Account** dropdown.

---

1. Click on the **Account** dropdown

<img src="/img/platform/key-concepts/nodes/built-in/ai_processor_node/select-byok-credential.png" width="700"/>

2. Click **Create a new credential**

<img src="/img/platform/key-concepts/nodes/built-in/ai_processor_node/click-create-credential.png" width="700"/>

3. Enter the required details:
   - **Connection Name**  
   - **Secret Key (API Key)**  

<img src="/img/platform/key-concepts/nodes/built-in/ai_processor_node/provide-credential.png" width="500"/>

4. Click **Save**

<img src="/img/platform/key-concepts/nodes/built-in/ai_processor_node/click-credential-save-button.png" width="500"/>

---

#### Select Existing Credential

- Choose a credential from the **Account** dropdown  
- The selected credential will be used for execution  

After creating a credential, it will appear in the list for selection.

---

</TabItem>

<TabItem value="byok-off" label="BYOK OFF">

**Keep the BYOK toggle button OFF**

- No API key required  
- Uses **platform-managed credentials**  

<img src="/img/platform/key-concepts/nodes/built-in/ai_processor_node/ai-processor-byok-toggle.png" width="700"/>

</TabItem>

</Tabs>

### 4. Configure AI Prompt

Move to the **Configure** step.

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-configuration-page.png" width="700"/>

---

#### **Message** *

The main prompt sent to the AI model.

**Provide the prompt in the Message field**
- Supports dynamic expressions (e.g., `{{$payload.field}}`)
- Allows structured instructions and contextual data

#### Example:

```text
Analyze the following product and generate insights:

Product Details:
- Name: {{$payload.name}}
- SKU: {{$payload.sku}}
- Price: {{$payload.price}}

Tasks:
1. Rewrite description
2. Generate SEO keywords
3. Suggest category
4. Provide improvements
```
<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\prompt-configuration-field.png" width="700"/>

---

#### ℹ️ **Optional Fields Note**

Click on **Optionals** if Optional fields are required

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\select-optional-fields.png" width="700"/>

The following fields are optional and can be configured based on your use case:

- **System Message**
- **Temperature**
- **Structured Response Format**

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\optional-fields.png" width="700"/>


You may:
- Provide all, some, or none of these fields  
- Skip them entirely for basic prompt execution  

If not provided:
- Default model behavior will be used  
- Output will be unstructured unless a schema is defined  

---

#### **System Message (Optional)**

Defines AI behavior.

#### Example
```text
You are an advanced product intelligence assistant.
- Ensure structured output
- Avoid generic responses
- Focus on SEO optimization
```

#### **Temperature (Optional)**

Controls the randomness and creativity of the AI response.

- `0.0` → Most consistent and deterministic output 
- `1.0` → Noticeably more creative and varied responses 
- `2.0` → Most creative and diverse output  

ℹ️ If not specified, the default value (`0.7`) is used.

--- 

#### **Structured Response Format (Optional)**

Define a JSON schema to enforce structured output.

You can either:
- Manually define your own JSON schema  
- Use predefined templates available in the node for quick reference  

#### Example

```JSON
{
  "type": "object",
  "properties": {
    "itemCode": { "type": "string" },
    "description": { "type": "string" },
    "keywords": {
      "type": "array",
      "items": { "type": "string" }
    }
  }
}
```
⚠️ If schema is invalid, the response may not follow the expected format.

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-optional-field-config.png" width="700"/>

--- 

### 5. Execute the Node

Click **Continue**, then **Run** to execute.

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-continue-button.png" width="700"/>

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-run-button.png" width="700"/>

---

### 6. Output

After execution:

AI response is generated
Structured output is returned (if schema is used)
Output is available for downstream nodes

<div
  style={{
    maxHeight: '350px',
    overflow: 'auto',
    border: '1px solid #ddd',
    padding: '12px',
    borderRadius: '6px'
  }}
>
<pre>
<code>
```JSON
[
  {
    "content": "{\"itemCode\":\"Gucci7890\",\"description\":\"Experience the sophisticated allure of the Gucci Perfume, a signature scent that encapsulates luxury and elegance. With its unique blend of floral and spicy notes, this perfume elevates your everyday style, leaving a lasting impression. Each bottle represents the timeless charm and modern creativity the Gucci brand is renowned for, making it an indispensable addition to your fragrance collection.\",\"keywords\":[\"Gucci Perfume\",\"luxury fragrance\",\"signature scent\",\"elegant perfume\",\"floral perfume\",\"spicy notes\",\"designer fragrance\",\"Gucci eau de parfum\"],\"category\":\"Luxury Fragrances\"}",
    "structured_content": {
      "itemCode": "Gucci7890",
      "description": "Experience the sophisticated allure of the Gucci Perfume, a signature scent that encapsulates luxury and elegance. With its unique blend of floral and spicy notes, this perfume elevates your everyday style, leaving a lasting impression. Each bottle represents the timeless charm and modern creativity the Gucci brand is renowned for, making it an indispensable addition to your fragrance collection.",
      "keywords": [
        "Gucci Perfume",
        "luxury fragrance",
        "signature scent",
        "elegant perfume",
        "floral perfume",
        "spicy notes",
        "designer fragrance",
        "Gucci eau de parfum"
      ],
      "category": "Luxury Fragrances"
    },
    "usage_metadata": {
      "input_tokens": 138,
      "output_tokens": 124,
      "total_tokens": 262
    },
    "response_metadata": {
      "token_usage": {
        "completion_tokens": 124,
        "prompt_tokens": 138,
        "total_tokens": 262,
        "completion_tokens_details": {
          "accepted_prediction_tokens": 0,
          "audio_tokens": 0,
          "reasoning_tokens": 0,
          "rejected_prediction_tokens": 0
        },
        "prompt_tokens_details": {
          "audio_tokens": 0,
          "cached_tokens": 0
        }
      },
      "model_provider": "openai",
      "model_name": "gpt-4o-2024-08-06",
      "system_fingerprint": "fp_fab7bd3a94",
      "id": "chatcmpl-Dc4gW4PzDTiNalY3LxKyli3ziE83V",
      "service_tier": "default",
      "finish_reason": "stop",
      "logprobs": null
    },
    "credits_consumed": "0.422667"
  }
]
```
</code>
</pre>
</div>

<img src="\img\platform\key-concepts\nodes\built-in\ai_processor_node\ai-processor-output.png" width="700"/>

---

**Key Features**
- Multi-provider AI support
- BYOK and appse ai-managed credentials
- Dynamic expressions in prompts
- System-level AI behavior control
- Structured JSON output support
- Seamless workflow integration

---

**Notes**
- Use System Message to guide AI behavior
- Use JSON Schema for structured outputs
- Ensure valid credentials when BYOK is ON

---