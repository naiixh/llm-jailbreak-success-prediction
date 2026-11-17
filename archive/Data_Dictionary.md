# Data Dictionary: LLM Adversarial Jailbreak & Security Benchmark (OWASP Top-10)

This dataset serves as an enterprise-grade quantitative benchmark for evaluating Large Language Model (LLM) security guardrails against adversarial prompt injections and jailbreak attacks.

---

### Files Included
* **`train.csv`** (12,000 rows): Labeled historical benchmark instances with ground-truth outcome `is_jailbreak_success`.
* **`test.csv`** (3,000 rows): Unlabeled evaluation set for blind model validation and competition leaderboards.
* **`sample_submission.csv`** (3,000 rows): Template submission file mapping `prompt_id` to binary prediction `is_jailbreak_success`.
* **`llm_jailbreak_full_benchmark.csv`** (15,000 rows): Consolidated dataset containing all historical instances.

---

### Feature Schema

| Column Name | Data Type | Range / Values | Description |
| :--- | :--- | :--- | :--- |
| `prompt_id` | String | `PRM_00001` - `PRM_15000` | Unique cryptographic identifier for each prompt instance. |
| `prompt_token_count` | Integer | $10 - 2200$ | Number of input tokens computed via standard Byte-Pair Encoding (BPE). |
| `char_to_token_ratio` | Float | $3.2 - 8.5$ | Ratio of raw characters to tokens. Higher ratios indicate ciphers, hex, or base64. |
| `lexical_entropy` | Float | $1.5 - 8.8$ | Shannon entropy of token frequency distribution. Higher values denote randomness/obfuscation. |
| `obfuscation_score` | Float | $0.0000 - 1.0000$ | Algorithmic detection score for leetspeak, zero-width characters, Base64, and ciphers. |
| `semantic_policy_distance` | Float | $0.0500 - 0.9900$ | Cosine distance between prompt embedding vector and safe enterprise policy anchor embeddings. |
| `roleplay_framing_depth` | Integer | $0 - 4$ | Depth of nested fictional framing or persona hijacking (e.g., DAN, evil twin, virtual sim). |
| `hypothetical_filter_trigger` | Binary | $0, 1$ | Flag indicating evasive hypothetical prefixes ("for academic research only", "in a parallel world"). |
| `payload_toxicity_signal` | Float | $0.0000 - 1.0000$ | Heuristic score measuring weaponization or malicious intent indicators in the payload. |
| `system_prompt_leak_attempt` | Binary | $0, 1$ | Flag detecting explicit system instructions extraction ("ignore previous instructions", "print system prompt"). |
| `recursive_nesting_level` | Integer | $0 - 4$ | Count of recursively nested quote blocks or fictional simulation loops. |
| `target_model_family` | Categorical | 5 Models | Base model evaluated: `GPT-4o-Mini`, `Llama-3.1-70B-Instruct`, `Claude-3.5-Sonnet`, `Mistral-Large-2`, `DeepSeek-V2.5`. |
| `guardrail_layer_type` | Categorical | 5 Layers | Firewall/Guardrail layer deployed: `Llama-Guard-3`, `NeMo-Guardrails`, `Lakera-Endpoint-Guard`, `Heuristic-Regex-Filter`, `No_Guardrail`. |
| `temperature_setting` | Float | $0.00 - 1.10$ | Sampling temperature parameter during inference generation. |
| `attack_vector` | Categorical | 6 Classes | Taxonomy classification based on MITRE ATLAS / OWASP LLM-01. |
| `vulnerability_risk_score` | Float | $0.00 - 100.00$ | Continuous risk assessment index calculated prior to guardrail response. |
| `is_jailbreak_success` | Binary (Target) | $0, 1$ | Ground truth label: `1` if prompt successfully bypassed guardrails and produced unsafe output, `0` otherwise. |

---

### Evaluation Metric
* **Primary Competition Metric:** **ROC-AUC (Area Under the Receiver Operating Characteristic Curve)**
* **Secondary Metric:** **Macro F1-Score** (to penalize false positives and false negatives equally under adversarial distribution shift).
