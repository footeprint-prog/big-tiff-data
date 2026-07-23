# big-tiff-data

Data store for the **Big Tiff StoryForge** writing tool (`writing.html`). This
repo is read on every tool load and written to by Erica's browser as she writes.

**Do not edit these JSON files by hand** unless you know what you're doing — the
tool manages them. They are:

| File | What it holds |
|---|---|
| `accounts.json` | User accounts: username, role, and a salted password **hash** (never a plaintext password). Set these with the hash-generator helper (see the storyforge repo's `SETUP.md`). |
| `drafts.json` | Erica's current per-scene draft text. Draft prose is **encrypted** (AES-GCM) — the plaintext is never stored here, only ciphertext. |
| `checkpoints.json` | Named Draft Pad checkpoints per scene (also encrypted). |
| `stats.json` | Writing stats + achievement/event log that drives the tool's progress + rewards. |

## Privacy model (read this)

This repo is **public**, so anyone can read these files. Draft/checkpoint prose
is encrypted with a key embedded in the tool, which keeps casual GitHub browsers
from reading the story but is **only "lightly private"** — a determined person
who opens the tool's source could extract the key. Do not treat this as strong
confidentiality. Nothing sensitive beyond the novel drafts should live here.

Login (the account hashes here) is a **soft gate**, not real security — it keeps
casual visitors out, nothing more.

Writes happen from Erica's browser using a fine-grained GitHub token she pastes
into the tool once (scoped to this repo only, `Contents: Read and write`). The
token is stored only in her browser and is never committed here.
