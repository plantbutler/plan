# Plant Butler — the plan

The Shape Up plan for [Plant Butler](../README.md), kept as an
[openproj](https://github.com/jcanton/openproj) repository: one markdown file per record, the
fields in frontmatter and the shaping document as the body. Records are grouped
`product ← project ← pitch`; only `depends_on` is stored, and every date is derived from sizes,
dependencies and availability.

```bash
OP="uv run --project ~/projects/openproj openproj"
$OP check .                                   # every rule; exits non-zero only on blockers
$OP schedule .                                # derived dates, one line per record
$OP render . /tmp/plan-out && open /tmp/plan-out/index.html
git clone --bare . /tmp/plan.git && $OP serve --repo /tmp/plan.git --auth dev   # the editable UI
$OP new pitch . --title "…" --set parent=proj-… --set person_weeks=0.5          # a new record
```
