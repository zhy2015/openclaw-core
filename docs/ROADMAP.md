# Roadmap

## Phase 1 — Engine-only stabilization

- [x] replace polluted workspace snapshot with engine-only skeleton
- [x] restore minimal runtime dependency chain for core tests
- [x] add bilingual README and architecture overview
- [ ] remove remaining host/workspace residue from repo root
- [ ] make CLI path handling more robust

## Phase 2 — Standalone execution closure

- [ ] make sample workflow execution independent of external workspace state
- [ ] remove or replace legacy runtime assumptions
- [ ] provide one deterministic built-in smoke workflow path
- [ ] ensure `workflow run` works in a fresh clone

## Phase 3 — Public engine usability

- [ ] add stronger install/bootstrap contract
- [ ] add workflow smoke CI job
- [ ] document extension points for new tools/skills
- [ ] separate stable public API from internal experimental modules

## Phase 4 — Production-grade polish

- [ ] improve repository boundary discipline
- [ ] refine architecture docs and diagrams
- [ ] add more focused engine/runtime tests
- [ ] publish usage examples and integration patterns
