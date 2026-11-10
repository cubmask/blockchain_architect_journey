Review my work as a senior architect in a design review.

Target: $ARGUMENTS (a file, folder, or "latest changes"; if empty, review the files I changed most recently, e.g. via git diff).

- For design docs: check requirements have numbers, trust assumptions are explicit, trade-offs and rejected alternatives are stated, and the on-chain/off-chain split is justified.
- For code: run `forge build` and `forge test`, then check security (reentrancy, access control, oracle, signatures, DoS, rounding), gas, readability and test coverage of the invariants.
- Give findings as a table: severity (critical/high/medium/low/note), location, issue, why it matters, hint to fix. Give hints, not finished fixes, unless I ask.
- End with what I did well, and 1 to 3 check questions.
