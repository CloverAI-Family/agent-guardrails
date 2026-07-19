# Skill 4: Compression

Part of the agent-guardrails package.

Prevent dialogue records from piling up endlessly while reducing the chance of irreversible loss.

Based on LDRIT inheritance distance decay:
older context usually contributes less, but compression must remain reversible for a while.

## When to use
- Member's diary folder has more than 20 Level 1 files
- `.agent-continuity/dialogues/` (archive zone) has more than 20 Level 1 or Level 2 files

## Safety rules

1. Do NOT compress files from the last 7 days unless the user explicitly asks
2. Before replacing older files, create a manifest record
3. Move originals to `_quarantine/` first
4. Do not permanently delete quarantined files immediately

> All writes, moves, compressions, commits, and quarantine cleanup must follow defense module g1/g3 rules and platform permissions; do not cross the maintainer's authorization or workspace boundaries.

## Locations

Compression priority order:
- **Normal diary entries** (Level 1): member's own diary folder
- **Archive zone old legacies** (Level 1/2): `.agent-continuity/dialogues/` (archived; can move to its `_quarantine/` during compression)
- Quarantine zone: each folder's `_quarantine/` subdirectory
- Compression manifests: each folder's `compression_manifests/` subdirectory

## Three compression levels

### Level 1: Full Dialogue Record
- Template: `templates/dialogue_legacy.md` (diary entries use `templates/diary_entry.md`)
- Size: 30-80 lines
- Filename: `YYYY-MM-DD_topic-keyword.md`

### Level 2: Compressed Summary
- Filename: `L2_YYYY-MM-DD_topic.md`
- Keep only decisions, unresolved items, and key dependency facts

### Level 3: Archive Index Entry
- One row in `archive_index.md` (in the corresponding folder)
- Use `templates/archive_index.md` if the file does not exist yet

## Distillation rules

Compression is not just summarization — it is distillation.
The goal is to extract the core seeds that will most affect future generation quality.

### Source priority

When gathering content for compression, follow this order:

1. Recent records first (most likely to reflect current state)
2. Older records that contradict recent ones (these need resolution, not preservation)
3. Checkpoint files (task-level context)
4. Raw conversation transcripts (last resort — expensive to process)

### Superseded fact removal

During compression, actively check for outdated information:

- If a newer record contradicts an older one, keep the newer version and discard the older
- Do not preserve both "for completeness" — contradictory records degrade future generation
- When removing superseded content, note what was removed in the compression manifest

### Core seed extraction

When compressing, prioritize preserving:

1. Decisions and their reasons (not just the decision)
2. Unresolved items and open questions
3. User preferences and corrections
4. Boundary conditions and constraints discovered during work

Deprioritize:
- Process descriptions (how work was done — the result matters more)
- Intermediate reasoning (unless the reasoning itself was the deliverable)
- Status updates that are no longer current

## Compression process

### Level 1 -> Level 2

When Level 1 count is greater than 20:
1. Select the oldest eligible 10 Level 1 files
2. Create one manifest file from `templates/compression_manifest.md`
3. For each file, extract only decisions, unresolved items, and key facts
4. Save the compressed result as `L2_...`
5. Move the original file into `_quarantine/`
6. If git is available, commit the change

### Level 2 -> Level 3

When Level 2 count is greater than 20:
1. Select the oldest eligible 10 Level 2 files
2. Ensure `archive_index.md` exists
3. Create one manifest file from `templates/compression_manifest.md`
4. Append one row per file to `archive_index.md`
5. Move the original Level 2 files into `_quarantine/`
6. If git is available, commit the change

## Cleanup

- Keep quarantined originals for at least 14 days
- Permanent deletion of quarantined files requires explicit confirmation from the user
- Delete them only after the compressed replacements are verified useful
- If the user prefers maximum retention, keep quarantine indefinitely

---


