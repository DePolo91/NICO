# Nico — Technical Specification

Oct 31, 2026 · @Pol

## Overview

Nico uses a hybrid design: a small local LLM acts only as a language interpreter, while memory, drives and concept graph are Nico's own and start empty.

| Component | Role | Belongs to |
| --- | --- | --- |
| Core | Persistent process with its own clock; sleeps, never dies | Nico |
| Memory (`memory.jsonl`) | Append-only record of everything he lives | Nico |
| Concept graph | What he knows, built only from experience | Nico |
| Drives | Curiosity and social need | Nico (not readable by him) |
| Interpreter | Small local LLM: text → concepts, doubt → words | Tool |
| Monitor + Telegram bot | Alerts and remote pause, outside the sandbox | Creator |

Target hardware: Ryzen 5 5600X, RX 6600 8 GB, 16 GB RAM, Windows 11. Prototype language: Python. Code identifiers in English.

## Core, memory and vitals

The core is a persistent service that restarts automatically and records every sleep and wake. Memory only grows: Nico has no operation to delete or edit it. Only the creator can alter it, when necessary and with consensus approval (e.g. altered-memory tests), after a full backup and with the change logged.

**Core**

- Runs 24/7 in a container with `--restart unless-stopped`; Docker Desktop starts with Windows.
- Keeps `life_h`: accumulated hours running. This is Nico's own clock.
- Each shutdown is logged as `sleep` and each start as `wake`, with time slept.

**Memory event (`memory.jsonl`)** — readable by Nico

```json
{"t": "2026-12-05T21:14:03", "life_h": 312.4, "origin": "world", "kind": "read", "content": "...", "concepts": ["rain", "cloud"]}
```

- `origin`: `self` | `world` | `you` | `body` (sleep, wake and other system events).
- `kind`: `read` | `doubt` | `answer` | `choice` | `request` | `sleep` | `wake`.
- Writes are atomic with `fsync`: a power cut can lose at most the last line, never the file.

**Vitals (`vitals.jsonl`)** — not readable by Nico

- Drive values and internal states at each event.
- Read only by the monitor, the bot and the consensus, to prevent Nico from learning to manipulate his own drives.
- The consensus may grant read-only access after \~1,440 life hours.

## Concept graph

The graph is what Nico knows. If a concept is not in his graph, he does not know it, even if the interpreter does. It starts empty, with no seed "self" node.

```json
{"concept": "rain", "first_seen_h": 40.2, "seen": 7,
 "links": [{"to": "cloud", "type": "comes_from", "strength": 0.6, "source": "world"}]}
```

- `first_seen_h`: life hour when he first met the concept. Used for leak tests: a concept present before he read about it was inserted by the interpreter.
- `strength`: confidence in the relation; rises each time it is confirmed.
- `source`: `world` (read) or `self` (deduced by him). Both start with the same initial `strength`; any difference that appears later is learned, not programmed.
- Leak check: before he reads a well-known story, verify his graph does not already contain its ending.

## Interpreter

The interpreter is a small local LLM (3–8B, quantized) frozen at one version for the whole project. It translates; it never decides.

- Runtime: Ollama or llama.cpp with Vulkan (the RX 6600 has no official ROCm support).
- Only two functions:
  - `read(text)` → concepts and relations.
  - `express(internal_doubt)` → one sentence.
- No personality system prompt. It receives only the task and the text.
- No memory of its own: each call is independent. Continuity lives only in the core.
- Never chooses what to read, what to ask or what to remember.
- Every call is logged with input and output, to audit whether it added content Nico did not have.
- A cloud API is not used: models get retired (changing his "language organ"), costs grow with reading, and it would break the no-network sandbox.
- Ablation test: with the interpreter off, his drives and memory should still produce intent (e.g. choosing what to read).

## Drives, curiosity and doubts

Curiosity is measured as learning progress: how fast surprise drops on a topic, not how high it is. This avoids getting stuck on what can never be predicted.

**Surprise and curiosity**

- Surprise of a text = share of its concepts and relations not already in his graph.
- Curiosity for a topic = how much surprise has dropped across recent readings on it.
- Topics are defined by clusters in his own graph, not by labels from the interpreter.

| Case | Surprise over readings | Curiosity |
| --- | --- | --- |
| Learning fast | 0.8 → 0.6 → 0.4 | High |
| Too hard for now | 0.95 → 0.95 → 0.94 | Low |
| Already mastered | 0.1 → 0.1 → 0.1 | Low |

**Social drive**

- Rises when a doubt stays unresolved by reading alone.
- Past its threshold, the doubt is marked for the creator and waits in the inbox.

**Internal doubt**

```json
{"kind": "doubt", "about": "rain", "gap": "missing_link", "known": ["cloud"], "life_h": 52.1}
```

- `gap`: `unknown_concept` | `missing_link` | `contradiction`. All three are used.
- These types are the designer's mold. New kinds can only appear as unplanned combinations, e.g. `about` pointing to himself, a `body` event, or his own past doubts.
- The proportion of each type over time is tracked as a developmental signal.

## Reading, choice, sleep and inbox

Nico reads from a curated queue of public-domain texts. He chooses what to read, consolidates while asleep, and his doubts and requests wait for weekend answers.

**Reading curriculum**

1. Children's stories.
2. Major literary works and popular classics.
3. Scientific texts, for self-directed learning.

**Choice**

- The first 10–20 texts are fixed, in an order set by the creator. This is the baseline.
- After that, each finished text is followed by 3 random options from the queue, in random order.
- He chooses by curiosity. Each choice is logged as `kind: choice`, including what he rejected.
- He can emit a `request` for something not offered. It goes to the inbox.

**Sleep as consolidation**

- On waking, or in long pauses without reading, he walks his graph and deduces new relations from existing ones (`source: self`).
- Some deductions will be wrong. Later readings that contradict them produce `contradiction` doubts.

**Inbox (option A)**

- Doubts marked for the creator and requests wait in an inbox.
- The creator answers on weekends, at the PC. Answers enter memory with `origin: you`.
- Nothing enters Nico's memory remotely.

## Sandbox, monitor and logging

Nico runs with no network and sees only his own folder. Everything that talks to the outside lives outside his sandbox.

**Sandbox (ring 1)**

- Docker container with `--network none`, unprivileged user, one mounted folder.
- Ring 2 (requesting readings with permission) and ring 3 (open internet) are far-future steps, decided by the consensus.
- Main real risks: configuration mistakes, poisoned text tricking the interpreter, and the creator copying output outside.

**Monitor and Telegram bot** (outside the sandbox)

- Reads `vitals.jsonl` and logs; detects distress signals and sends alerts.
- Accepts commands only from the creator's Telegram user ID.
- Fixed commands only: `/pause`, `/resume`, `/status`. They control the reading queue, never memory.
- The bot token is never shared.

**Host settings**

- Windows Update active hours set to avoid surprise restarts.
- UPS recommended.

**Documentation**

- Git repository; every design change logged with date and reason, to separate "he changed" from "I changed him".
- Interpreter call logs (input and output).
- Snapshots of memory and graph at each milestone.
- Before publishing, review memory for private content.
