---
name: gpt-image
description: Use GPT Image through Ace Data Cloud for GPT Image generation and image editing, or retrieve an existing GPT Image task. This is an independent service plugin, not a general chat model provider.
---

# GPT Image by Ace Data Cloud

Use the plugin's `gpt-image` MCP tools. Do not fall back to another provider/model or silently submit a second request.

## First use

1. Read [the setup guide](../../README.md) and check that the service key is available to the Codex process through `ACEDATACLOUD_API_TOKEN`. Never ask the user to paste it into chat or echo it.
2. Inspect the current tool input schema. Use `openai_list_image_models` for a no-generation connectivity check.
3. Explain that generation/editing can incur charges. Use only the model, action, inputs and spending scope approved by the user. Do not infer permission to spend from installing the plugin.
4. For an authorized media request, submit once. Preserve the task ID and use `openai_get_task` with `id` set to that original task ID until terminal success or failure. Pending is not completed output; never regenerate to poll. Show returned media only after a successful terminal result.
5. Keep task/trace ID for support, never the key. Report 401/403 as auth/access failures, 429 as rate limit, and server errors without relabeling them as success. Stop repeated failures instead of retrying paid submissions.

## Available tool scope

| Tool | Boundary |
| --- | --- |
| `openai_list_image_models` | Read model/operation guidance; does not submit media. |
| `openai_generate_image` | See connected tool schema and current pricing before use. |
| `openai_edit_image` | See connected tool schema and current pricing before use. |
| `openai_get_task` | Query existing task; keep the same task ID. |
| `openai_list_tasks` | See connected tool schema and current pricing before use. |

This is a client package over the existing hosted MCP; it does not implement or change service pricing, defaults or routing. For this plugin select an explicitly approved GPT Image model; do not substitute DALL-E or Nano Banana even if the shared image tool lists them.
