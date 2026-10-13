# Reka for Hermes

Use [Reka](https://developer.reka.ai) models in
[Hermes Agent](https://github.com/NousResearch/hermes-agent). This plugin adds
Reka as a model provider, so you pick it in `hermes model` like any built-in
provider. Requests go straight to Reka's OpenAI-compatible application
programming interface (API) at `https://api.reka.ai/v1`.

**[Screenshot quickstart: install, add your key, pick a model](docs/quickstart.md)**

## Install

You need Hermes 0.21.6 or later and a Reka API key from
[developer.reka.ai](https://developer.reka.ai).

```sh
hermes plugins install "https://github.com/reka-ai/reka-hermes#reka-provider" --enable
hermes model
```

In `hermes model`, select **Reka**, enter your key, keep the default endpoint and
choose **qwen3.8-27b**. Then start a chat:

```sh
hermes chat --provider reka -m qwen3.8-27b
```

## Models

The picker offers five models that support tool calling and have at least the
64K tokens of context Hermes needs for an agent turn:

| Model | Context window | Image input |
|---|---:|---|
| `qwen3.8-27b` (default) | 262,144 | Yes |
| `glm5.3-flash` | 262,144 | Yes |
| `deepseek4-flash` | 262,144 | No |
| `deepseek-v4-pro` | 1,048,576 | No |
| `qwen3.6-27b` | 262,144 | No |

Your Reka account decides which models you can call. Prices are listed on
[developer.reka.ai](https://developer.reka.ai).

## What the plugin does

- Declares each model's context window, tool support, reasoning support and
  image input, so Hermes does not have to guess them.
- Sends Hermes's reasoning setting as Reka's `reasoning_effort` field. With no
  setting, nothing is sent and the model's own default applies.
- Lists only the models above, even when your account's catalog contains more.

It registers one provider and nothing else: no tools, background services,
telemetry or update mechanism. Hermes manages your key; the plugin never reads
credential files. The installed code is the [`reka-provider`](reka-provider)
folder.

## Configuration

| Variable | Purpose |
|---|---|
| `REKA_API_KEY` | Your Reka API key. Set it through `hermes model` or the dashboard's **Keys** page. |
| `REKA_BASE_URL` | Optional. Another authorized Reka endpoint instead of `https://api.reka.ai/v1`. |

## License

[MIT](LICENSE)
