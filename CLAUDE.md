# llm-training-lab

Hands-on pretraining and post-training (SFT, DPO, GRPO) of small LLMs, published with costs and before/after numbers.

## Tech Stack

Python 3.11+ (uv), PyTorch, Karpathy nanochat (pretrain → SFT → RL), Hugging Face TRL + PEFT/LoRA, Modal for GPUs.

## Commands

- Setup: `uv sync`
- Tests: `uv run pytest`
- Modal GPU runs must be prefixed `GPU_ESTIMATE='<time>, $<cost>'`.

<!-- Keep this lean — only what the agent needs while coding.
     No partnership context, goals, or tracking: those live in knowledge/ or the
     project's private working notes. -->
