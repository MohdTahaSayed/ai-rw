PHASE 1 — DATASET
    |
    +-- Collect four datasets
    +-- Align using SHA256
    +-- Verify labels
    +-- Select informative features
    +-- Construct 318-feature dataset
    +-- Validate final dataset

PHASE 2 — DATA ANALYSIS
    |
    +-- Class distribution
    +-- Feature statistics
    +-- Feature importance
    +-- API analysis
    +-- DLL analysis
    +-- PE Header analysis
    +-- PE Section analysis
    +-- Feature-group ablation

PHASE 3 — CLASSICAL BASELINE
    |
    +-- 60:20:20 split
    +-- LazyPredict
    +-- Compare baseline models
    +-- Retain HGB reference
    +-- Error analysis

PHASE 4 — LLM DATASET
    |
    +-- Design structured representation
    +-- Design instruction format
    +-- Design output schema
    +-- Generate training examples
    +-- Validate examples
    +-- Create train/validation/test JSONL

PHASE 5 — QLoRA / SFT
    |
    +-- DeepSeek-Coder
    +-- Qwen2.5-Coder-1.5B-Instruct
    +-- Llama-3.2-3B-Instruct
    +-- Evaluate immediately after SFT

PHASE 6 — RLHF
    |
    +-- Generate candidate responses
    +-- Build preference dataset
    +-- Define reward criteria
    +-- RLHF optimization
    +-- Evaluate after RLHF

PHASE 7 — GRPO
    |
    +-- Generate response groups
    +-- Define reward function
    +-- Relative reward comparison
    +-- GRPO optimization
    +-- Evaluate after GRPO

PHASE 8 — FINAL ANALYSIS
    |
    +-- Compare SFT vs RLHF vs GRPO
    +-- Compare DeepSeek vs Qwen vs LLaMA
    +-- Feature-group ablation
    +-- Error analysis
    +-- Hallucination analysis
    +-- Grounding analysis
    +-- Computational-cost comparison

PHASE 9 — FINAL DELIVERABLE
    |
    +-- Final model
    +-- Malware-analysis pipeline
    +-- Evaluation results
    +-- Research report
    +-- GitHub documentation
    +-- Presentation
    +-- Demonstration