# Changelog

Each release is a tagged commit on `main`. Update an installed plugin with
`hermes plugins update reka-provider`, then run `hermes model --refresh`.

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
