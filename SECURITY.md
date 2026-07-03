# Security

This repository is intended for public review (e.g. job applications). Follow these steps before sharing it.

## Exposed credentials in project history

The upstream **IIA4XAI** repository historically contained a **hardcoded Hugging Face user access token** in notebook source code. That token must be treated as **compromised**.

### Required manual actions

1. **Revoke the exposed token** at [Hugging Face → Settings → Access Tokens](https://huggingface.co/settings/tokens). Create a new token only if you still need one, and store it in `.env` or your shell environment — never in source files.
2. **Verify Git history** before making the repo public or sending links to recruiters:
   - This `static.` repository was recreated with a **clean initial commit** (no token in current history).
   - The original `vannoordenne/IIA4XAI` repository may still contain the token in its commit history. If that repo is or was public, assume the token was scraped and **revoke it regardless**.
3. **Do not commit** `.env`, API keys, Colab secrets exports, or personal Google Drive paths.

### Local checks

Run these from the repository root before sharing:

```bash
git grep -n "hf_"          # should return no real token values
git grep -n "auth_token"   # should return no hardcoded token strings
```

## Configuration (no secrets in source)

| Variable | Purpose |
|----------|---------|
| `HF_TOKEN` | Hugging Face authentication for model downloads |
| `IIA4XAI_OUTPUT_DIR` | Writable folder for images and CSV output |
| `IIA4XAI_PROMPT_FILE` | Path for the latest generated prompt text |

Copy `.env.example` to `.env` for local runs.

### Google Colab Secrets (recommended in Colab)

1. Open the notebook in Colab.
2. Click the **key icon** in the left sidebar → **Secrets**.
3. Add a secret named **`HF_TOKEN`** with your Hugging Face token.
4. Optional: `IIA4XAI_OUTPUT_DIR`, `IIA4XAI_PROMPT_FILE` for custom paths.
5. Run the setup cell — the notebook reads secrets automatically (no token in source).

If no secret is set, the notebook falls back to interactive `notebook_login()`.

## Reporting

If you discover a credential in this repository, open an issue or contact the maintainer privately so it can be rotated and removed from history.
