# DESIGN.md Format

`DESIGN.md` is the project's **visual glossary** — the source of truth for its design language, sitting alongside `CONTEXT.md` (the domain glossary). It records *decisions*, not components: where the dials sit, the tokens taste resolves to, the type and motion language, and the slop this project specifically guards against.

## Structure

```md
# {Project} — Design Language

{One or two sentences: what this product is, and the feeling its UI should give.}

## Dials

- **Variance**: {low | medium | high} — {one line of why}
- **Motion**: {low | medium | high} — {one line}
- **Density**: {low | medium | high} — {one line}

## References

- {link or path} — {what we take from it: structure / rhythm / a specific pattern}

## Tokens

Point at where tokens actually live in the codebase; mirror only the decisions here.

- **Typeface(s)**: {display} / {body} — {why chosen}
- **Type scale**: {e.g. 1.25 modular, base 16px}
- **Accent**: {token name} — spent only on the primary action
- **Neutrals**: tinted toward {hue}; text is {near-black token}, never #000
- **Radius**: {scale} · **Elevation**: {shadow scale} · **Spacing**: {4/8px base}

## Motion language

- **Durations**: {tokens, e.g. fast 150ms / base 220ms}
- **Easing**: {default ease-out curve; where spring is used}
- **What animates**: {the surfaces that move} · **What stays still**: {the ones that don't}

## Guardrails

Project-specific anti-slop watches — the tells most likely to creep into *this* codebase.

- {e.g. "no gradients — flat fills only"}
- {e.g. "cards only for genuinely separable content; default to whitespace"}
```

## Rules

- **Record decisions, not inventory.** A chosen accent token and *why* belongs here; a list of every button variant does not — that lives in code.
- **Point at tokens, don't duplicate them.** Name where tokens live and mirror only the load-bearing choices, so `DESIGN.md` can't drift out of sync with the real token file.
- **Keep it a glossary.** No spec, no implementation notes — the same discipline that keeps `CONTEXT.md` pure.
- **Write lazily and inline.** Create `DESIGN.md` when the first choice crystallises; add to it the moment each later one does, never in a batch at the end.
