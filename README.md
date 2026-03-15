# omlx-tools

CLI utilities for [oMLX](https://github.com/jundot/omlx), the Apple Silicon LLM inference server.

## Tools

### omlx-top

Live TUI dashboard for monitoring the oMLX server. Shows server status, GPU/CPU/RAM usage, loaded models, and per-model performance metrics.

```bash
omlx-top                                    # localhost:11435, 2s refresh
omlx-top --url http://192.168.50.225:11435  # remote server
omlx-top -n 5                               # 5-second refresh interval
```

Requires Python 3.10+ and [rich](https://github.com/Textualize/rich).

### omlx-add

Download an MLX model from HuggingFace and register it with oMLX in one step.

```bash
omlx-add mlx-community/Qwen3-8B-4bit              # download, symlink, restart
omlx-add mlx-community/some-model --no-restart     # download and symlink only
```

Handles the full workflow: `hf download` → find snapshot hash → symlink into `~/.omlx/models/` → restart the oMLX brew service.

Requires the `hf` CLI (`pip install huggingface_hub`).

## Installation

```bash
git clone https://github.com/nireson/omlx-tools.git
cd omlx-tools
ln -s "$(pwd)/omlx-top" /opt/homebrew/bin/omlx-top
ln -s "$(pwd)/omlx-add" /opt/homebrew/bin/omlx-add
```

## License

MIT
