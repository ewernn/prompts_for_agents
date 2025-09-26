---

for karpathy's repo https://github.com/karpathy/nanoGPT.git

---

# nanoGPT

Simplest repository for training/finetuning medium-sized GPT models.

## Repository Structure

```
nanoGPT/
├── config/             # Training config files
├── data/               # Dataset prep scripts
│   ├── shakespeare/    # Shakespeare text dataset
│   ├── shakespeare_char/ # Character-level Shakespeare
│   └── openwebtext/    # OpenWebText dataset
└── assets/             # Images and diagrams
```

## Quick Start

1. Install dependencies
   ```bash
   pip install torch numpy transformers datasets tiktoken wandb tqdm
   ```

2. Train on Shakespeare (character-level)
   ```bash
   python data/shakespeare_char/prepare.py
   python train.py config/train_shakespeare_char.py
   ```

3. Generate samples
   ```bash
   python sample.py --out_dir=out-shakespeare-char
   ```

## Core Components

### Model
**Purpose**: GPT model implementation
**Entry point**: `model.py`
**Key classes**:
- `GPT` - Main model class
- `GPTConfig` - Configuration
- `CausalSelfAttention` - Attention mechanism

### Training
**Purpose**: Train or finetune models
**Entry point**: `train.py`
**Supports**: Single GPU, DDP multi-GPU, multi-node

### Sampling
**Purpose**: Generate text from trained models
**Entry point**: `sample.py`
**Options**: Temperature, top-k, custom prompts

### Configuration
**Purpose**: Training hyperparameters
**Entry point**: `config/` directory
**Key files**:
- `train_shakespeare_char.py` - Quick demo
- `train_gpt2.py` - Reproduce GPT-2
- `finetune_shakespeare.py` - Finetuning example

### Data Preparation
**Purpose**: Process datasets for training
**Entry point**: `data/*/prepare.py` scripts
**Creates**: `train.bin` and `val.bin` files

## Architecture

The model (`model.py`) defines a GPT transformer. Training (`train.py`) loads configs from `config/`, reads data from `data/`, and saves checkpoints to `out_dir`. Sampling (`sample.py`) loads checkpoints and generates text.

## Navigation Guide

To work on:
- Model architecture → `model.py`
- Training loop → `train.py`
- Text generation → `sample.py`
- Hyperparameters → `config/`
- Dataset prep → `data/*/prepare.py`
- Benchmarking → `bench.py`

## Current Status

**Working**:
- Character-level Shakespeare training
- GPT-2 reproduction on OpenWebText
- Single GPU and multi-GPU training
- Finetuning from pretrained checkpoints
- Sampling from trained models

**Requirements**:
- PyTorch 2.0+ recommended
- GPU optional (CPU and Apple Silicon MPS supported)
- Use `--compile=False` on Windows or older PyTorch

---

## Documentation Update Guidelines

### Core Principle
Delete first, add second. Always remove outdated content before adding new documentation.

### Update Rules
- **Present tense only** - Document what exists now
- **No history** - Delete references to previous versions
- **No promises** - Remove all "TODO" and "coming soon"
- **Test everything** - Verify every command and path
- **Keep it minimal** - If it's obvious from the code, don't document it

### When to Delete
- References to removed features
- Anything containing "previously", "will be", or "planned"
- Documentation you can't verify
- Explanations of obvious things

### When to Update
- Feature added → Update immediately
- Feature removed → Delete docs first
- Found outdated section → Delete or fix now

Remember: Documentation is complete when there's nothing left to remove.