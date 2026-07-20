# Changelog

All notable changes to agent-guardrails will be documented in this file.

This project follows a simple public changelog format. Version numbers may be introduced once tagged releases begin.

## Unreleased

No unreleased changes yet.

## 0.1.0 - Initial Public Release

### Added

- Initial public `agent-guardrails` framework.
- Five module structure: `defense`, `continuity`, `quality`, `review`, and `watchdog`.
- Installation guide for copying the module folder and wiring trigger tables.
- `SECURITY.md` with vulnerability reporting guidance and safety scope.
- `CONTRIBUTING.md` with contribution rules, privacy boundaries, and pull request checklist.
- `CHANGELOG.md` to track public project changes.
- `docs/quickstart.md` with a short first-run setup path.
- `docs/modules.md` with a one-page overview of the five modules.
- `docs/platform-adaptation.md` with guidance for adapting the framework outside Claude Code.
- `examples/` with starter workflows for trigger tables, delivery scans, and continuity checkpoints.
- GitHub issue templates for bug reports, feature requests, and documentation issues.
- GitHub pull request template with safety and verification checks.
- MIT license.
- README background and platform scope notes.

### Notes

- The framework was developed and tested on Claude Code.
- Concepts can be adapted to other AI coding or agent platforms, but hooks and trigger mechanics may require platform-specific changes.
- The framework is not a complete security boundary by itself; host platform permissions and human review remain necessary.
