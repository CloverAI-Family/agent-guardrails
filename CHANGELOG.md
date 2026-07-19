# Changelog

All notable changes to agent-guardrails will be documented in this file.

This project follows a simple public changelog format. Version numbers may be introduced once tagged releases begin.

## Unreleased

### Added

- `SECURITY.md` with vulnerability reporting guidance and safety scope.
- `CONTRIBUTING.md` with contribution rules, privacy boundaries, and pull request checklist.
- `CHANGELOG.md` to track public project changes.
- `docs/quickstart.md` with a short first-run setup path.
- `examples/` with starter workflows for trigger tables, delivery scans, and continuity checkpoints.

## 0.1.0 - Initial Public Release

### Added

- Initial public `agent-guardrails` framework.
- Five module structure: `defense`, `continuity`, `quality`, `review`, and `watchdog`.
- Installation guide for copying the module folder and wiring trigger tables.
- MIT license.
- README background and platform scope notes.

### Notes

- The framework was developed and tested on Claude Code.
- Concepts can be adapted to other AI coding or agent platforms, but hooks and trigger mechanics may require platform-specific changes.
- The framework is not a complete security boundary by itself; host platform permissions and human review remain necessary.
