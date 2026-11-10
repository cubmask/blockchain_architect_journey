# Blockchain Architect Journey

A mentored path from first smart contract to blockchain solution architect, run with Claude Code. Every module is a real system built end to end: requirements, HLD, LLD, implementation, security review, operations.

## Setup (once)
1. Install Claude Code, Node.js 20+, and Git.
2. Install Foundry: `curl -L https://foundry.paradigm.xyz | bash` then `foundryup` (on Windows, use WSL).
3. Put this folder under git: `git init && git add . && git commit -m "Start journey"` (optionally push it to a private GitHub repo).

## Every session
```
cd blockchain-architect-journey
claude
/start-session
```
- `/start-session [focus]` recaps where you are and starts the lesson. The first time, it runs a short diagnostic.
- `/review [file or folder]` gets a design-review style critique of your design doc or code.
- `/wrap-up` records decisions, updates your profile, sets homework and suggests a commit.

Commit after every session so your portfolio and progress are saved.

## What's here
- `CLAUDE.md`: the mentor's instructions (loaded automatically by Claude Code).
- `CURRICULUM.md`: Stage 0 bootcamp plus 10 real systems and a capstone.
- `TEMPLATES.md`: requirements, HLD, LLD, ADR, security checklist templates.
- `LEARNER_PROFILE.md`: your level and progress; the mentor keeps it updated.
- `systems/`: one folder per system you build, e.g. `systems/00-tip-jar/`.

Never commit private keys. Use a fresh test wallet, and keep keys in `.env` (already git-ignored).
