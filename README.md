# omlx-tools

CLI utilities for [oMLX](https://github.com/jundot/omlx), an Apple Silicon LLM inference server built on MLX.

## Tools

### omlx-top

Live TUI dashboard for monitoring the oMLX server. Shows server status, GPU/CPU/RAM usage, loaded models, and per-model performance metrics (requests, prefill tok/s, generation tok/s).

```bash
omlx-top                              # default: localhost:11435, 2s refresh
omlx-top --url http://10.0.0.5:11435  # remote server
omlx-top -n 5                         # 5-second refresh interval
```

Per-model performance data is read from `~/.omlx/stats.json`, which oMLX updates automatically.

### omlx-add

Download an MLX model from HuggingFace and register it with oMLX in one step.

```bash
omlx-add mlx-community/Qwen3-8B-4bit           # download, symlink, restart
omlx-add mlx-community/some-model --no-restart  # download and symlink only
```

Handles the full workflow: `hf download` → find snapshot hash → symlink into `~/.omlx/models/` → restart oMLX (if managed via Homebrew).

Some HuggingFace models require authentication. Run `huggingface-cli login` first if you hit access errors.

#### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `OMLX_MODELS_DIR` | `~/.omlx/models` | Where oMLX looks for model directories |
| `OMLX_HOME` | `~/.omlx` | Base oMLX config directory (used by omlx-top for stats) |
| `HF_CACHE_DIR` | `~/.cache/huggingface/hub` | HuggingFace download cache |

## Installation

```bash
git clone https://github.com/nireson/omlx-tools.git
cd omlx-tools
```

Symlink into your PATH:

```bash
# Using ~/.local/bin (make sure it's in your $PATH):
ln -s "$(pwd)/omlx-top" ~/.local/bin/omlx-top
ln -s "$(pwd)/omlx-add" ~/.local/bin/omlx-add

# Or for Homebrew users:
ln -s "$(pwd)/omlx-top" "$(brew --prefix)/bin/omlx-top"
ln -s "$(pwd)/omlx-add" "$(brew --prefix)/bin/omlx-add"
```

## Requirements

- macOS with Apple Silicon (M1/M2/M3/M4)
- [oMLX](https://github.com/jundot/omlx) installed and running
- Python 3.10+ with [rich](https://github.com/Textualize/rich) (`pip install rich`) — for omlx-top
- `hf` CLI from [huggingface_hub](https://github.com/huggingface/huggingface_hub) (`pip install huggingface_hub`) — for omlx-add

## License

MIT — see [LICENSE](LICENSE).
