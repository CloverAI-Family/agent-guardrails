# Skill 3: Load Past Context

Part of the agent-guardrails package.

Find and load relevant records from previous conversations.

## When to use
- User references past work
- You need historical context for the current topic

## 搜尋兩個位置（v0.1 規則）/ Two search locations

**Location 1 (new, priority)**: Member's own diary folder (each member records their path in their own MEMORY or CLAUDE.md)
**Location 2 (archive, read-only)**: `.agent-continuity/dialogues/` (old archive zone, read-only)

Search both locations; merge results and rank by score.

If both are empty: load nothing, continue normal operation.

Ignore in both locations:
- `_quarantine/`
- `compression_manifests/`

## How to search

### Step 1: Index first

If the diary folder or `.agent-continuity/dialogues/` contains an `archive_index.md`, read its table first to shortlist candidates —
do not open any record files before shortlisting.
Then list filenames in both folders to catch any unindexed files.

### Step 2: Quick topic scan

For each shortlisted candidate, read only the minimum needed:
- Level 1 files: frontmatter + first 5 lines
- Level 2 files (`L2_` prefix): first 8 lines

This gives topic + date + importance without loading full files.

### Step 3: Match and score (three factors)

Score = relevance + recency + importance.
(Three-factor retrieval follows Generative Agents, Park et al. 2023 — adapted
as heuristics, no vector search needed.)

| Factor | Signal | Points |
|--------|--------|--------|
| Relevance | Topic keyword matches user's words | +1 per match (max +3) |
| Relevance | Topic meaning is similar | +2 |
| Recency | Within last 7 days | +2 |
| Recency | Within last 30 days | +1 |
| Importance | Frontmatter `importance` 8-10 | +3 |
| Importance | Frontmatter `importance` 5-7 | +2 |
| Importance | `importance` 1-4 or missing | +1 |
| Bonus | Has unresolved items | +1 |

Backward compatible: legacies without an `importance` field score +1
on that factor — old files still work.

This is **heuristic semantic matching**, not vector search. Use meaning, not just exact string overlap.

### Step 4: Load top results

- Read full content of the top 3 scoring legacies at most
- If a candidate is a Level 3 archive row, the row itself is the context
- If nothing scores above 0, load nothing

### Edge case: "Continue from last time"

- Load the most recent record from both locations regardless of topic score
- If multiple recent topics are plausible, ask the user to choose

---


