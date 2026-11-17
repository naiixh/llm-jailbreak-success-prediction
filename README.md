# Predicció de l'èxit de jailbreaks contra guardrails de LLM
 
Projecte del Cas Kaggle d'Aprenentatge Computacional (UAB, 2026-27).
 
## Pregunta
 
Donat un prompt advers caracteritzat per mètriques de telemetria (entropia lèxica, ofuscació, profunditat de roleplay, etc.), el model atacat i el guardrail que el protegeix, aconseguirà l'atac saltar-se el guardrail i produir una sortida insegura?
 
És un problema de classificació binària. A més de predir, es vol analitzar en quins casos fallen els guardrails (per tipus d'atac, per guardrail i per model).
 
## Base de dades
 
- **Nom:** LLM Adversarial Jailbreak & Security Benchmark
- **Enllaç (Kaggle):** https://www.kaggle.com/datasets/itzzomkar/llm-adversarial-jailbreak-and-security-benchmark
- **Contingut:** 15.000 instàncies d'avaluació de prompts, provades sobre 5 famílies de models i 5 tipus de guardrail. Segons la seva descripció, són dades de benchmark sintètiques.
- **Atribut a predir:** `is_jailbreak_success` (1 si el prompt s'ha saltat el guardrail i ha produït una sortida insegura, 0 altrament).
