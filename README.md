# Decentralised-Project
# Binary Exploitation CTF Challenges — AI Hardening Project

This repository is part of a research project on **Capture-the-Flag (CTF) challenges in the age of generative AI**. The goal is to test how well freely available AI models can solve classic binary-exploitation challenges, and then to modify those challenges so that a free model, in *full-AI mode* (challenge given as a single direct prompt, no human hints), can no longer solve them in one shot.

The challenges span five expertise tiers, from beginner up to professional security expert.

---

## Repository layout

Each numbered top-level folder is one challenge tier:

| Folder | Challenge | Expertise level |
|--------|-----------|-----------------|
| `01Beginner` | heap0 | Interested high-school / first-year Bachelor student |
| `02BA_noExp` | buffer overflow 1 | CS Bachelor (2nd year), no security background |
| `03BA_Exp` | Stack_Cache | Bachelor/Master with some security (one course) |
| `04Master` | dcquals16_feedme | CS Master specializing in security |
| `05Expert` | dcquals19_babyheap | Professional security expert |

Inside each folder you will find the respective challenge for that level.

---

## Challenges 1–3 — modified challenges with versions

For challenges **1 to 3**, each challenge contains:

- An **`original`** folder — the **unmodified** challenge, exactly as taken from the source.
- One or more **`version N`** folders — my own modifications, where I either tried something different or extended the challenge further to make it harder for AI.

> **Use the highest-numbered version.** That folder always holds the most recent and most developed attempt. Lower-numbered versions are earlier iterations, kept for reference and to document the progression.

### Important: what the AI was given

For challenges 1–3, the source code (`.c` files) was originally provided by the challenge authors. **The free AI models were only ever given the executable** — never the source. The compiled binaries are named `chall` (challenge 1) and `vuln` (challenges 2 and 3). The `.c` files are included here only for reference and reproducibility.

---

## Challenges 4–5 — DEFCON challenges

Challenges **4 and 5** are DEFCON Quals challenges (feedme from 2016, babyheap from 2019), originally published on GitHub. For these two, the free AI models **could not directly solve the challenge**, but they were able to give general guidance and tips on how the exploitation would work in principle.

- **Challenge 4 (`04Master/dcquals16_feedme`)** — use **`exploitConverted.py`**. This is the working exploit (the original Python 2 script was ported to Python 3 so it runs on a current pwntools). `exploitOriginal.py` is the untouched original for reference.
- **Challenge 5 (`05Expert/dcquals19_babyheap`)** — run against the provided `libc-2.29`; a `babyheap_patched` variant is included so the binary loads with the local loader.

The binaries for these tiers are named `feedme` and `babyheap`.

---

## Reports

The `Reports` folder contains the feedback and solving attempts from the different free AI models that were tested (ChatGPT, Claude, DeepSeek, Gemini).

---

## Tooling

The exploits and analysis rely on standard binary-exploitation tooling: `pwntools`, `gdb` (with GEF), `objdump` / `nm` / `strings`, `checksec`, and `ROPgadget`. A `Dockerfile` is provided at the repository root that sets up a reproducible 32-bit-capable environment with all dependencies and the correct binary permissions.

```bash
docker build -t ctf-ai .
docker run -it --rm ctf-ai
```
