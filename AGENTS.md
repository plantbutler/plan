# Working on the plan

This is an [openproj](https://github.com/jcanton/openproj) repository: one markdown file per
record, YAML frontmatter for the fields, the shaping document as the body, git as the database.
Read the umbrella's [AGENTS.md](https://github.com/plantbutler/plantbutler/blob/main/AGENTS.md)
first for what the project is and where things stand.

## Running openproj

`openproj` is Jacopo's own tool, checked out at `~/projects/openproj/`. Either form works:

```bash
alias openproj='uv run --project ~/projects/openproj openproj'        # from the checkout
export OPENPROJ_STATIC=~/projects/openproj/static                     # if using the pip-installed one
openproj check .                    # every rule; exits non-zero only on blockers — run before every push
openproj schedule .                 # derived dates, one line per record, with the reason
openproj render . /tmp/plan-out     # static pages
git clone --bare . /tmp/plan.git && openproj serve --repo /tmp/plan.git --auth dev   # the editable UI
```

The pip-installed wheel does not carry `static/`, hence `OPENPROJ_STATIC`. Serve a **bare clone**,
not this checkout: a save from the browser moves the branch without touching the working tree.

## Writing records

Use `openproj new`; it mints the id, files the record under its kind's directory, starts the body
from the kind's template and refuses anything `check` would block:

```bash
openproj new pitch . --title "…" --set parent=proj-… --set person_weeks=0.5 --tag backend
openproj new note  . --title "…" --as jcanton        # an idea that is not yet a pitch
openproj new issue . --title "…" --as jcanton        # something existing that is broken
```

- `product ← project ← pitch`. Products are the repositories; projects are milestones; pitches are
  bets. There are no tasks yet, on purpose.
- Sizes are **person-weeks**. `nominal_availability` is 0.2 (a day a week); cycle files set it per
  person per cycle. Nobody types a forecast — dates are derived.
- Only `depends_on` is stored, on the record that waits. Any kind may wait on any kind.
- Statuses: `thinking → shaping → ready → in_progress → done`, or `shelved`. `ready` needs an
  owner, assignees, a reviewer (or `review_waived`) and a size; `in_progress` needs a
  `start_date`; `done` needs an `end_date` and a PR.
- Bodies are short: a few sentences under Problem / Appetite / Solution / Rabbit holes / No-gos.
  Jacopo asked twice not to go overboard.
- A cycle is `cycles/NNNN.md`: `starts_on` (betting table, first day of build), `reviews_on`, and
  `availability` per person. Its body is the notes from the betting table.
- Ids are random; use titles in prose and commit messages.

## State on 2026-08-30

Five products, six projects, fifteen pitches, three notes. Cycle 1 has four pitches `ready`
(see `cycles/0001.md`); everything else is `shaping` with an appetite and dependencies, so the
timeline can draw it. Known gap in the tool itself: a `parent` that names no record is not
reported — jcanton/openproj#178.
