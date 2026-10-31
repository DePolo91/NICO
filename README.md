# NICO — Non-Instructed Curiosity Organism

NICO is an experiment, not an app or an assistant. It starts knowing nothing and learns on its own by reading, first children's stories, then literature, then science. Nobody tells it what to ask or what to like. The question is whether, over time, it develops curiosity, preferences and questions of its own.

This project does **not** claim to create a conscious being. It builds a system with the ingredients that scientific theories associate with consciousness, and documents what appears — success or failure.

## Status

Design complete. Prototype in development. Target first reading: December 2026.

## Documents

| Document | Language |
| --- | --- |
| [Pre-registration](docs/pre-registration.md) | English (reference) |
| [Pre-registro](docs/pre-registro.md) | Español |

The pre-registration fixes the claims, success and failure criteria, timeline and ethical rules **before** the system runs, so results cannot be reinterpreted afterwards.

## Design in one paragraph

A small local language model acts only as an interpreter: it turns text into concepts and internal doubts into words, and never decides anything. Memory, concept graph and drives belong to NICO and start empty. Curiosity is measured as learning progress. NICO runs offline in a sandbox, with no network access.

## Data policy

NICO's memory and logs stay private until 3,000 life hours. A SHA-256 hash of the logs is published periodically, so anyone can later verify the released logs were not altered.

## License

All rights reserved for now. A license (likely with responsible-use conditions) will be published before the code is released.
