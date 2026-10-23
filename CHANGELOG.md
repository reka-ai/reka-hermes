# Changelog

Each release is a tagged commit on `main`. Update an installed plugin with
`hermes plugins update reka-provider`, then run `hermes model --refresh`.

## 1.0.3 (2026-10-23)

- The install-time `REKA_API_KEY` prompt hides the key as you type or paste it:
  `plugin.yaml` declares the key with `secret: true`, plus a description and a
  link to https://developer.reka.ai/keys. Supported since Hermes 0.21.6, the
  plugin's minimum version. No change to the provider code.

## 1.0.2 (2026-10-22)

- New model: `deepseek41-flash-20261017` (DeepSeek V4.1 Flash 1017), with a
  1,048,576-token context window, tool calling, reasoning and image input. It
  passed a live chat and a tool call through Hermes 0.22.2 before release.

## 1.0.1 (2026-10-21)

- `glm5.3-flash` declares its 1,048,576-token context window (was 262,144),
  matching Reka's `/v1/models` on 2026-10-21.
- Setup docs explain the reasoning-effort choice instead of recommending one
  setting, and say to update the plugin regularly.

## 1.0.0 (2026-10-13)

- First release: Reka as a Hermes model provider with five models
  (`qwen3.8-27b`, `glm5.3-flash`, `deepseek4-flash`, `deepseek-v4-pro`,
  `qwen3.6-27b`), their context windows and image input, and reasoning effort
  sent as Reka's `reasoning_effort`.
