# Add promotable mockups alongside throwaway prototypes

The repo had one visual tool: [`prototype`](../../skills/engineering/prototype/SKILL.md). Its whole discipline is that it is **throwaway** — it answers one design question, carries no tests or abstractions, and is deleted once the answer is captured (the decision folded into real code, the prototype parked on a side branch). That discipline is what keeps it fast and honest.

But there is a second, distinct need the prototype deliberately does not serve: **seeing and aligning on a whole flow before building it**, cheaply, with an artifact you *keep and grow into the feature*. This is the opposite lifecycle — one polished direction across every screen of a flow, meant to become production, not to be thrown away. Forcing it through `prototype` would break prototype's throwaway rule (no polish, no persistence, several variations to compare); stretching `prototype` to be promotable would blur the one thing that makes it useful.

## The two are distinguished by lifecycle and question

| | `prototype` | `mockup` |
| --- | --- | --- |
| lifecycle | throwaway, deleted after | **promotable**, seeds the build (mock → real) |
| question | one open question | a whole flow, aligned end-to-end |
| shape | several radically different variations, to *choose* | one polished direction, to *align and seed* |
| stack | whatever is fastest, marked as scrap | the project's **real** UI stack + design tokens |

Collapsing them into one skill would force one lifecycle onto both needs. Keeping them separate lets each stay deep: `prototype` to *decide* cheaply and discard; `mockup` to *align* on a coherent flow and carry it into production.

## Decision

- Add a **`mockup`** skill (engineering, model-invoked): high-fidelity, promotable, whole-flow UI in the project's real stack with mock data behind a clear seam, on a dedicated route. It is reference-driven — it asks the user for references and binds them to the repo's own tokens.
- Keep **`prototype`** exactly as it is. The two coexist; [`ask-tutu`](../../skills/engineering/ask-tutu/SKILL.md) draws the boundary so neither is reached for in the other's situation.
- The mockup's scoping unit is a **wave** (see [`to-waves`](../../skills/engineering/to-waves/SKILL.md)) — a flow, not one ticket and not the whole app — and its semantic markup seeds the [`e2e`](../../skills/engineering/e2e/SKILL.md) tests, threading it into the traceability spine.

## Invariants this creates

- `mockup` must stay **promotable**: real components, real design tokens, mock data isolated behind one seam — never throwaway HTML, never a rewrite to promote. This is the line that separates it from `prototype`; a mockup that can't be promoted by swapping its data seam has become a prototype.
- `ask-tutu` must keep the `prototype` ↔ `mockup` boundary current — throwaway-to-decide vs promotable-to-align — so a stale router doesn't send work to the wrong tool.
- As a promoted (`engineering/`) skill, `mockup` carries an entry in the top-level `README.md`, the bucket `README.md`, `.claude-plugin/plugin.json`, and a docs page under `docs/engineering/`.
