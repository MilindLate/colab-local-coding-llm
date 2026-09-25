# colab-local-coding-llm

Run a local, open-weight coding LLM (**Qwen2.5-Coder**, via Ollama) entirely inside a free Google Colab GPU runtime — chat with it from a real terminal, no local setup or PC required.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/MilindLate/colab-local-coding-llm/blob/main/local_coding_model_colab.ipynb)

## What this does

- Installs **Ollama** and runs it as a local model server inside the Colab VM (`localhost:11434`)
- Installs **colab-xterm**, giving you a real bash terminal inside a notebook cell — so you can just type `ollama run qwen2.5-coder:7b` and chat like a normal CLI
- Auto-detects your assigned Colab GPU (T4 / L4 / A100 / none) and picks the largest **Qwen2.5-Coder** size that actually fits in VRAM
- Includes a Python fallback (`ask_coding_model()`) for calling the model programmatically instead of typing into the terminal
- Optional integration with [`aider`](https://aider.chat) so the local model can act as a full coding agent — reading/editing files in a real git repo, not just single-shot chat

## Why Qwen2.5-Coder

Apache-2.0 licensed (no gated download, no usage restrictions), strong published coding benchmarks, and first-class support across every size tier in Ollama's registry — so the same notebook logic just swaps the model tag depending on the GPU you land on.

| GPU (Colab) | VRAM | Model tag | Notes |
|---|---|---|---|
| None (CPU only) | — | `qwen2.5-coder:1.5b` | Basic help only; switch to a GPU runtime if you can |
| T4 (free tier) | ~15 GB | `qwen2.5-coder:7b` | Best balance of speed/quality on free Colab |
| L4 / A10 (Colab Pro) | ~22–24 GB | `qwen2.5-coder:14b` | Noticeably better multi-step reasoning |
| A100 (Colab Pro+) | 40 GB | `qwen2.5-coder:32b` | Strongest open-weight tier that fits one GPU |

## Quick start

1. Click **Open in Colab** above.
2. `Runtime` → `Change runtime type` → select a GPU (T4 is free).
3. Run every cell top to bottom.
4. In the terminal that opens (Section 6), run:
   ```bash
   ollama run qwen2.5-coder:7b
   ```
   and start chatting.

## Limitations

- Nothing persists across Colab sessions — if the runtime disconnects, rerun the install/pull cells.
- Free-tier Colab GPUs can disconnect after ~90 min idle / ~12h total.
- This is single-GPU, single-user, local-only — nothing is exposed to the internet by default.
- A strong open-weight model, not a claim of parity with hosted frontier coding assistants.

## License

MIT (or your choice) — this repo is just notebook + config; the model itself is licensed separately by Alibaba under Apache-2.0.
