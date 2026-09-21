# SOKE 2.0.0 — Self‑Optimizing Knowledge Engine

SOKE is a Windows-based system for building, training, converting, expanding, healing, and inspecting AI models using a new container format: **SFF (.sff)** — a paged, gauge‑tagged, append‑only, self‑describing model store.  
It also forges new **GGUF** models from templates, harvesting weights from existing Ollama models and improving layouts through trial‑and‑error on your own text.


## **📄 README — Part 1 (Header + Summary)**

```markdown
# SOKE 2.0.0 — Self‑Optimizing Knowledge Engine

SOKE is a Windows-based system for building, training, converting, expanding, healing, and inspecting AI models using a new container format: **SFF (.sff)** — a paged, gauge‑tagged, append‑only, self‑describing model store.

It also forges new **GGUF** models from templates, harvesting weights from existing Ollama models and improving layouts through trial‑and‑error on your own text.

Author: BS Medicineman / Knight Industries
```

---

## **📄 README — Part 2 (Key Features)**

```markdown
## Features

- Dual-model chat console with advisor diagnostics
- Unified Import Store for text, PDFs, ebooks, and models
- Windows‑95 style UI skin
- PDF/ePub/HTML ingestion using only Python stdlib
- ~17 Forge template presets + 10 probe presets
- Real-time testing during training
- Tandem knowledge-tree scaffold for multi-model routing
- CLI tools for ingestion, tandem routing, forging, and inspection
- 390 self-test checks for reliability
```

---

## **📄 README — Part 3 (Installation)**

```markdown
## Installation

1. Unzip `SOKE-2.0.0.zip` anywhere (e.g., `C:\Knight\SOKE`).
2. Run `INSTALL.bat`.
   - Installs Python 3.12 if needed
   - Installs numpy
   - Creates shortcuts
   - Runs quick self-test
3. Launch via desktop icon or `SOKE.bat`.

Requirements:
- Windows 10/11
- ~200 MB disk
- Internet once for installation
- Runtime dependency: numpy only
```

---

## **📄 README — Part 4 (Tab Overview)**

```markdown
## Tab Overview

### Home
Add folders/files, choose duration, start learning, test the model, import GGUF.

### Forge
Build new GGUF models from templates using donor weights. Includes:
- Donor inventory
- Template editor
- Probes
- Trial loop (15 operators)
- Behavior fine-tuning layer
- Export to GGUF + SFF + Modelfile

### Help
Plain-language explanations of all processes.

### Build & Train
Full training controls, live loss curve, grow/heal/finalize.

### Import GGUF
Stream GGUF → SFF without loading whole file.

### Inspect SFF
View tensors, lineage, patch log, storage gauges, verification.

### Knowledge
Helical memory, ACTG strands, domain routing, math boot.

### Generate
Byte-level generation from SFF with streaming experts.

### Ledger & Self-Test
Hash-chained ledger + 375 checks.
```

---

## **📄 README — Part 5 (CLI Examples)**

```markdown
## CLI Examples

soke train --corpus C:\my\notes --model-id v001 --cycles 20 --steps 100 --finalize
soke convert C:\models\phi-3.5-mini-q4_k_m.gguf
soke inspect C:\models\phi-3.5-mini-q4_k_m.sff --opt --verify
soke generate soke_data\models\v001-final.sff --prompt "The theorem states"
soke settings --model-dir C:\Users\me\.ollama\models\blobs
soke forge-inventory
soke forge-build --donors qwen2.5/0.5b deepseek-r1-draft --preset math-always-on --topics math,language,science,code --out tpl.json
soke forge-run tpl.json --corpus C:\my\notes --trials 40 --minutes 60 --priority math --export mine.gguf
soke chat mine.gguf --prompt "What is a prime number?"
soke behavior --climate scarcity --out climate.json
soke clone --user me --session STANDARD
soke forge-run tpl.json --corpus C:\my\notes --behavior climate.json --export mine.gguf
soke forge-export tpl.json --out mine.gguf --behavior clone_profile.json --clone-consent
```

---

## **📄 README — Part 6 (SFF vs GGUF)**

```markdown
## SFF vs GGUF

| Property | GGUF | SFF |
|---------|------|-----|
| Loading | Whole-file mapped | Paged; ~60 ms open |
| Modification | Overwrite | Append-only; instant rollback |
| Checkpoints | Full copies | DELTA8 pages |
| Encoding | One quant per tensor | Per-page gauge; exact imports |
| Provenance | KV metadata | Full lineage + patch log + ledger |
| Knowledge | None | Domain helices + ACTG |
| Experts | n/a | Routed experts loaded on demand |
```

---

## **📄 README — Part 7 (Repo Structure)**

```markdown
## Repository Structure

SOKE/
  INSTALL.bat  SOKE.bat  SOKE-CLI.bat  UNINSTALL.bat
  soke_main.py
  soke/
    sff.py teeth.py
    gguf_rewrites.py
    frame_engine.py
    tower.py actg_parser.py memory_engine.py
    proof_engine.py math_engine.py
    model_engine.py kernels.py
    loss_engine.py expansion_engine.py heal_engine.py meta_optimizer.py orchestrator.py
    ledger.py memguard.py util.py selftest.py cli.py rng.py winshortcut.py
    tokenizer.py
    llm_engine.py
    forge.py forge_loop.py
    behavior.py
    clone_battery.py
    gui.py gui_home.py gui_forge.py gui_help.py
  docs/
    SFF_SPEC.md
    ARCHITECTURE.md
  tests/
  soke_data/
```

---

## **📄 README — Part 8 (Self-Test)**

```markdown
## Self-Test

Run:
SOKE.bat selftest

- 375 executed checks (317 in --quick)
- Validates RNG, frame calculus, codecs, container, GGUF dequantizers, tower, ACTG, proof engine, backward pass, heal/grow, orchestrator, tokenizer, inference engine, forge, trial loop.
```

---

## **📄 README — Part 9 (License + Contact)**

```markdown
## License
MIT License

## Contact
Author: BS Medicineman  
GitHub: https://github.com/bsmedicineman  
Email: bsmedicineman@gmail.com
```

