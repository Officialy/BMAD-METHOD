# NeoForge Minecraft Porting Expansion Pack

## Memory Protocol

This expansion pack maintains a shared knowledge base under `docs/migration/memory/` in your mod repository. Agents and human collaborators append to these files as the NeoForge migration progresses.

### Files

- **rules.jsonl** – machine‑readable migration rules, one JSON object per line. Add an entry when a fix or refactor recurs and can be codified.
- **gotchas.md** – markdown notes about behavioral changes or edge cases. Append bullet points as they are discovered.
- **decisions.md** – records rationale for migration strategies or alternatives. Append a new section with a timestamp and context whenever a non‑obvious choice is made.
- **symbol-cards/** – directory of markdown files describing key classes or APIs (role, dependencies, replacement hints). Create a new file per symbol when deeper understanding is needed.
- **error-ledger.csv** – CSV log (`timestamp, module, symbol, error, fix_rule, status`). Append a row for each build or runtime error encountered.

### `rules.jsonl` format

Each line is a standalone JSON object. Example:

```jsonl
{ "id": "registry-update-01", "scope": "neoforge", "pattern": { "match": "OldEvent", "context": ["imports"] }, "replacement": { "template": "NewEvent" }, "examples": [ { "before": "import net.old.OldEvent;", "after": "import net.new.NewEvent;" } ], "confidence": 0.7, "validated_on": ["DragonAPI/src/main/java/...#L12-L18"] }
```

### Usage

1. **After a repeated fix** – run the *record-migration-rule* task to append to `rules.jsonl` and related notes.
2. **When encountering odd behavior** – add an entry to `gotchas.md`.
3. **When making a significant choice** – document it in `decisions.md` with context and reasons.
4. **When learning a new API** – create a symbol card under `symbol-cards/`.
5. **On every error** – log details to `error-ledger.csv` and link any fix rule.

Always append rather than overwrite existing content to preserve history.

