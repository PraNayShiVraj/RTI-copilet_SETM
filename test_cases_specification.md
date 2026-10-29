# 🧪 Comprehensive Test Cases Specification
**Project:** RTI Copilot  
**Objective:** Ensure agent accuracy, legal compliance, and system constraints.

### 🗣️ 1. Input & Processing Test Cases
| ID | Feature | Scenario | Expected Result | Status |
|:---|:---|:---|:---|:---:|
| **TC-01** | Multilingual Voice | User speaks Marathi grievance. | Translated to English via IndicTrans2; facts extracted. | ⚪ |
| **TC-02** | Intake Guardrail | User says "tell me about my village" (vague). | Agent asks clarifying questions up to the capped limit. | ⚪ |
| **TC-03** | Translation Loop | User submits text in Hindi. | Translated to English for processing, then back to Hindi. | ⚪ |

### ⚖️ 2. Legal & AI Agent Test Cases
| ID | Feature | Scenario | Expected Result | Status |
|:---|:---|:---|:---|:---:|
| **TC-04** | Draft Schema | Agent drafts the application. | Output perfectly matches the required Pydantic JSON schema. | ⚪ |
| **TC-05** | Critic Agent | Draft asks a "why" (opinion) question. | Critic flags it as a rejection risk; triggers revision loop. | ⚪ |
| **TC-06** | Loop Bound | Critic repeatedly flags unfixable issues. | Loop terminates at exactly 2 cycles to ensure latency limits. | ⚪ |
| **TC-07** | RAG Verification | Draft cites "Section 8(1)(j)". | Citation Verifier confirms against `bge-m3` retrieved texts. | ⚪ |
| **TC-08** | Hallucination Check| LLM invents "Section 99" in the draft. | Verifier fails the claim and removes it (Cite or Refuse rule). | ⚪ |
| **TC-09** | Authority Match | User selects "Maharashtra". | System retrieves correct Marathi fee & filing mode from JSON. | ⚪ |

### ⏰ 3. Tracking & Lifecycle Test Cases
| ID | Feature | Scenario | Expected Result | Status |
|:---|:---|:---|:---|:---:|
| **TC-10** | Deadline Engine | RTI marked as filed on 2024-01-01. | APScheduler computes exact 30-day reply/appeal windows. | ⚪ |
| **TC-11** | Missing Reply | 30-day deadline passes without reply. | Appeal Agent automatically drafts "non-reply" first appeal. | ⚪ |
| **TC-12** | OCR Extractor | User uploads skewed photo of PIO reply. | Tesseract extracts text; UI allows manual user correction. | ⚪ |

### 🔒 4. Privacy & Deployment Test Cases
| ID | Feature | Scenario | Expected Result | Status |
|:---|:---|:---|:---|:---:|
| **TC-13** | Offline Privacy | Processing corruption grievance. | No external API calls made; handled by local Qwen LLM. | ⚪ |
| **TC-14** | Deployment | User runs `docker compose up`. | FastAPI, Qdrant, UI, and Models start without manual config. | ⚪ |