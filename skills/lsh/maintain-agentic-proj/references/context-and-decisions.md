# Context and Decision Docs

Use this reference when maintaining optional `CONTEXT.md`, `CONTEXT-MAP.md`, or ADR files.

## CONTEXT.md

`CONTEXT.md` is a glossary for project-specific language. It is not a spec, plan, status file, or scratch pad.

Format:

```md
# Context Name

One or two sentences describing the context.

## Language

**Canonical Term**:
One or two sentences defining what it is.
_Avoid_: synonym, overloaded old term
```

Rules:

- Include only terms specific to this project or research area.
- Prefer one canonical term and list avoided synonyms.
- Keep definitions tight.
- Create lazily only when a term is resolved and useful.

For multiple contexts, use a root `CONTEXT-MAP.md` that points to local `CONTEXT.md` files. Do not create a multi-context layout unless the repo already needs it.

## ADRs

ADR means Architecture Decision Record. It records why a durable choice was made.

Create an ADR only when all are true:

- Hard to reverse.
- Surprising without context.
- Based on a real tradeoff among alternatives.

Do not create ADRs for:

- Ordinary failed experiments.
- Temporary status.
- Active next steps.
- Generic implementation details.
- Anything better explained in `STATUS.md` or `PLAN.md`.

Location:

- Follow existing repo convention.
- If no convention exists, prefer `spec/adr/` for research/spec-heavy repos.
- Otherwise prefer `docs/adr/`.

Filename:

```text
0001-short-slug.md
```

Minimal format:

```md
# Short title

One to three sentences: context, decision, and why.
```

Optional sections such as status, considered options, or consequences are allowed only when they add value.
