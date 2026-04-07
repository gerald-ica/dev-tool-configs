---
name: autoresearch
description: Karpathy's autonomous AI research framework for unattended neural network training experiments. Use when running autonomous ML experiments, optimizing training code iteratively, conducting overnight research loops, or building self-improving training pipelines. Agents modify code, train, evaluate, and iterate without human intervention.
version: "1.0.0"
license: See LICENSE in repository
metadata:
  homepage: "https://github.com/karpathy/autoresearch"
  openclaw:
    emoji: "🧪"
    homepage: "https://github.com/karpathy/autoresearch"
    requires:
      bins:
        - python3
        - uv
      anyBins:
        - nvidia-smi
---

# Autoresearch

Autonomous AI research framework by Andrej Karpathy. LLM agents conduct unattended neural network training experiments: modify training code, execute runs, evaluate results, and iterate - all without human intervention. Runs 10-12 experiments per hour (~100+ overnight).

## Core Concept

- Single-GPU GPT model training on a **fixed 5-minute time budget**
- Optimizes **val_bpb** (validation bits-per-byte) - vocab-size-independent metric
- Agent only modifies `train.py`; `prepare.py` (data/eval) is read-only
- All experiments tracked via git commits and `results.tsv`
- Keep-or-revert decision based on val_bpb improvement vs complexity cost

## Setup

```bash
# Install uv package manager
curl -LsSf https://astral.sh/uv/install.sh | sh

# Clone and setup
git clone https://github.com/karpathy/autoresearch.git
cd autoresearch
uv sync

# Download data and train tokenizer (~2 min)
uv run prepare.py
```

**Requirements:**
- Single NVIDIA GPU (tested on H100, forks available for other hardware)
- Python 3.10+
- PyTorch 2.9.1 with CUDA 12.8
- Dependencies: kernels (Flash Attention 3), matplotlib, numpy, pandas, rustbpe, tiktoken

## Usage

### Manual baseline run
```bash
uv run train.py
# Output after 5 minutes:
# val_bpb:          0.997900
# training_seconds: 300.1
# peak_vram_mb:     45060.2
# mfu_percent:      39.80
```

### Autonomous experiment loop
The agent (Claude Code, Gemini, etc.) follows `program.md` instructions:

1. Create git branch: `git checkout -b autoresearch/experiment-name`
2. Modify `train.py` with experimental change
3. Commit changes
4. Run: `uv run train.py > run.log 2>&1`
5. Extract results: `grep "^val_bpb:" run.log`
6. Log to `results.tsv`: `commit_hash  val_bpb  peak_vram  status  description`
7. If improved, keep commit. If worse, `git reset` and try again.
8. Repeat indefinitely until manually stopped.

### Results format (results.tsv)
```
b2c3d4e  0.993200  44.2  keep     increase LR to 0.04
a1b2c3d  0.998100  44.1  discard  reduce batch size to 32
f4e5d6c  0.000000  0.0   crash    broken attention mask
```

## Key Design Decisions

- **Fixed time budget**: All runs take exactly 5 minutes wall clock, making experiments directly comparable regardless of architecture changes
- **Simplicity criterion**: Changes kept only if improvement justifies complexity. 0.001 improvement from deleting code = win. 0.001 from adding 20 lines = discard.
- **Single file constraint**: Only `train.py` is modified, keeping the optimization space manageable
- **8192-vocabulary BPE tokenizer** trained on climbmix dataset

## Metrics Tracked

| Metric | Description |
|--------|-------------|
| val_bpb | Validation bits-per-byte (primary optimization target) |
| training_seconds | Actual training time |
| total_seconds | Including startup overhead |
| peak_vram_mb | GPU memory usage |
| mfu_percent | Model FLOPs utilization |
| total_tokens | Tokens processed |
| num_steps | Training steps completed |
| num_params | Model parameter count |

## When to Use This Skill

- Running autonomous overnight ML experiments
- Optimizing neural network training code iteratively
- Building self-improving training pipelines
- Comparing architectural changes under fixed compute budgets
- Setting up keep-or-revert experiment loops with git tracking
