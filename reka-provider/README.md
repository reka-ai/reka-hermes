# Reka for Hermes

Connect Hermes directly to [Reka](https://developer.reka.ai) using its existing
model picker and API client. You need a Reka API key from
[developer.reka.ai/keys](https://developer.reka.ai/keys). The plugin adds no
runtime dependencies. The full setup guide, with a video, is on
[developer.reka.ai](https://developer.reka.ai/integrations/agents#hermes).

## Connect

On Hermes 0.22.3 or later, install it from the Hermes plugin catalog by name:

```sh
hermes plugins install reka-provider --enable
hermes model
```

If the installer asks for `REKA_API_KEY`, paste your key (the prompt hides it)
and press Enter. In `hermes model`, select **Reka**, then press Enter to keep
your key and the default endpoint, choose **qwen3.8-27b** and pick a reasoning
effort. If you skipped the key at install, paste it when Hermes asks
`REKA_API_KEY (or Enter to cancel):`, because Enter there cancels the setup.
Higher reasoning levels can help with harder tasks but are slower; **Disable
reasoning** is the fastest. Hermes saves the key and model selection for the
active profile. For a named profile, use `hermes -p PROFILE` for both commands.
No manual YAML edit is needed.

On Hermes 0.21.6 to 0.22.2, which can't read the catalog's listing, install the
same plugin from GitHub instead:

```sh
hermes plugins install "https://github.com/reka-ai/reka-hermes#reka-provider" --enable
```

Installed from GitHub before and now on Hermes 0.22.3 or later? Switch to the
catalog copy with `hermes plugins install reka-provider --force --enable`.

## Configuration

Hermes reads `REKA_API_KEY` and sends requests to `https://api.reka.ai/v1`.
`REKA_BASE_URL` optionally selects another authorized endpoint. The provider ID is
`reka`; use this canonical name in `reka:qwen3.8-27b` model syntax.

```sh
hermes chat --provider reka -m qwen3.8-27b
```

The picker offers five models that support tool calling, have at least the 64K
tokens of context Hermes needs for an agent turn, and passed a live chat check
through Hermes:

| Model | Context window | Image input |
|---|---:|---|
| `qwen3.8-27b` (default) | 262,144 | Yes |
| `glm5.3-flash` | 1,048,576 | Yes |
| `deepseek41-flash` | 1,048,576 | Yes |
| `deepseek4-flash` | 262,144 | No |
| `qwen3.6-27b` | 262,144 | No |

Qwen 3.8 27B is the default and also runs Hermes's background tasks. Your Reka
account decides which models you can call, so a model in the picker is not a
guarantee of access. The plugin doesn't update itself: run
`hermes plugins update reka-provider` every few weeks to get new models and
fixes, then `hermes model --refresh` to clear cached model IDs.

The plugin sends Reka's top-level `reasoning_effort`: unset stays omitted,
off sends `none`, and Hermes's `ultra` maps to `max`. Which levels a model
accepts varies by model. Images you attach follow each model's declared
capability. Images inside tool results use Hermes's text fallback.

## Scope

Prompts, tool definitions and results, supported user images, and model-list
requests go to the configured Reka endpoint through Hermes. Credentials and
configuration stay managed by Hermes. The plugin registers one provider; it adds
no tools, background services, telemetry, credential files, or update mechanism.

MIT license; the license text is included in the installed directory.
